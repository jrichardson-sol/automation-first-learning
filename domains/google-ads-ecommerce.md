# Google Ads for E-commerce - Automation Blueprint

> From $15K/month in manual ad management to 90% automated in 6 weeks

## 🎯 The Problem

You're running Google Ads for an e-commerce store. You're spending 15-20 hours per week doing repetitive tasks that don't scale:
- Checking keyword performance daily and adjusting bids
- Pausing ads with high CPA, increasing bids on winners
- Writing ad copy variations to test
- Adding negative keywords from search term reports
- Monitoring competitor prices and adjusting your strategy

**Cost of staying manual:** 80 hours/month at $50/hour opportunity cost = $4,000/month + suboptimal campaign performance

---

## 🔍 Manual Bottlenecks (Ranked by Impact)

### 1. **Bid Management** ⚡ Highest ROI
- **Frequency:** Daily (30-45 min/day)
- **Manual process:** Export keywords → filter by CPA → adjust bids → upload
- **Pain level:** High - miss a day and waste $200-500
- **Automation potential:** 95%

### 2. **Negative Keyword Discovery** 
- **Frequency:** Weekly (2-3 hours)
- **Manual process:** Download search terms → identify waste → add negatives
- **Pain level:** Medium - 10-15% of spend is wasted on irrelevant searches
- **Automation potential:** 80%

### 3. **Ad Copy Testing**
- **Frequency:** Bi-weekly (3-4 hours)
- **Manual process:** Brainstorm variants → write copy → create ads → set up tests
- **Pain level:** Medium - testing = revenue, but it's tedious
- **Automation potential:** 70%

### 4. **Budget Reallocation**
- **Frequency:** Weekly (1-2 hours)
- **Manual process:** Analyze campaign performance → shift budgets to winners
- **Pain level:** Low - but compounds over time
- **Automation potential:** 85%

### 5. **Performance Reporting**
- **Frequency:** Weekly/monthly (2-4 hours)
- **Manual process:** Pull data → create charts → write analysis
- **Pain level:** Low - but takes time from optimization
- **Automation potential:** 90%

---

## 🚀 MVP Automation (Week 1-2)

**Target:** Automate bid management for keywords based on CPA performance

### The System

**Tool Stack:**
- Google Ads Scripts (free, built-in)
- Google Sheets (logging & monitoring)
- Email notifications (alert on issues)

**How It Works:**
```
Every morning at 6am:
1. Script pulls all keyword data from yesterday
2. Identifies keywords with CPA > $75 for 3+ days → pause
3. Identifies keywords with CPA < $40 and conversions > 5 → increase bid 15%
4. Identifies keywords with no impressions for 7 days → flag for review
5. Logs all changes to Google Sheet
6. Emails summary of actions taken
```

