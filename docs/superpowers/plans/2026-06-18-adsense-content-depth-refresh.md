# Adsense Content Depth Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add 15 useful evergreen articles across three static sites and repair old content patterns that can trigger AdSense low-value or replicated-content concerns.

**Architecture:** Each site remains static HTML. New articles are standalone pages using the existing local layout, then linked from the relevant index/category page and sitemap. Existing pages are repaired by removing empty links, exaggerated claims, duplicate boilerplate, and thin article recommendations.

**Tech Stack:** Static HTML, CSS, XML sitemaps, Git.

---

### Task 1: MoneyMind Content Refresh

**Files:**
- Create 5 pages in `F:\me\ads\模版\aicoolgames.cool2\blog\`
- Modify `F:\me\ads\模版\aicoolgames.cool2\blog.html`
- Modify `F:\me\ads\模版\aicoolgames.cool2\sitemap.xml`
- Repair selected older MoneyMind pages that contain overpromising or thin related sections.

- [ ] Add articles about irregular expenses, grocery budget resets, debt fatigue, shared money meetings, and beginner investing mistakes.
- [ ] Link all new articles from relevant topic hubs.
- [ ] Add all new URLs to the sitemap.

### Task 2: Practical Tech Guide Content Refresh

**Files:**
- Create 5 pages in `F:\me\ads\模版\aicoolgames.com2\`
- Modify `F:\me\ads\模版\aicoolgames.com2\categories.html`
- Modify `F:\me\ads\模版\aicoolgames.com2\index.html`
- Modify `F:\me\ads\模版\aicoolgames.com2\sitemap.xml`
- Repair old tech articles that read like generic launch/news copy.

- [ ] Add articles about home office monitors, password manager evaluation, used phone buying, AI note-taking tools, and router upgrades.
- [ ] Link all new articles from category lists and homepage.
- [ ] Add all new URLs to the sitemap.

### Task 3: Game520 Engineering Content Refresh

**Files:**
- Create 5 pages in `F:\me\ads\模版\game520game2\articles\`
- Modify `F:\me\ads\模版\game520game2\blog.html`
- Modify `F:\me\ads\模版\game520game2\index.html`
- Modify `F:\me\ads\模版\game520game2\sitemap.xml`
- Repair existing pages that contain generic, repeated, or inflated claims.

- [ ] Add articles about incident communication, dependency review, feature flags, data migration readiness, and AI observability.
- [ ] Link all new articles from the correct topic clusters.
- [ ] Add all new URLs to the sitemap.
- [ ] Remove remaining empty links and unverifiable claims from the homepage and article templates.

### Task 4: Verification and Publishing

- [ ] Confirm `ads.txt` is unchanged in all three repositories.
- [ ] Run local static link checks across all three sites.
- [ ] Confirm no `.claude` worktree files are staged.
- [ ] Commit and push each repository via SSH.
