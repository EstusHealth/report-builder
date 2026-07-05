# OT Driving Assessment Report Builder

A single-page, client-side tool for drafting Estus Health occupational therapy driving assessment reports.

The entire app lives in `public/index.html` (HTML/CSS/vanilla JS, no build step, no backend — all data stays in the browser).

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
