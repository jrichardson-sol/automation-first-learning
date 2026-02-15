# Contributing to Automation-First Learning

First off, **thank you** for considering contributing! This framework gets better when people share their real-world automation wins.

The goal is simple: **help others learn any domain by building systems instead of grinding hours.**

---

## 🎯 What Makes a Great Contribution

We're looking for **practical, tested automations** that:

1. **Save significant time** - At least 5+ hours per month
2. **Are reproducible** - Others can follow your steps and get similar results
3. **Include real numbers** - Actual build time, time saved, ROI
4. **Show the journey** - Manual → MVP → Scaled, not just the end state
5. **Are domain-specific** - Tied to a particular field, not generic productivity tips

---

## 📝 Types of Contributions We Love

### 1. New Domain Examples

**Best contributions:** Complete domain breakdowns following our framework

**What to include:**
- Domain name and context
- 3-5 manual bottlenecks (ranked by impact)
- MVP automation with code/setup instructions
- Scaling path (weeks 2-8)
- ROI breakdown with real numbers
- Common pitfalls and leverage points

**File location:** `domains/your-domain-name.md`

**Template:** See `templates/domain-template.md`

### 2. Working Code Examples

**We need:**
- Google Ads Scripts
- Excel/Sheets automation
- Python scripts for data processing
- Zapier/Make workflow templates
- API integration examples

**File location:** `examples/tool-or-platform/script-name.ext`

**Requirements:**
- Include setup instructions
- Add comments explaining logic
- Note any API keys or dependencies
- Provide example data if possible

### 3. Tool Comparisons

**Helpful additions:**
- "Zapier vs Make vs n8n for [use case]"
- "When to use Python vs no-code tools"
- "Free tiers comparison for automation tools"

**File location:** `resources/tool-comparisons.md`

### 4. Templates & Calculators

**What helps:**
- ROI calculators for specific domains
- Decision trees ("which tool should I use?")
- Process documentation templates
- Automation audit checklists

**File location:** `templates/` or `calculators/`

### 5. Bug Fixes & Improvements

- Typos, broken links, outdated info
- Better explanations
- Code optimizations
- Mobile/accessibility improvements

---

## 🚀 How to Contribute

### Quick Contributions (Typos, Small Fixes)

1. Click "Edit" on the file in GitHub
2. Make your change
3. Submit a pull request
4. We'll review and merge quickly

### Domain Examples & Code (Bigger Contributions)

**Step 1: Check Existing Content**
- Review `domains/` folder
- Make sure your domain isn't already covered
- If it is, consider improving the existing example

**Step 2: Fork & Clone**
```bash
git clone https://github.com/[your-username]/automation-first-learning.git
cd automation-first-learning
```

**Step 3: Create Your Branch**
```bash
git checkout -b add-domain-[domain-name]
# or
git checkout -b add-example-[tool-name]
```

**Step 4: Add Your Content**

For domain examples, use this structure:

```markdown
# [Domain Name] - Automation Blueprint

> One-line hook with outcome

## 🎯 The Problem
Describe the manual pain...

## 🔍 Manual Bottlenecks (Ranked by Impact)
### 1. [Bottleneck Name] ⚡ Highest ROI
- Frequency: [how often]
- Manual process: [what people do now]
- Pain level: [High/Medium/Low]
- Automation potential: [percentage]

[Continue for 3-5 bottlenecks]

## 🚀 MVP Automation (Week 1-2)
**Tool Stack:** [list tools]
**How It Works:** [explain the workflow]
**Build Time:** [realistic estimate]
**Expected Results:** [what they'll achieve]

### Implementation [Code/Setup]
[Provide actual working code or detailed setup steps]

## 📈 Scaling Path
[Week-by-week progression]

## 💰 ROI Breakdown
[Manual baseline vs automated state with numbers]

## ⚠️ Common Pitfalls
[Things that typically go wrong]

## 🎯 Leverage Points
[Where small improvements create big gains]
```

**Step 5: Test Your Content**
- If it's code, make sure it runs
- If it's a process, walk through each step
- Check that links work
- Run through spell check

**Step 6: Commit & Push**
```bash
git add .
git commit -m "Add [domain name] automation example"
git push origin add-domain-[domain-name]
```

