# Silverpush SEO Agent

## What this is

A single-file (`index.html`) SEO command centre built specifically for **silverpush.co**. It runs entirely in the browser — no backend, no build step, no dependencies beyond Google Fonts and the Anthropic API. State is persisted in `localStorage`.

The tool was purpose-built to track, execute, and automate an SEO improvement roadmap for Silverpush (an AI-powered contextual video advertising company). It doubles as a lightweight project management tool for the SEO sprint.

---

## Navigation / Panels

The app has nine tabs rendered as `<section class="panel">` elements toggled by the `go()` JS function:

| Tab | Panel ID | Purpose |
|---|---|---|
| Dashboard | `p-dashboard` | KPI summary, sprint progress, high-priority task list |
| Action Plan | `p-tasks` | Full SEO task backlog across 4 sprints, filterable by sprint/status/category |
| Crawl | `p-crawl` | Launch simulated site crawls, live log output, progress bar |
| GEO | `p-geo` | Generative Engine Optimisation plan (AI citation readiness) |
| Schedule | `p-schedule` | Monthly audit scheduling, Zapier automation instructions, 2026 crawl calendar |
| Competition | `p-compete` | Competitor crawl and head-to-head SEO metrics comparison |
| Analytics | `p-analytics` | Google Analytics 4 + Search Console integration |
| Keywords | `p-keywords` | 25 ranked keyword opportunities for silverpush.co |
| Reports | `p-reports` | Generated audit report cards |

---

## Data model

Tasks (the `SEED` array, ~37 items) are the core data type. Each task has:

```js
{ id, s (sprint 1-4), p (priority HIGH/MED/LOW), t (description), o (owner), e (effort), st (status: todo/inprogress/done/scheduled), c (category) }
```

Tasks are loaded from `localStorage` key `sp2_t` on boot, falling back to the hardcoded `SEED`. Status changes are immediately saved back to `localStorage`.

Categories: `technical`, `onpage`, `content`, `performance`, `monitoring`, `schema`, `geo`

---

## Sprint structure

| Sprint | Focus | Timeframe |
|---|---|---|
| 1 | Critical fixes — H1s, title/meta length, deleted blog restores, 15 MB GIF | Week 1 |
| 2 | On-page metadata — 22 over-length titles, 18 over-length descriptions, H1 keyword improvements | Weeks 2–3 |
| 3 | Technical, schema & performance — structured data, alt text, page speed, sitemap | Weeks 4–6 |
| 4 | Content strategy & GEO — AI citation optimisation, pillar pages, competitor comparison pages | Month 2+ |

---

## AI integration

- **Anthropic Claude** (`claude-sonnet-4-6`) is called in the Competition Analysis tab (`fetchAIInsight()`) to generate SEO insight summaries per competitor.
- API key is stored in `localStorage` via the Settings modal (⚙️ button in header).
- Analytics tab calls **Google Analytics 4 Data API** and **Google Search Console API** directly from the browser using user-supplied API keys.

---

## Crawl modules

Eight simulated crawl modes selectable in the Crawl tab:

| Module | What it checks |
|---|---|
| Full SEO Audit | All 11 data categories |
| 404 & Redirect Check | Response codes, 301/404 patterns |
| On-Page Elements | Titles, meta descriptions, H1/H2 |
| Page Size Audit | Page weights, response times, text ratios |
| Internal Links Audit | Inlinks, outlinks, orphan pages |
| Schema & Canonicals | Canonical tags, schema signals |
| GEO Readiness Scan | FAQ schema, speakable, definition blocks |
| Competitor Benchmark | Crawl and compare competitor SEO metrics |

Crawl output streams to a terminal-style log (`#clog`). Progress is shown with a strip progress bar.

---

## GEO (Generative Engine Optimisation)

The GEO tab covers getting silverpush.co cited in ChatGPT, Perplexity, Gemini, Grok, Claude, and Bing Copilot. Six optimisation modules are tracked (AI Search Readiness, Speakable/FAQ Schema, Definition Blocks, Statistics & Data Citations, Entity Optimisation, E-E-A-T Signals). Each AI engine has a tailored strategy card.

---

## Theming

The file contains two layered CSS themes in `<style>` tags:
1. A base indigo/blue theme
2. An override `adtech-theme` layer (`#adtech-theme`) — deep navy header (`#080F22`→`#162D60`), ad-tech brand colours, subtle grid background. This is the active visual theme.

Fonts: Bricolage Grotesque (headings), Inter/Lato (body), JetBrains Mono (monospace/labels).

---

## Key hardcoded context

- **Target site:** `https://silverpush.co`
- **Pre-configured competitors:** channelfactory.com, gumgum.com, pixability.com
- **Scheduled cadence:** Monthly full audit on the 1st of each month
- **Company context:** Silverpush makes contextual video advertising AI (products: Mirrors, Parallels, Crafters). Post-Vidgyor acquisition, CTV is a key content growth area.
