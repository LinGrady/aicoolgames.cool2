# AdSense Audit Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Audit and harden the static MoneyMind site so it looks like a credible, single-author personal finance publication with fewer Google AdSense review risks.

**Architecture:** Keep the site as static HTML/CSS. First produce a concrete audit report, then fix P0 technical/trust risks, then fix P1 credibility and content-quality risks, leaving only lower-priority P2 polish for later. Avoid new frameworks, fake authority signals, or broad rewrites that do not directly improve AdSense readiness.

**Tech Stack:** Static HTML, CSS, XML sitemap, robots.txt, ads.txt, Google Analytics tag, Google AdSense publisher metadata.

---

## File Structure

- Create: `docs/adsense-audit-report.md` — the working audit report with P0/P1/P2 findings and final status.
- Modify: `index.html` — homepage identity, ad-placeholder cleanup, credibility copy, navigation/footer consistency.
- Modify: `blog.html` — blog hub audit fixes, brand consistency, ad-placeholder cleanup, topic structure risk notes.
- Modify: `about.html` — author credibility and trust copy.
- Modify: `contact.html` — contact purpose, correction path, realistic small-site tone.
- Modify: `privacy-policy.html` — cookies, analytics, AdSense, third-party and email handling language.
- Modify: `terms-of-service.html` — content disclaimer and site usage language.
- Modify: `affiliate-disclosure.html` — affiliate and editorial independence disclosure.
- Modify: `faq.html` — remove low-value repetition and align with single-author site.
- Modify: `resources.html` — ensure it is useful rather than an empty resources shell.
- Modify: `blog/*.html` — targeted metadata/identity/ad-shell/high-risk phrase cleanup only.
- Modify: `sitemap.xml` — match actual live pages.
- Modify: `robots.txt` — keep crawl-friendly and point to the sitemap.
- Modify: `ads.txt` — keep publisher authorization accurate and minimal.
- Modify: `styles.css` — only if removing ad placeholders leaves layout gaps or if audit report links reveal broken visual spacing.

---

### Task 1: Create the AdSense audit report skeleton

**Files:**
- Create: `docs/adsense-audit-report.md`

- [ ] **Step 1: Create the report with explicit review criteria**

Write `docs/adsense-audit-report.md` with this exact structure:

