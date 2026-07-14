# OT Driving Assessment Report Builder

A single-page, client-side tool for drafting Estus Health occupational therapy driving assessment reports.

The entire app lives in `public/index.html` (HTML/CSS/vanilla JS, no build step, no backend — all data stays in the browser).

## Features (v2.0)

- **Assessment library** — remove any standardised cognitive assessment you didn't administer, add more from the built-in library (Trail Making A & B, OT Drive Home Maze, DriveSafe DriveAware, Intersection Diagram, Bells, MoCA, MMSE, Clock Drawing, UFOV), or add fully **custom assessments** with your own scoring, interpretation and reference. Scores are auto-interpreted against driving thresholds and references are compiled automatically.
- **Auto-drafted clinical text** — reason for referral, screen interpretations, summary (including an outcome paragraph), recommendations (library + custom), declarations, and five letters (GP cover, MDI referral, NDIS support, family/supervising drivers, plain-language client letter), all pronoun-aware via `{name}`/`{he}`-style tokens and editable.
- **Live A4 preview** with per-document tabs (report package and each letter), zoom / fit-width, print-to-PDF of the active document, and Word export.
- **Guided completion** — per-section progress chips, a validation checklist grouped by section that jumps to the missing field, and export blocking until the report is complete.
- Drafts autosave to the browser; save/open per-client `.json` draft files (Ctrl/⌘+S).

## Local preview

Open `public/index.html` directly in a browser, or serve it locally:

```
npx serve public
```

## Deploying to Vercel

This repo is a static site with no build step. On [vercel.com](https://vercel.com):

1. Import this GitHub repository as a new Vercel project.
2. Framework preset: **Other** (no build command needed).
3. Output directory: `public`.
4. Deploy.

Or via the Vercel CLI from the repo root:

```
npx vercel
```
