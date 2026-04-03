# GrowthX System — Agent Handoff

> **Last updated:** 2026-04-02
> **Purpose:** Everything a new agent needs to pick up exactly where the last one left off.

---

## What This Project Is

A free, gated lead magnet called **"The GrowthX System"** — 7 learning modules that teach the mental models, frameworks, and first principles behind how GrowthX approaches AI-led growth. The same thinking that drives results for Webflow, Ramp, Lovable, and 60+ other companies paying $10K–$60K/month.

**Live site:** Deployed via GitHub Pages from the `gh-pages` branch of `williamproctor/growthx-system`.

---

## Repository Structure

This is a **separate git repo** nested inside the `Will-s-Workspace` repo at `docs/growthx/`. The parent workspace does NOT track it. All commits happen here.

```
docs/growthx/                  ← repo root (williamproctor/growthx-system.git)
├── index.html                 ← Project hub (internal dashboard)
├── shared.css                 ← Design system (colors, typography, components)
├── theme.js                   ← Light/dark mode toggle
├── mermaid-init.js            ← Mermaid diagram renderer
├── assets/
│   ├── favicon.svg            ← GrowthX "X" mark, centered
│   ├── growthx-logo-dark.svg  ← Dark-background logo
│   ├── og-image.png           ← Social share card
│   └── og-image.html          ← OG image generator
├── system/index.html          ← Landing page (gated, email capture form)
├── inventory/index.html       ← Content inventory + clip map (dark theme)
├── assessments/index.html     ← 39-question interactive self-assessment quiz
└── modules/
    ├── index.html             ← Module overview grid
    ├── 01.html – 07.html      ← Individual module pages with interleaved video + text
```

## Deploy Workflow

```bash
cd docs/growthx
git add -A && git commit -m "message"
git push origin main
git checkout gh-pages && git merge main --ff-only && git push origin gh-pages && git checkout main
```

Always push to both `main` and `gh-pages`. GitHub Pages serves from `gh-pages`.

---

## Navigation

Every page has a global nav bar with the same 5 links:
- **Hub** → `index.html`
- **Landing Page** → `system/index.html`
- **Modules** → `modules/index.html`
- **Inventory** → `inventory/index.html`
- **Self-Assessments** → `assessments/index.html`

Paths use `../` prefix when pages are in subdirectories. The dark/light theme toggle and (on the landing page only) a "Get the System →" CTA button follow the nav links.

---

## Landing Page (`system/index.html`)

**Fully gated.** Every clickable element on the page (module cards, CTAs, bottom CTA) links to `#form`, which is a 6-field email capture form (name, work email, company, role, company size, biggest challenge). The nav links are the only way to navigate to real pages — everything else gates.

### Key sections (top to bottom):
1. **Hero** — "The system 60+ companies pay $10K–$60K/month for. *Yours, free.*" (yellow highlight)
2. **Logo ticker** — 11 SVG logos (Ramp, Webflow, Lovable, Augment Code, Reddit, Superhuman, Deepgram, SentinelOne, Exec, Abnormal Security, Lovable alt) from `growthx-landing-prototype` repo. Infinite scroll animation.
3. **"Why This Exists"** — Two-column split: "Without a system" (problem) vs "What this system teaches" (solution). Gold accent border on the system side.
4. **"What's Inside"** — 8 module cards (01–07 + Self-Assessments), all link to `#form`.
5. **Results** — 60+ companies, $14M run-rate, 24x traffic at Deepgram, 500+ paid $300 live.
6. **Testimonials** — Cecilia Stallsmith (Lovable), Mike Bosserman (Exec).
7. **"Who It's For"** — Qualification checklist + dark background section.
8. **Form** — The gate. 6 fields, JS validation (blocks free email providers), success state.
9. **Final CTA** — "Value first" messaging + link back to `#form`.

### Removed companies from logo ticker:
- HashiCorp, Scale AI, Service Titan (not clients — those were Marcel's past employers)
- Deepgram IS a client, was kept

---

## Video Infrastructure

28 clips hosted on **Cloudflare R2 CDN** (free, no egress fees):
```
https://pub-0ecfe34e9a4a41dfa8a92bb569890cbe.r2.dev/module-XX/NN-slug.mp4
```

Pattern: `module-01/` through `module-07/`, clips numbered `01-`, `02-`, etc.

The **inventory clip map** has play buttons (▶) on every row that open an inline modal video player (dark overlay, close with X/Escape/click-outside).

---

## Design System

`shared.css` defines all variables. Key tokens:
- `--accent-gold: #C49A3C` (gold accent, CTAs)
- `--background` / `--foreground` swap on `data-theme="dark"`
- `--font-mono: 'JetBrains Mono'`
- `--radius: 8px`, `--radius-pill: 100px`
- `.site-nav` is the shared sticky nav
- `.site-footer` is the shared footer

The landing page has additional scoped `<style>` for its unique sections (ticker, shift columns, module cards, stats, form, etc.).

The inventory page uses `data-theme="dark"` on `<html>`.

---

## Content Stats

| Category | Count |
|---|---|
| Video clips in modules | 28 (~149 min) |
| Words of written content | ~6,200 |
| Module learning time | ~3 hrs |
| Full YouTube workshops | 4 (~6 hrs 15 min) |
| Self-assessment questions | 39 |
| Assessment time | ~1 hr 15 min |
| **Total potential learning time** | **~10.5 hours** |

---

## What Was Done in This Session (2026-04-02, afternoon)

1. **SVG logo ticker** — Replaced text-only company names with real SVG brand logos from `growthx-landing-prototype` repo. Removed HashiCorp, Scale AI, Service Titan.
2. **Global nav standardization** — All 12 pages now have identical nav: Hub, Landing Page, Modules, Inventory, Self-Assessments.
3. **Landing page gating** — All module cards and CTAs link to `#form`. Nav links remain navigable.
4. **"Yours, free." yellow highlight** — `#E4C02A` on the H1 span.
5. **Results stats updated** — $13M → $14M, 250+ → 500+.
6. **Clip map video player** — Added ▶ play buttons to all 28 clips with a modal overlay player.
7. **Expanded totals section** — Three-part breakdown (modules, workshops, assessments) + gold "Total potential learning time" card (~10.5 hrs).
8. **Redesigned "The Shift" section** — From confusing Before/Now/With the Right Thinking three-card layout to a clean two-column problem/solution split.

---

## Known Remaining Work

- **Module 01 gap** — Marcel still needs to record the dedicated 15-min system overview. Script is written.
- **CRM integration** — Form currently logs to console. Needs HubSpot/webhook connection.
- **Marcel's Notion prompt doc** — Referenced in workshops but not in the Content Vault. Needed for Module 06.
- **Content Vault stubs** — Quality Benchmarks from ALG Vault still gated (intake only).

---

## Important Files Outside This Repo

- **TEAM-MEMORY.md** (workspace root) — Shared knowledge base. Read before every session. Append learnings at end.
- **Content Vault/** (workspace root) — Obsidian vault with 105+ markdown notes, transcripts, and video files. Obsidian MCP can search it.
- **growthx-landing-prototype/** (`~/Documents/GitHub/`) — Source repo for SVG logos and the original landing page design. Separate repo, not nested.
- **memory/ideas.md** (workspace root) — Background ideas captured during sessions.

---

## How to Use This File

Tell your Claude agent:

> Read `docs/growthx/HANDOFF.md` — it has the full state of the GrowthX System project. Then read `TEAM-MEMORY.md` for broader workspace context. Pick up where the last session left off.

That's it. The agent will know the file structure, deploy workflow, design system, what's been done, and what's left.