```markdown
# Google AdSense Site Audit Report

## Audit Goal

Make MoneyMind look like a credible, single-author personal finance publication and reduce Google AdSense review risks.

## P0: Strong Review Risks

| Status | Area | Finding | Evidence | Fix |
| --- | --- | --- | --- | --- |

## P1: Quality and Trust Risks

| Status | Area | Finding | Evidence | Fix |
| --- | --- | --- | --- | --- |

## P2: Later Optimization

| Status | Area | Finding | Evidence | Fix |
| --- | --- | --- | --- | --- |

## Pages Reviewed

- Home: `index.html`
- Blog hub: `blog.html`
- Trust pages: `about.html`, `contact.html`, `privacy-policy.html`, `terms-of-service.html`, `affiliate-disclosure.html`, `faq.html`, `resources.html`
- Articles: `blog/*.html`
- Technical files: `sitemap.xml`, `robots.txt`, `ads.txt`

## Final Readiness Notes

- P0 open items:
- P1 open items:
- P2 deferred items:
```

- [ ] **Step 2: Verify the report exists**

Run:
```bash
test -f "docs/adsense-audit-report.md" && printf "audit report created\n"
```
Expected: `audit report created`

---

### Task 2: Inventory P0/P1/P2 risks across the site

**Files:**
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Scan for brand drift and fake authority signals**

Run:
```bash
rg -n "AI Cool Finance|AI Cool|AICoolFinance|MoneyMind|Jake|Jake Miller|expert|team|CFP|CFA|12,000|12K\+|proven strategies|transform" "f:/me/ads/模版/aicoolgames.cool2" --glob "*.html" --glob "!**/.claude/**"
```
Expected: matches show whether pages still mix old brand names, inflated trust claims, or generic authority language.

- [ ] **Step 2: Scan for ad placeholders and monetization-first signals**

Run:
```bash
rg -n "adsbygoogle|ad-container|data-ad-slot|Top Ad Banner|Ad Banner|Google AdSense" "f:/me/ads/模版/aicoolgames.cool2" --glob "*.html" --glob "!**/.claude/**"
```
Expected: matches show where ad scripts or empty ad blocks appear before approval.

- [ ] **Step 3: Scan for placeholder, empty, and AI-like phrases**

Run:
```bash
rg -n "TODO|TBD|placeholder|lorem|ultimate guide|comprehensive guide|in today's fast-paced world|unlock|power of|game-changer|revolutionize|expert advice" "f:/me/ads/模版/aicoolgames.cool2" --glob "*.html" --glob "!**/.claude/**"
```
Expected: matches identify content that may read as low-value, generated, or unfinished.

- [ ] **Step 4: Scan live page references for broken links**

Run:
```bash
python - <<'PY'
from pathlib import Path
import re
root = Path('f:/me/ads/模版/aicoolgames.cool2')
files = [p for p in root.rglob('*.html') if '.claude' not in p.parts]
missing = []
for p in files:
    text = p.read_text(encoding='utf-8', errors='ignore')
    for href in re.findall(r'href="([^"]+)"', text):
        if href.startswith(('http://','https://','mailto:','#','javascript:')):
            continue
        if href.endswith('/'):
            target = (p.parent / href / 'index.html').resolve()
        else:
            target = (p.parent / href.split('#')[0].split('?')[0]).resolve()
        if href and not target.exists():
            missing.append((p.relative_to(root).as_posix(), href))
for page, href in missing:
    print(f'{page} -> {href}')
print(f'MISSING_LINKS={len(missing)}')
PY
```
Expected: `MISSING_LINKS=0` or a list of exact links to fix.

- [ ] **Step 5: Update the report with actual findings**

Add rows to `docs/adsense-audit-report.md` using this format:

```markdown
| Open | P0 | Mixed brand identity remains on trust/legal pages | `terms-of-service.html` uses AI Cool Finance while homepage uses MoneyMind | Replace with MoneyMind by Jake Miller and author `Jake Miller` |
| Open | P0 | Ad placeholders appear before approval | `blog.html` contains `adsbygoogle` ad slot markup | Remove visible ad blocks and keep only required policy/ads.txt references |
| Open | P1 | Homepage trust claims sound inflated | `index.html` claims 12K+ monthly readers without supporting evidence | Replace with restrained author-first copy |
```

Only include rows backed by scan evidence.

---

### Task 3: Fix P0 brand identity and authority drift

**Files:**
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
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Apply the canonical site identity everywhere**

Use these exact identity rules:

```text
siteName: MoneyMind
authorName: Jake Miller
siteLabel: MoneyMind by Jake Miller
domain: https://www.aicoolgames.cool
voice: practical, plain-spoken, single-author, not credential-inflated
```

For every HTML page:
- `<meta name="author">` must be `Jake Miller`.
- Header logo must read `Money<span>Mind</span>` or equivalent MoneyMind-only markup.
- Footer brand references must use `MoneyMind` or `MoneyMind by Jake Miller`.
- Remove `AI Cool Finance`, `AI Cool`, and `AICoolFinance` from visible copy and metadata.
- Replace `team`, `experts`, `expert advice`, and credential-like language with first-person or publication-neutral wording.

- [ ] **Step 2: Verify old brand strings are gone from public HTML**

Run:
```bash
rg -n "AI Cool Finance|AI Cool|AICoolFinance|CFP|CFA|team of experts|our experts|expert advice|12K\+|12,000" "f:/me/ads/模版/aicoolgames.cool2" --glob "*.html" --glob "!**/.claude/**"
```
Expected: no matches, unless a match is inside historical documentation rather than public HTML.

- [ ] **Step 3: Mark resolved report rows**

For each brand/authority row fixed in `docs/adsense-audit-report.md`, change `Open` to `Fixed` and keep the evidence row intact.

---

### Task 4: Fix P0 ad-shell and monetization-first signals

**Files:**
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
- Modify: `styles.css` if empty ad layout styles are no longer used
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Remove visible ad blocks before approval**

For public HTML pages, remove blocks like this:

```html
<div class="ad-container">
    <div class="container">
        <ins class="adsbygoogle"
             style="display:block"
             data-ad-client="ca-pub-1091058137620121"
             data-ad-slot="7890123456"
             data-ad-format="auto"
             data-full-width-responsive="true"></ins>
        <script>
             (adsbygoogle = window.adsbygoogle || []).push({});
        </script>
    </div>
</div>
```

Also remove empty ad containers like this:

```html
<div class="ad-container">
    <div class="container">
    </div>
</div>
```

- [ ] **Step 2: Decide whether to keep the global AdSense script**

Before approval, prefer removing page-level AdSense script tags from public HTML:

```html
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-1091058137620121" crossorigin="anonymous"></script>
```

Keep `ads.txt` and policy language so ownership and disclosure remain correct.

- [ ] **Step 3: Verify ad-shell markup is gone from public HTML**

Run:
```bash
rg -n "adsbygoogle|ad-container|data-ad-slot|Top Ad Banner|Ad Banner|pagead2.googlesyndication.com" "f:/me/ads/模版/aicoolgames.cool2" --glob "*.html" --glob "!**/.claude/**"
```
Expected: no matches in public HTML.

- [ ] **Step 4: Mark resolved report rows**

For each ad-shell row fixed in `docs/adsense-audit-report.md`, change `Open` to `Fixed`.

---

### Task 5: Fix P0 crawl, sitemap, and published-page consistency

**Files:**
- Modify: `sitemap.xml`
- Modify: `robots.txt`
- Modify: `ads.txt`
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Generate the exact public HTML page list**

Run:
```bash
python - <<'PY'
from pathlib import Path
root = Path('f:/me/ads/模版/aicoolgames.cool2')
for p in sorted(root.rglob('*.html')):
    if '.claude' in p.parts:
        continue
    print(p.relative_to(root).as_posix())
PY
```
Expected: a list containing root pages and all `blog/*.html` article pages.

- [ ] **Step 2: Update `sitemap.xml` to match the generated list**

Use URLs in this format:

```xml
<url>
  <loc>https://www.aicoolgames.cool/blog/budgeting-101.html</loc>
  <lastmod>2026-05-12</lastmod>
  <changefreq>monthly</changefreq>
  <priority>0.7</priority>
</url>
```

Priority guidance:
- `index.html` or `/`: `1.0`
- `blog.html`: `0.9`
- trust pages: `0.6`
- article pages: `0.7`

- [ ] **Step 3: Keep `robots.txt` simple**

Make sure `robots.txt` contains only crawl-friendly rules like:

```text
User-agent: *
Allow: /

Sitemap: https://www.aicoolgames.cool/sitemap.xml
```

Do not block `/blog/`, CSS, or root HTML pages.

- [ ] **Step 4: Keep `ads.txt` minimal and accurate**

Verify `ads.txt` contains the publisher line only, for example:

```text
google.com, pub-1091058137620121, DIRECT, f08c47fec0942fa0
```

- [ ] **Step 5: Verify sitemap URLs map to real files**

Run:
```bash
python - <<'PY'
from pathlib import Path
import xml.etree.ElementTree as ET
root = Path('f:/me/ads/模版/aicoolgames.cool2')
ns = {'sm': 'http://www.sitemaps.org/schemas/sitemap/0.9'}
tree = ET.parse(root / 'sitemap.xml')
missing = []
for loc in tree.findall('.//sm:loc', ns):
    url = loc.text.strip()
    path = url.replace('https://www.aicoolgames.cool/', '')
    if path in ('', '/'):
        file = root / 'index.html'
    else:
        file = root / path
    if not file.exists():
        missing.append(url)
for url in missing:
    print(url)
print(f'MISSING_SITEMAP_URLS={len(missing)}')
PY
```
Expected: `MISSING_SITEMAP_URLS=0`

---

### Task 6: Fix P1 trust and compliance page quality

**Files:**
- Modify: `about.html`
- Modify: `contact.html`
- Modify: `privacy-policy.html`
- Modify: `terms-of-service.html`
- Modify: `affiliate-disclosure.html`
- Modify: `faq.html`
- Modify: `resources.html`
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Make About credible without inflated credentials**

`about.html` should clearly say:

```text
MoneyMind is written by Jake Miller, a personal finance writer sharing practical lessons from budgeting, debt payoff, saving, and beginner investing.
```

Avoid claims of professional certification unless the page already has verifiable evidence.

- [ ] **Step 2: Make Contact useful and specific**

`contact.html` should include clear reasons to contact:

```text
- corrections or outdated information
- questions about an article
- privacy or policy questions
- affiliate disclosure questions
```

Use the existing email address if present; do not invent a new one.

- [ ] **Step 3: Ensure Privacy covers review-relevant topics**

`privacy-policy.html` must mention:

```text
cookies, Google Analytics, Google AdSense, third-party advertising partners, affiliate links, email contact handling, policy updates
```

- [ ] **Step 4: Ensure Terms include finance disclaimer**

`terms-of-service.html` must clearly say content is educational and not individualized financial, tax, investment, or legal advice.

- [ ] **Step 5: Ensure Affiliate Disclosure separates editorial content from monetization**

`affiliate-disclosure.html` must clearly say affiliate links may earn commissions and that recommendations should be evaluated by the reader.

- [ ] **Step 6: Make FAQ and Resources non-empty and useful**

`faq.html` and `resources.html` should contain practical, non-duplicative material that supports the site theme. Remove repeated marketing copy and avoid listing tools without context.

- [ ] **Step 7: Verify trust pages have required terms and no old brand**

Run:
```bash
rg -n "MoneyMind|Jake Miller|cookies|Google Analytics|Google AdSense|affiliate|educational|not financial advice|corrections|AI Cool Finance|expert advice|team" about.html contact.html privacy-policy.html terms-of-service.html affiliate-disclosure.html faq.html resources.html
```
Expected: required trust terms are present, and old brand/fake authority terms are absent.

---

### Task 7: Fix P1 homepage and blog hub review quality

**Files:**
- Modify: `index.html`
- Modify: `blog.html`
- Modify: `styles.css` only if layout cleanup is necessary
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Make homepage copy restrained and author-led**

Replace unsupported claims such as reader counts, guaranteed outcomes, or hype with plain author positioning:

```text
MoneyMind is a practical personal finance site by Jake Miller, focused on budgeting, debt payoff, saving, and beginner investing for people who want clearer money decisions without jargon.
```

- [ ] **Step 2: Make homepage sections serve clear roles**

Keep only sections that answer one of these questions:

```text
Who writes this site?
What topics does it cover?
Which articles should a new reader start with?
How can a reader contact or evaluate the site?
```

Remove sections that only repeat marketing claims.

- [ ] **Step 3: Make blog page topic-led**

`blog.html` should group articles by meaningful sections such as:

```text
Debt Recovery
Budgeting Basics
Saving & Safety Net
Beginner Investing
Life & Money
```

Each section should have a short human-written description and article links.

- [ ] **Step 4: De-emphasize the AdSense article**

If `blog/google-adsense-guide.html` remains public, do not feature it on the homepage or primary blog hub. It makes the site look monetization-first.

- [ ] **Step 5: Verify homepage and blog do not look like a content farm index**

Run:
```bash
rg -n "12K\+|12,000|comprehensive library|expert advice|transform your finances|guaranteed|AdSense|adsbygoogle|AI Cool Finance" index.html blog.html
```
Expected: no matches except unavoidable references in non-prominent contexts.

---

### Task 8: Fix P1 article metadata and high-risk generated-copy patterns

**Files:**
- Modify: `blog/*.html`
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Normalize article author metadata**

For every `blog/*.html` page:
- `<meta name="author">` must be `Jake Miller`.
- Header and footer must use MoneyMind.
- Structured data author, if present, must use `Jake Miller`.

- [ ] **Step 2: Remove high-risk generated phrases**

For article copy, replace common AI-like phrases with plain wording:

```text
"ultimate guide" -> "guide"
"comprehensive guide" -> "practical guide"
"transform your finances" -> "make better money decisions"
"in today's fast-paced world" -> remove the phrase and start with the actual topic
"unlock the power" -> use a direct verb such as "use" or "build"
```

- [ ] **Step 3: Add at least one contextual internal link to high-value article pages that lack them**

Use existing article URLs only. Example link pattern:

```html
<a href="emergency-fund.html">emergency fund</a>
<a href="budgeting-101.html">first budget</a>
<a href="debt-snowball-vs-avalanche.html">debt payoff method</a>
<a href="investing-101.html">beginner investing plan</a>
```

- [ ] **Step 4: Verify article high-risk phrases are reduced**

Run:
```bash
rg -n "AI Cool Finance|AICoolFinance|expert advice|ultimate guide|comprehensive guide|in today's fast-paced world|unlock the power|revolutionize|transform your finances|adsbygoogle|ad-container" "f:/me/ads/模版/aicoolgames.cool2/blog" --glob "*.html"
```
Expected: no old brand, no ad-shell markup, and only a small number of phrase matches if the phrase is contextually justified.

---

### Task 9: Final full-site validation and audit report closeout

**Files:**
- Modify: `docs/adsense-audit-report.md`

- [ ] **Step 1: Run the final consistency scan**

Run:
```bash
rg -n "AI Cool Finance|AICoolFinance|12K\+|12,000|CFP|CFA|team of experts|our experts|expert advice|ad-container|adsbygoogle|data-ad-slot|placeholder|TODO|TBD|lorem" "f:/me/ads/模版/aicoolgames.cool2" --glob "*.html" --glob "!**/.claude/**"
```
Expected: no public HTML matches.

- [ ] **Step 2: Run the final broken-link scan**

Run:
```bash
python - <<'PY'
from pathlib import Path
import re
root = Path('f:/me/ads/模版/aicoolgames.cool2')
files = [p for p in root.rglob('*.html') if '.claude' not in p.parts]
missing = []
for p in files:
    text = p.read_text(encoding='utf-8', errors='ignore')
    for href in re.findall(r'href="([^"]+)"', text):
        if href.startswith(('http://','https://','mailto:','#','javascript:')):
            continue
        clean = href.split('#')[0].split('?')[0]
        if not clean:
            continue
        target = (p.parent / clean).resolve()
        if not target.exists():
            missing.append((p.relative_to(root).as_posix(), href))
for page, href in missing:
    print(f'{page} -> {href}')
print(f'MISSING_LINKS={len(missing)}')
PY
```
Expected: `MISSING_LINKS=0`

- [ ] **Step 3: Run the final sitemap validation**

Run:
```bash
python - <<'PY'
from pathlib import Path
import xml.etree.ElementTree as ET
root = Path('f:/me/ads/模版/aicoolgames.cool2')
ns = {'sm': 'http://www.sitemaps.org/schemas/sitemap/0.9'}
tree = ET.parse(root / 'sitemap.xml')
missing = []
for loc in tree.findall('.//sm:loc', ns):
    url = loc.text.strip()
    path = url.replace('https://www.aicoolgames.cool/', '')
    file = root / 'index.html' if path in ('', '/') else root / path
    if not file.exists():
        missing.append(url)
for url in missing:
    print(url)
print(f'MISSING_SITEMAP_URLS={len(missing)}')
PY
```
Expected: `MISSING_SITEMAP_URLS=0`

- [ ] **Step 4: Close the report**

Update `docs/adsense-audit-report.md`:

```markdown
## Final Readiness Notes

- P0 open items: none found after final scan
- P1 open items: list any remaining article-depth improvements that were intentionally deferred
- P2 deferred items: SEO polish, visual rhythm, deeper article rewrites if needed
```

Do not claim Google AdSense approval is guaranteed.

---

## Self-review checklist before implementation starts

- [x] Every requirement from `docs/superpowers/specs/2026-05-12-adsense-audit-design.md` maps to at least one task.
- [x] The plan starts with a full-site audit before fixes.
- [x] P0, P1, and P2 are explicitly represented.
- [x] No new framework, CMS, or build system is introduced.
- [x] The plan avoids fake credentials and unsupported trust claims.
- [x] The plan does not guarantee AdSense approval.