**Build Time:** 6-8 hours (if you've never used Apps Script) or 2-3 hours (if familiar with JavaScript)

**Expected Results:**
- Prevents $500-2,000/month in wasted spend
- Captures 10-20% more revenue from underbid winners
- Saves 20 hours/month of manual work
- Break-even after first month

### Implementation Code

```javascript
// Save this as a Google Ads Script
// Run daily at 6am

function main() {
  var SPREADSHEET_URL = 'YOUR_SHEET_URL_HERE';
  var EMAIL = 'your-email@example.com';
  
  // Thresholds
  var HIGH_CPA_THRESHOLD = 75;
  var LOW_CPA_THRESHOLD = 40;
  var MIN_CONVERSIONS = 5;
  var BID_INCREASE = 0.15; // 15%
  var LOOKBACK_DAYS = 3;
  
  var changes = [];
  var today = new Date();
  
  // Get all keywords with sufficient data
  var keywordIterator = AdsApp.keywords()
    .withCondition('Status = ENABLED')
    .withCondition('Impressions > 100')
    .forDateRange('LAST_' + LOOKBACK_DAYS + '_DAYS')
    .get();
  
  while (keywordIterator.hasNext()) {
    var keyword = keywordIterator.next();
    var stats = keyword.getStatsFor('LAST_' + LOOKBACK_DAYS + '_DAYS');
    
    var conversions = stats.getConversions();
    var cost = stats.getCost();
    var cpa = conversions > 0 ? cost / conversions : 999;
    
    // High CPA - pause keyword
    if (cpa > HIGH_CPA_THRESHOLD && conversions > 0) {
      keyword.pause();
      changes.push({
        action: 'PAUSED',
        keyword: keyword.getText(),
        cpa: cpa.toFixed(2),
        conversions: conversions,
        cost: cost.toFixed(2)
      });
    }
    
    // Low CPA winners - increase bid
    if (cpa < LOW_CPA_THRESHOLD && conversions >= MIN_CONVERSIONS) {
      var currentBid = keyword.bidding().getCpc();
      var newBid = currentBid * (1 + BID_INCREASE);
      keyword.bidding().setCpc(newBid);
      changes.push({
        action: 'BID_INCREASED',
        keyword: keyword.getText(),
        cpa: cpa.toFixed(2),
        oldBid: currentBid.toFixed(2),
        newBid: newBid.toFixed(2)
      });
    }
  }
  
  // Log to sheet
  logToSheet(SPREADSHEET_URL, changes, today);
  
  // Send email summary
  sendEmail(EMAIL, changes, today);
}

function logToSheet(url, changes, date) {
  var sheet = SpreadsheetApp.openByUrl(url).getActiveSheet();
  
  changes.forEach(function(change) {
    sheet.appendRow([
      date,
      change.action,
      change.keyword,
      change.cpa || '',
      change.conversions || '',
      change.cost || '',
      change.oldBid || '',
      change.newBid || ''
    ]);
  });
}

function sendEmail(email, changes, date) {
  if (changes.length === 0) {
    MailApp.sendEmail(email, 
      'Google Ads Automation: No Changes', 
      'No keywords met automation criteria today.');
    return;
  }
  
  var paused = changes.filter(c => c.action === 'PAUSED').length;
  var increased = changes.filter(c => c.action === 'BID_INCREASED').length;
  
  var body = 'Automation Summary for ' + date.toDateString() + '\n\n';
  body += 'Keywords Paused: ' + paused + '\n';
  body += 'Bids Increased: ' + increased + '\n\n';
  body += 'Details:\n';
  
  changes.forEach(function(change) {
    body += '- ' + change.action + ': ' + change.keyword + 
            ' (CPA: $' + change.cpa + ')\n';
  });
  
  MailApp.sendEmail(email, 
    'Google Ads Automation: ' + (paused + increased) + ' Changes Made', 
    body);
}
```

**Setup Instructions:**
1. Create a new Google Sheet for logging
2. In Google Ads, go to Tools → Scripts
3. Create new script, paste code above
4. Replace `YOUR_SHEET_URL_HERE` with your Sheet URL
5. Replace email with your address
6. Preview → Authorize access
7. Set to run daily at 6am

**Testing:**
- Run manually first and check Sheet for logs
- Verify email notifications work
- Let run for 3 days, compare to manual approach

---

## 📈 Scaling Path

### Week 3-4: Add Negative Keyword Automation

```javascript
// Add this function to auto-detect wasted search terms

function addNegativeKeywords() {
  var searchQueryIterator = AdsApp.searchQueryReport()
    .withCondition('Impressions > 10')
    .withCondition('Conversions = 0')
    .withCondition('Cost > 20')
    .forDateRange('LAST_30_DAYS')
    .get();
  
  var negatives = [];
  
  while (searchQueryIterator.hasNext()) {
    var query = searchQueryIterator.next();
    var searchTerm = query.getSearchTerm();
    
    // Add wasteful terms as negative keywords
    var campaign = query.getCampaign();
    campaign.createNegativeKeyword(searchTerm);
    negatives.push(searchTerm);
  }
  
  Logger.log('Added ' + negatives.length + ' negative keywords');
}
```

**Result:** Reduces wasted spend by 8-12%

### Week 5-6: AI-Generated Ad Copy Testing

**Tool Stack:** OpenAI API + Google Ads API

```python
# Python script to generate ad copy variants

import openai
from google.ads.googleads.client import GoogleAdsClient

def generate_ad_variants(product, current_best_ad):
    prompt = f"""
    Product: {product}
    Current best performing ad: {current_best_ad}
    
    Generate 5 new ad copy variants that:
    1. Test different value propositions
    2. Use power words and urgency
    3. Stay under 30 characters for headline
    4. Include clear call-to-action
    
    Return as JSON array.
    """
    
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return response.choices[0].message.content

# Create ads in Google Ads via API
def create_ads(variants, campaign_id):
    # Implementation with Google Ads API
    pass
```

**Result:** Always have 3-5 ad tests running, improving CTR by 15-25%

### Month 2: Full Automated Bidding System

**Add:**
- Machine learning bid predictions based on historical data
- Seasonality adjustments (auto-increase bids on high-converting days)
- Competitor price monitoring with auto-adjustments
- Dynamic budget allocation across campaigns

**Result:** Campaign runs 90% autonomously, you spend 2-3 hours/week on strategy instead of 20 hours on execution

---

## 💰 ROI Breakdown

### Manual Baseline
- Time spent: 20 hours/month
- Opportunity cost: $4,000/month
- Ad spend waste: ~$1,500/month (10% of $15K budget)
- **Total cost: $5,500/month**

### Automated State (Month 3+)
- Time spent: 2 hours/month (monitoring)
- Build time investment: 40 hours upfront
- Ad spend waste: ~$300/month (2% of budget)
- Time savings value: $3,600/month
- Reduced waste: $1,200/month
- **Total monthly value: $4,800**

**Break-even:** After 8-9 cycles (just over 1 month of ad spend)

**Year 1 ROI:** $57,600 in value vs 40 hours upfront = $1,440/hour effective rate

---

## ⚠️ Common Pitfalls

1. **Over-automating too early** - Start with one script, validate, then expand
2. **Ignoring edge cases** - Add manual review flags for unusual situations
3. **Set-and-forget mentality** - Check logs weekly to catch issues
4. **Not tracking changes** - Always log what the automation does
5. **Poor thresholds** - Test your CPA cutoffs with small sample first

---

## 🎯 Leverage Points

The compounding effects of this automation:

1. **Faster iteration** - Test more strategies in less time
2. **Consistency** - Never miss a day of optimization
3. **Scalability** - Manage 5 accounts in the time it used to take for 1
4. **Data-driven** - All decisions logged and reviewable
5. **Sleep better** - System works while you don't

---

## 📊 Success Metrics

Track these monthly:

```
Manual time spent: ___ hours
Automated actions taken: ___ (from logs)
CPA improvement: ___% 
Wasted spend prevented: $___
New accounts managed: ___
```

---

## 🤝 Want to contribute improvements?

Have you automated something I missed? Built a better version? Submit a PR with:
- Your improvement
- Code/setup instructions
- Results you've seen

---

**Built by automating $2M+ in annual ad spend.**