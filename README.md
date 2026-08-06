# OT Driving Assessment Report Builder

A single-page, client-side tool for drafting Estus Health occupational therapy driving assessment reports.

The entire app lives in `public/index.html` (HTML/CSS/vanilla JS, no build step, no backend — all data stays in the browser).

## Interview mode

**Interview mode** drives you through the assessment one question at a time, the way a supervisor would ask them. The question set branches on the purpose of the assessment (learner driver, fitness to drive, return to driving, licence conditions, vehicle modifications) and covers the whole report — intake and referral, background history, the pre on-road screen, a post-drive debrief that walks the on-road checklist group by group, and the outcome reasoning behind your recommendations.

Each question shows why it is being asked, follow-up probes to use if the answer is thin, and the report field it feeds. You can type the answer straight into the question card and it lands in the right field, with the live report preview updating as you go.

**Recording and transcription happen in a third-party tool** — Google Meet, Heidi, or whatever you already use. This app never accesses the microphone and makes no network requests of any kind. Afterwards, paste the transcript or the processed note into section 0; inside interview mode you can show it beside each question with the relevant words highlighted, so you can lift each answer into the right field.

Use **Copy script** or **Print script** to take the question list into the session with you.

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
