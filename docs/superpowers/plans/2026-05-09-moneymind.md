# MoneyMind by Jake Miller Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the current static personal finance site into a believable single-author publication, **MoneyMind by Jake Miller**, with stronger topic clustering, cleaner trust signals, and much less AI-generated site feel.

**Architecture:** Keep the site static and simple. Treat the home page as the brand and topic entry point, the blog page as a topic hub, trust/legal pages as credibility anchors, and article pages as the content layer. Make each page do one job, reuse the existing HTML/CSS shell, and remove anything that reads like a template, a monetization shell, or a fabricated expert persona.

**Tech Stack:** Static HTML, CSS, vanilla JS, XML sitemap, robots.txt, ads.txt, Google AdSense tags, Google Analytics tag.

---

### Task 1: Lock the site identity and remove brand drift

**Files:**
- Modify: `index.html`
- Modify: `blog.html`
- Modify: `about.html`
- Modify: `contact.html`
- Modify: `faq.html`
- Modify: `resources.html`
- Modify: `privacy-policy.html`
- Modify: `terms-of-service.html`
- Modify: `affiliate-disclosure.html`
- Modify: `blog/*.html`
- Modify: `sitemap.xml`

- [ ] **Step 1: Inventory every brand string and author string**

Run:
```bash
rg -n "AI Cool Finance|MoneyMind|Jake|Jake Miller|AICoolFinance|aicoolgames.cool|CFP|CFA|12K\+|team|expert" "f:/me/ads/模版/aicoolgames.cool2"
```
Expected: a complete list of every file that still mixes brand names, author names, or fake credibility signals.

- [ ] **Step 2: Replace the mixed identity with one stable identity**

Use these rules everywhere:
```text
siteName: MoneyMind
authorName: Jake Miller
brand phrasing: MoneyMind by Jake Miller
voice: personal, practical, calm, lived-in
```

Update the shared shell in each page:
- `<title>` should use MoneyMind or MoneyMind by Jake Miller
- `<meta name="author">` should be `Jake Miller`
- canonical, OG, and Twitter URLs should stay on `www.aicoolgames.cool`
- header logo text should be MoneyMind
- footer should not mention AI Cool Finance
- any “expert team” or “our team” language should be removed

- [ ] **Step 3: Re-run the inventory and confirm the drift is gone**

Run:
```bash
rg -n "AI Cool Finance|AICoolFinance|Jake\b|Jake Miller|MoneyMind|CFP|CFA|12K\+|team|expert" "f:/me/ads/模版/aicoolgames.cool2"
```
Expected: only the final chosen brand and author remain, with no leftover mixed-brand pages.

- [ ] **Step 4: Commit this identity pass**

```bash
git add index.html blog.html about.html contact.html faq.html resources.html privacy-policy.html terms-of-service.html affiliate-disclosure.html sitemap.xml blog/*.html
git commit -m "feat: unify site identity around MoneyMind"
```

---

### Task 2: Rebuild the home page as a real publication front door

**Files:**
- Modify: `index.html`
- Modify: `styles.css` if any home-page section needs layout support

- [ ] **Step 1: Rewrite the hero into a plain, credible author introduction**

The home page should answer three questions immediately:
1. Who is writing this
2. What the site covers
3. Why it is trustworthy

Use a restrained hero copy style with concrete personal framing, not hype. Remove or reduce lines that feel like marketing claims, including reader-count bragging and “life-changing” language.

- [ ] **Step 2: Turn the page into a topic-led front door**

Keep these home sections:
- short author intro
- 5 topic cards
- 3 to 6 featured articles
- a recent updates strip
- trust-page links

Use these topic names consistently:
- Debt Recovery
- Budgeting Basics
- Saving & Safety Net
- Beginner Investing
- Life & Money

- [ ] **Step 3: Remove anything that looks like an ad shell or placeholder section**

Delete empty ad containers and blank blocks that exist only to make the page feel monetized.
If a section does not add value before approval, remove it rather than leaving it empty.

- [ ] **Step 4: Verify the home page reads like a real editorial site**

Run:
```bash
rg -n "12K\+|No spam|Start Here|incredible|transform|life-changing|AI Cool Finance|ad-container" index.html
```
Expected: no fake growth claims, no leftover brand drift, and no empty ad scaffolding.

- [ ] **Step 5: Commit the homepage rebuild**

```bash
git add index.html styles.css
git commit -m "feat: make the homepage feel like a real publication"
```

---

### Task 3: Rework the blog page into topic hubs instead of a flat list

**Files:**
- Modify: `blog.html`
- Modify: `styles.css` if topic grouping needs layout styling

- [ ] **Step 1: Replace the flat filter-first layout with topic-first grouping**

Keep the blog page useful as a map of the site, not just a card grid.
Each topic section should include:
- a short explanation of what belongs in the topic
- 3 to 6 representative articles
- a suggested reading order

- [ ] **Step 2: Make the blog page feel curated, not generic**

