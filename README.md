# OT Driving Assessment Report Builder

A single-page, client-side tool for drafting Estus Health occupational therapy driving assessment reports.

The entire app lives in `public/index.html` (HTML/CSS/vanilla JS, no build step, no backend — all data stays in the browser).

## What this tool is for

Version 2 was rebuilt around the Flinders University advanced competencies feedback. The core principle:

> **The report is written from the record. Not the other way round.**

Most of what follows exists to make that structurally true rather than merely intended. The general design rule is that **the builder never pre-fills a clinical finding**. Anything that looks like a finding has to be entered by the person who observed it.

### The governance layer

**Section 0 — Set-up & contemporaneous record**

- **Equipment check.** A grouped pre-assessment checklist covering the client file, vision screen, physical screen, the full cognitive battery and the on-road set-up. Every item is marked Ready or N/A-with-a-reason, then timestamped. Export is blocked until set-up is confirmed.
- **Field notes dock.** A capture panel available from any section (bottom-right button, or `⌘/Ctrl + ↵` to log). Each note is timestamped and tagged to a phase (pre-drive / on-road / debrief) and to a specific screen or on-road performance item.
- **Locking.** The record can be locked only once it meets minimum coverage: 6 pre-drive notes, 10 on-road notes, and at least one note against every one of the five on-road performance areas. After locking, notes cannot be edited or deleted — only timestamped addenda can be added, and anything added post-lock is marked as such in the report.
- **Provenance.** Who recorded the on-road notes and when, plus a declared AI-use position (none / language editing after drafting from notes / dictation of your own spoken notes). This prints in the report as a **Basis of Record** section stating note counts, lock time and the AI position.

### Traceability

- On-road checklist items start as **not yet rated**. Nothing is pre-ticked as safe.
- Any item rated as an **issue** must be linked to at least one field note logged at the time. The linked notes appear as timestamped chips under the item, and export is blocked while a flagged issue has nothing behind it.
- Items marked **not assessed** require a reason, which prints in the report rather than being silently dropped.

### Test administration integrity

Every standardised test carries an **administration record**: administered per manual, sample item completed, prompting/cueing given, environment free of distraction.

Each test also carries an expandable **administration script** setting out what you must do, what you may say, and what you must never say — written for the tests that go wrong most easily (Trail Making Test B, Drive Home Maze, Bells, DriveSafe, DriveAware, Intersection Diagram).

If answers, targets or route guidance were provided, or standard administration was departed from, the test is marked **not scoreable**. The score is then:

- excluded from the report's results table, which prints the reason instead of a number;
- excluded from the DriveSafe DriveAware combined outcome category;
- excluded from the auto-drafted summary, which states plainly that the result was not relied upon;
- blocked from export until you record what happened and what you are doing about it.

### Physical assessment

Manual muscle testing on the MRC (Oxford) 0–5 scale across twelve groups relevant to vehicle control, each annotated with why it matters for driving. Every group starts as **not tested**; a group left untested needs a documented reason, and the report states explicitly which groups were not tested and that no conclusion is drawn about them. An in-app reference card covers the grading scale, break-test technique and the grade-4-vs-5 error.

The other physical screens start blank. Standard "within normal limits" wording is available on demand per row, rather than being the default.

### Clinical interview

Sixteen occupational profile domains (thirteen core), each with prompt questions to ask. Core domains need at least 15 words or an explicit not-applicable with a reason. Covers roles, routine, work/study, community participation, transport reliance, goals, fatigue, medication timing, substance use, insight, supports for practice, learning style, incident history, sensory factors and communication needs.

### Report-writing quality gate

Two tiers, both enforced before export:

**Blockers** — must be fixed. Set-up and record gates, required fields, core profile domains, untested muscle groups without reasons, incomplete administration records, unrated on-road items, unlinked issues, unconfirmed summaries, unresolved `{tokens}` and `[placeholders]`, `[TBC]` in the licence expiry, outcome/finding contradictions (e.g. "fit to drive, no restrictions" alongside flagged issues; a vision standard recorded as not met alongside a supportive outcome), missing recommendations, missing consent, and the documentation competency standards.

**Advisories** — each must be individually ticked as considered. Contractions, unsupported phrasing ("seemed fine", "no issues", "I think", "obviously"), sentences over 45 words, missing terminal punctuation, thin sections by word count, short on-road duration, flagged issues that do not appear in the summary, and unedited template blocks.

### Sign-off

A single confirmation in Section 8: that you have read the report end to end against your field notes and every finding, interpretation and recommendation is traceable to something you recorded at the time. It is a hard blocker.

### Auto-draft discipline

Auto-drafted text is a skeleton, not a report. The summary, cognitive summary and physical summary each carry a confirmation bar — you tick that the text reflects your notes. The tick stores a hash of the text, so **editing afterwards silently un-ticks it** and you confirm again. An untouched auto-draft summary is a hard blocker.

### Competency coverage

All 50 standards from the *Australian Competency Standards for Occupational Therapy Driver Assessors* (Fields, Unsworth & Harreveld, 2018), mapped to the report. Most are evidenced automatically from what you entered; the rest are confirmed manually; ones that do not apply to the outcome are marked N/A. The four documentation standards (4.1, 4.2, 4.4, 4.5) are hard blockers.

Fields exist for the competencies that previously had nowhere to be recorded: suitability screening, prior assessments, communication screen, MDI briefing, safety management during the drive, off-road and on-road feedback to the client, licensing/insurance information given, licence conditions considered, and report turnaround.

## Local preview

Open `public/index.html` directly in a browser, or serve it locally:

```
npx serve public
```

Click **Load example** for a fully worked de-identified sample — 34 field notes, complete profile, muscle grades, administration records and linked on-road findings — which exports cleanly and shows what the finished discipline looks like.

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
