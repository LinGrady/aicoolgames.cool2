# Content Quality Refresh Design

## Goal

Refresh the three static sites with honest, useful, theme-matched content updates that improve reader value and site credibility without changing `ads.txt` or inventing false operating signals.

## Scope

- `aicoolgames.cool2`: personal finance content under MoneyMind.
- `aicoolgames.com2`: practical technology buying and product decision content.
- `game520game2`: software architecture and engineering practice content.

## Approach

Add one fresh, evergreen article to each site, link it from the relevant article index or homepage, and update sitemaps only when needed so new pages are discoverable. Where existing homepage copy makes inflated or unverifiable claims, replace it with calmer, transparent language.

## Guardrails

- Do not edit `ads.txt`.
- Do not create fake awards, fake traffic, fake teams, or fake publication history.
- Avoid time-sensitive factual claims unless they are framed as practical guidance rather than news.
- Keep changes within the three requested folders.

## Verification

Check Git diffs for forbidden files, verify every new article link exists, confirm the static HTML parses well enough for browser rendering, and commit/push each repository separately.