Reduce SEO-ish copy like “comprehensive library” and “expert advice.”
Use short editorial notes that sound like a human editor organizing their own writing.

- [ ] **Step 3: Decide how to handle the Google AdSense guide article**

The article at `blog/google-adsense-guide.html` is a credibility risk because it makes the site look self-referential and monetization-first.
Either:
- move it to a lower-visibility role in the blog hub, or
- rewrite it so it fits the personal finance voice and no longer feels like a site-monetization tutorial.

- [ ] **Step 4: Verify the blog page no longer looks like a content farm index**

Run:
```bash
rg -n "comprehensive library|expert advice|Make Money|AdSense|All|Budgeting|Investing|Debt|Retirement|Saving" blog.html
```
Expected: the page presents topics with editorial context, not a generic SEO grid.

- [ ] **Step 5: Commit the blog hub rewrite**

```bash
git add blog.html styles.css blog/google-adsense-guide.html
git commit -m "feat: reorganize the blog into topic hubs"
```

---

### Task 4: Rewrite the trust pages into one coherent single-author story

**Files:**
- Modify: `about.html`
- Modify: `contact.html`
- Modify: `privacy-policy.html`
- Modify: `terms-of-service.html`
- Modify: `faq.html`
- Modify: `affiliate-disclosure.html`
- Modify: `resources.html`

- [ ] **Step 1: Rewrite About as a believable author page**

Frame Jake as a normal person who learned money lessons the hard way, not as a finance authority with fake credentials.
Remove inflated claims, vague team language, and overly polished “mission statement” copy.

- [ ] **Step 2: Rewrite Contact to look like a real contact page**

Keep a real email address and a clear purpose for contact.
If the form stays, it should be a functional-looking feedback path, not a shell.
Make the page feel like someone can actually reach the author.

- [ ] **Step 3: Rewrite Privacy, Terms, FAQ, and Affiliate Disclosure with plain language**

The goal is to sound like a real small publication, not a policy template factory.
Cover cookies, analytics, AdSense, affiliate links, third-party resources, and contact email handling in straightforward language.

- [ ] **Step 4: Make resources and FAQ support the site voice instead of repeating it**

These pages should reinforce the personal finance topic and the single-author model without sounding like duplicated homepage copy.

- [ ] **Step 5: Verify no trust page still uses the old mixed identity**

Run:
```bash
rg -n "AI Cool Finance|AICoolFinance|team|expert|CFP|CFA|12K\+|fiscal responsibility|portfolio diversification" about.html contact.html privacy-policy.html terms-of-service.html faq.html affiliate-disclosure.html resources.html
```
Expected: no fake authority language and no leftover brand drift.

- [ ] **Step 6: Commit the trust-page rewrite**

```bash
git add about.html contact.html privacy-policy.html terms-of-service.html faq.html affiliate-disclosure.html resources.html
git commit -m "feat: rewrite trust pages for a single-author site"
```

---

### Task 5: Rebuild the article corpus into topic clusters and remove AI-like patterns

**Files:**
- Modify: `blog/budgeting-101.html`
- Modify: `blog/cut-monthly-expenses.html`
- Modify: `blog/automate-finances.html`
- Modify: `blog/frugal-lifestyle.html`
- Modify: `blog/meal-planning-budget.html`
- Modify: `blog/paycheck-to-saving-50-percent.html`
- Modify: `blog/high-yield-savings.html`
- Modify: `blog/emergency-fund.html`
- Modify: `blog/debt-snowball-vs-avalanche.html`
- Modify: `blog/improve-credit-score.html`
- Modify: `blog/investing-101.html`
- Modify: `blog/401k-vs-ira.html`
- Modify: `blog/retirement-planning-guide.html`
- Modify: `blog/tax-strategies.html`
- Modify: `blog/passive-income-streams.html`
- Modify: `blog/negotiate-salary.html`
- Modify: `blog/first-time-home-buyer.html`
- Modify: `blog/college-savings.html`
- Modify: `blog/insurance-guide.html`
- Modify: `blog/travel-hacking.html`
- Modify: `blog/credit-card-rewards-strategy.html`
- Modify: `blog/talk-to-partner-about-money.html`
- Modify: `blog/best-side-hustles-2026.html`
- Modify: `blog/financial-freedom-roadmap.html`
- Modify: `blog/daily-habits-wealth.html`
- Modify: `blog/google-adsense-guide.html`

- [ ] **Step 1: Group the articles by topic before editing copy**

Use these clusters:
- Debt Recovery: `debt-snowball-vs-avalanche.html`, `improve-credit-score.html`, `emergency-fund.html`
- Budgeting Basics: `budgeting-101.html`, `cut-monthly-expenses.html`, `automate-finances.html`, `frugal-lifestyle.html`, `meal-planning-budget.html`, `paycheck-to-saving-50-percent.html`, `high-yield-savings.html`
- Beginner Investing: `investing-101.html`, `401k-vs-ira.html`, `retirement-planning-guide.html`, `tax-strategies.html`, `passive-income-streams.html`
- Life & Money: `negotiate-salary.html`, `first-time-home-buyer.html`, `college-savings.html`, `insurance-guide.html`, `travel-hacking.html`, `credit-card-rewards-strategy.html`, `talk-to-partner-about-money.html`, `best-side-hustles-2026.html`, `financial-freedom-roadmap.html`, `daily-habits-wealth.html`

