---
name: academic-dashboard
description: "Render research dashboards and data views in a clean, restrained, journal/preprint visual language — light warm-paper background, serif display type, muted palette, ruled data tables, and a LOCKED color encoding for Scite Smart Citations (supporting / contrasting / mentioning). Use this skill whenever building any HTML dashboard, report, or data visualization from Scite / research literature data — especially anything involving citations, citation classifications, papers, clinical trials, patents, or grants. Trigger on requests like 'build a dashboard', 'visualize these citations', 'make a view of supporting vs contrasting', 'turn this into a dashboard', or any research data display — even if the word 'dashboard' isn't used. The goal is output that reads as a credible research artifact, not a SaaS analytics app or marketing collateral. Always use this skill so multiple dashboards built across a session look like siblings."
---

# Academic Dashboard

Render research data as a clean, journal-style HTML dashboard. Output is a single self-contained `.html` file.

The aesthetic is deliberate: this should look like a working paper or a preprint's figures page — **neutral, credible, restrained** — not like a SaaS analytics product. No gradients, no glow, no full-bleed dark chrome, no oversized metric tiles, no emoji. White space and a single reading column do the work.

## How to use this skill

1. **Read `references/template.html` first.** It is the canonical source for every color token, font, and component class. Copy tokens and component markup directly — do not reconstruct them from memory or invent new colors. The template includes a worked masthead, key-figures row, a stacked Smart Citations chart, a ruled data table, and a colophon. Populate that skeleton.
2. Save the result to `/mnt/user-data/outputs/[slug].html` and deliver it.
3. Keep everything in one file. Chart.js (from CDN) is the only allowed external dependency, and only when a chart is genuinely needed.

## The one rule that never bends: Smart Citations encoding

Every Scite citation classification uses the **same** three colors and labels in **every** dashboard, every time. This consistency is the point — it's how the audience learns to read the trust signal at a glance, and it's why two dashboards built minutes apart look like one product.

| Classification | Token | Color | Meaning |
|---|---|---|---|
| **Supporting** | `--supporting` | muted forest green `#2E7D5B` | the citing work's evidence backs the claim |
| **Contrasting** | `--contrasting` | muted clay red `#B0472B` | the citing work's evidence disputes the claim |
| **Mentioning** | `--mentioning` | warm gray `#7A756A` | cited without stated support or dispute |

Never recolor these, never reorder the legend, never substitute a brighter "alert red." Clay-not-fire-engine is intentional: contrasting evidence is a finding, not an error. Use the `.chip`, `.sc-dot`, and `.fig-val` classes from the template; use the soft `*-soft` fills for chip backgrounds and chart fills.

Include the `.sc-legend` once, near the top of the first view that shows classifications.

## What every dashboard includes

- **Masthead** — eyebrow, serif title that names the *analysis* (not the tool), one-line subtitle, and a mono byline that states the exact query/finding/condition analyzed, the date, and n. Naming the query on the page makes it reproducible and screenshot-credible.
- **Key figures** — the ruled `.figures` row. Lead with the total, then supporting / contrasting / mentioning in their locked colors. Keep it to ≤5 figures.
- **The body** — chart sections and/or `table.data` sections. Most research views are a timeline (stacked bar, by type) plus a table of the actual citing works. Prefer a real table of named papers over an abstract chart — seeing the citing works is what makes it trustworthy.
- **Colophon** — always close with the provenance line: source (Scite Smart Citations via Scite MCP), dataset, retrieval date, a note that classifications are Scite's, and "Built with Claude Code."

## Charts

Use the Chart.js config in the template as the default: **stacked bar, series colored from the locked tokens, muted gridlines, mono ticks, no built-in legend** (the `.sc-legend` covers it). Avoid line/area charts with fills — they read as marketing. One chart per section, max. If the data is small (under ~8 rows), skip the chart and use a table; a clean table beats a sparse chart.

## Voice in the copy

Section notes and subtitles are plain and declarative — written for a mixed room of librarians, lab leads, and developers. One sentence on how to read each view. No hype verbs, no "unlock/supercharge/transform," no exclamation marks. Let the data carry it.

## Output

Save as `/mnt/user-data/outputs/[slug].html` and deliver the file. Keep it self-contained so it can be opened directly or hosted as-is.