**Step 7: Open Pull Request**
- Go to the original repo on GitHub
- Click "New Pull Request"
- Select your branch
- Fill out the PR template

---

## ✅ PR Checklist

Before submitting, make sure:

- [ ] Content follows the framework structure
- [ ] Real numbers included (build time, time saved, ROI)
- [ ] Code tested and working (if applicable)
- [ ] Links are valid
- [ ] Spelling and grammar checked
- [ ] File is in the correct folder
- [ ] Markdown renders properly
- [ ] Examples use realistic scenarios
- [ ] Success metrics are measurable

---

## 📋 PR Template

When you open a PR, please include:

```markdown
## What does this add?
[Brief description]

## Type of contribution
- [ ] New domain example
- [ ] Code example
- [ ] Tool comparison
- [ ] Template/calculator
- [ ] Bug fix
- [ ] Documentation improvement

## Have you tested this?
- [ ] Yes, I've built and used this automation
- [ ] Yes, I've tested the code
- [ ] Yes, I've verified all links work
- [ ] No, this is theoretical/untested

## Results you've seen
- Build time: [X hours]
- Time saved: [X hours/month]
- Break-even point: [X months]
- Other benefits: [list]

## Additional context
[Any other info we should know]
```

---

## 🎨 Style Guidelines

### Writing Style
- **Be direct** - Get to the point quickly
- **Use real numbers** - "Saves 4 hours/month" not "saves time"
- **Show, don't tell** - Include actual code and examples
- **Be honest** - Include what didn't work, not just wins
- **Skip the fluff** - No "in today's fast-paced world" intros

### Code Style
- **Comment generously** - Explain the why, not just the what
- **Use descriptive names** - `calculate_roi()` not `calc()`
- **Include error handling** - Show how to catch failures
- **Provide examples** - Add sample data or test cases
- **Note dependencies** - List all required packages/tools

### Formatting
- Use emojis sparingly for section headers only
- Keep line length under 100 characters for code
- Use `code blocks` for commands and file names
- Bold for **emphasis** on key points
- Use > blockquotes for important warnings

---

## 🚫 What We Don't Accept

**Hard pass on:**
- Theoretical automations you haven't built
- Generic productivity tips ("use Pomodoro technique")
- Affiliate links or paid tool promotions
- AI-generated content without real-world testing
- Copying existing content from other sources
- Anything that violates terms of service
- Incomplete examples without working code

**We're skeptical of:**
- Claims without supporting data
- "This should work but I haven't tried it"
- Overly complex solutions for simple problems
- Domain examples with <3 bottlenecks identified

---

## 🏆 Recognition

Contributors get:
- Name in the contributors list
- Credit in the specific file you contributed
- Our eternal gratitude
- Bragging rights for helping others escape manual work

**Top contributors** (most impactful additions) may be featured in:
- README showcase section
- Social media shoutouts
- "Featured Domain" spotlights

---

## 💬 Questions?

**Not sure if your contribution fits?** Open an issue and describe what you want to add. We'll give feedback before you spend time building it.

**Need help with the PR process?** Check out [GitHub's PR guide](https://docs.github.com/en/pull-requests) or open an issue asking for help.

**Want to discuss big changes?** Open an issue first so we can align on direction before you build.

---

## 📜 Code of Conduct

**TL;DR: Don't be a jerk.**

We're here to help each other build better systems. That means:
- Be respectful and constructive in feedback
- Assume good intentions
- Focus on ideas, not people
- Help newcomers learn
- Give credit where it's due

If someone's being problematic, report it to the maintainers.

---

## 🔄 Review Process

**What happens after you submit a PR:**

1. **Initial review** (1-3 days) - We check if it fits the framework
2. **Feedback** - We may suggest changes or ask questions
3. **Iteration** - Make requested changes (or discuss why you disagree)
4. **Approval** - Once it's good, we merge it
5. **Thanks!** - You've made the framework better for everyone

**Most PRs get merged within a week.** If yours is taking longer, ping us in the PR comments.

---

## 🙏 Thank You

Every contribution makes this framework more valuable. Whether you're adding a full domain example or fixing a typo, **you're helping others escape the manual work trap.**

Let's build systems together.

**Now go automate something and share what you learned!** 🚀