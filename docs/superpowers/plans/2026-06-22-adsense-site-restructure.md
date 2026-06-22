# AdSense Site Restructure Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rework MoneyMind into a focused, actively maintained personal-finance site for AdSense review.

**Architecture:** Keep the static HTML architecture and existing CSS. Replace public entry pages with curated topic paths, add a handful of recent practical articles, and update sitemap links without touching `ads.txt`.

**Tech Stack:** Static HTML, existing `styles.css`, XML sitemap, Git.

---

### Task 1: Rebuild Public Entry Pages

**Files:**
- Modify: `index.html`
- Modify: `blog.html`
- Modify: `about.html`
- Modify: `contact.html`

- [ ] Replace the homepage hero with a modest explanation of the site, four reader paths, recent updates, and trust links.
- [ ] Replace the blog index with five topic clusters and remove hype-like calls to action.
- [ ] Refresh author/about language around one small-site author and correction process.
- [ ] Make contact copy clear that email is the reliable path for corrections and feedback.

### Task 2: Add Recent Practical Content

**Files:**
- Create: `blog/weekly-money-review-routine.html`
- Create: `blog/checking-account-buffer.html`
- Create: `blog/when-to-pause-debt-payoff.html`

- [ ] Add three new human-sounding guides with dated metadata, concrete examples, and internal links.
- [ ] Keep advice educational and avoid professional-advice claims.

### Task 3: Update Discovery and Verify

**Files:**
- Modify: `sitemap.xml`

- [ ] Add new public article URLs to `sitemap.xml` with `2026-06-22` lastmod.
- [ ] Verify no `ads.txt` changes.
- [ ] Run a local link check for missing internal HTML targets.