- [ ] **Step 2: Rewrite article openings to sound like a person, not a template**

Each article should use a different opening style depending on the topic:
- a short personal scene
- a concrete mistake
- a decision point with trade-offs
- a direct answer to the reader’s problem

Do not reuse the same introduction structure across every article.

- [ ] **Step 3: Rewrite titles and summaries to reduce AI polish**

Titles should be specific and human, not formulaic.
Prefer ordinary phrasing and avoid overhyped patterns like “ultimate guide,” “comprehensive guide,” or “transform your finances.”
Keep useful titles, but make them sound like something a real person would actually publish.

- [ ] **Step 4: Normalize author, date, and reading-time metadata**

Use the same author name everywhere and make date/reading-time patterns consistent enough to feel maintained, but not so uniform that the site looks generated in a batch.

- [ ] **Step 5: Add stronger internal links within each topic cluster**

Every article should link to at least one sibling article and one topic hub path from the blog page.
This is what makes the site feel curated and maintained instead of random.

- [ ] **Step 6: Review the AdSense article as part of the rewrite pass**

For `blog/google-adsense-guide.html`, either tone it down so it fits the money site voice or reduce its prominence if it keeps making the site feel self-referential.

- [ ] **Step 7: Verify the article corpus no longer reads like a generated batch**

Run:
```bash
rg -n "ultimate guide|comprehensive guide|transform your finances|expert advice|in today's fast-paced world|unlock|power of|the beauty of|let me break down|real talk" blog/*.html
```
Expected: the most AI-sounding stock phrases are gone or reduced to a tiny minority.

- [ ] **Step 8: Commit the article rewrite batch**

```bash
git add blog/*.html
git commit -m "feat: rewrite articles for stronger topic clusters and human voice"
```

---

### Task 6: Clean the technical trust layer and ensure the site matches what is published

**Files:**
- Modify: `sitemap.xml`
- Modify: `robots.txt`
- Modify: `ads.txt`
- Modify: `index.html`
- Modify: `blog.html`
- Modify: `about.html`
- Modify: `contact.html`
- Modify: `privacy-policy.html`
- Modify: `terms-of-service.html`
- Modify: `affiliate-disclosure.html`
- Modify: `faq.html`
- Modify: `resources.html`
- Modify: `blog/*.html`
- Modify: `styles.css` if any empty ad containers or trust sections need visual cleanup

- [ ] **Step 1: Align sitemap entries with the actual published pages**

Add every live HTML page and every real article page to `sitemap.xml`.
Use the exact published file URLs, not invented paths.
Keep the last-mod values believable and current.

- [ ] **Step 2: Keep robots.txt simple and crawl-friendly**

Allow normal crawling, block only real private or temporary directories if they exist, and keep the sitemap line correct.
Do not add unnecessary directives that make the site look engineered for bots.

- [ ] **Step 3: Keep ads.txt accurate and non-distracting**

Leave `ads.txt` as the AdSense authorization file only.
Do not add extra marketing text or filler.

- [ ] **Step 4: Remove any leftover empty ad containers or dead layout blocks**

If a page has an ad container that exists only as a placeholder, remove it before approval.
This lowers the “site built for monetization first” impression.

- [ ] **Step 5: Run a full-site consistency scan**

Run:
```bash
rg -n "AI Cool Finance|AICoolFinance|12K\+|CFP|CFA|team|expert|ad-container|adsbygoogle|placeholder|TODO|TBD" "f:/me/ads/模版/aicoolgames.cool2"
```
Expected: only intentional AdSense/analytics references remain, and no placeholder or fake-author signals are left.

- [ ] **Step 6: Check the site locally in a browser**

Run:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000/` and inspect:
- home page brand clarity
- blog topic grouping
- About/Contact trust signals
- article tone
- no obvious AI-generated feel

- [ ] **Step 7: Commit the final technical cleanup**

```bash
git add sitemap.xml robots.txt ads.txt index.html blog.html about.html contact.html privacy-policy.html terms-of-service.html affiliate-disclosure.html faq.html resources.html blog/*.html styles.css
git commit -m "chore: align sitemap and site structure with published content"
```

---

### Self-review checklist before implementation starts

- [ ] Every requirement from `docs/superpowers/specs/2026-05-09-moneymind-design.md` has a matching task.
- [ ] No task says “TBD”, “TODO”, “later”, or “similar to above.”
- [ ] Every file path is exact and real.
- [ ] The plan explicitly addresses the user’s main concern: the site should not look obviously AI-generated.
- [ ] The plan keeps the site single-author, personal-finance, and AdSense-friendly without adding unnecessary complexity.
