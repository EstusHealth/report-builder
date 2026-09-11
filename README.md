# OT Driving Assessment Report Builder

A single-page, client-side tool for drafting occupational therapy driving assessment reports. Free and open source under the [MIT licence](LICENSE) — fork it, rebrand it, adapt it to your own practice. It ships set up for Estus Health; [swapping in your own logo, colours and letterhead](#making-it-your-own) takes a couple of minutes and no code.

The entire app lives in `public/index.html` (HTML/CSS/vanilla JS, no build step, no backend, no dependencies).

**Nothing leaves the browser.** There is no server, no analytics and no network call except the Google Fonts stylesheet. Client data, drafts, your practice profile and your logo all live in `localStorage` on the machine you are using. Drafts move between machines as files you save yourself. That also means clearing site data deletes your drafts, so keep file copies of anything you need.

> ⚠️ This tool encodes **Australian** practice: Austroads *Assessing Fitness to Drive*, AHPRA registration, state driver licensing authorities, and the Australian competency standards for OT driver assessors. The test cut-offs and licensing wording will not be correct in other jurisdictions without review. It supports clinical documentation — it does not make clinical decisions, and the assessor remains responsible for every word that goes out.

## What this tool is for

It was rebuilt around a set of supervisor feedback on a driver assessment course. The core principle:

> **The report is written from what you observed. Not the other way round.**

The builder does not hold your assessment notes — keep those however you normally do. What it does is refuse to invent the parts only you can supply. The general design rule is that **the builder never sets a clinical judgement for you**. Nothing starts as normal, nothing is pre-ticked as safe, and every status is one the assessor sets. Where a status *has* been set, the builder will write the standard wording for it in one click so you are editing a sentence rather than typing one — but the judgement behind it is always yours, and a quick fill never touches a row you have already rated.

## The four stages

The form follows the four phases of the assessment itself rather than presenting one long document. Only the stage you are in is on screen, and each tab carries its own outstanding-item count, so you can see what a phase still owes you before you leave it.

| Stage | Sections | What it covers |
| --- | --- | --- |
| **1 · Initial Interview** | ⚙, 0–3 | Practice profile, room set-up, client and referral details, reports reviewed, and the clinical interview and occupational profile |
| **2 · Off-Road Assessment** | 4 | Hearing and communication, vision, physical, and the standardised cognitive battery — each with a how-to-conduct card |
| **3 · On-Road Assessment** | 5 | Vehicle, conditions, route, MDI briefing, safety management and the performance checklist |
| **4 · Feedback & Finalising** | 6–9 | Summary and clinical reasoning, recommendations, feedback given to the client, declarations, sign-off and competency coverage |

Within a stage, **one section is open at a time** — opening a section closes its siblings, so a stage is one form rather than a long scroll. Section numbers are unchanged, so the validation panel's `§` references still point where they always did — and clicking an outstanding item switches to the right stage, opens the section it lives in, and jumps to the field. The stage you were last on is remembered.

### The governance layer

**Section 0 — Set-up**

- **Equipment check.** A grouped pre-assessment checklist covering the client file, vision screen, physical screen, the full cognitive battery and the on-road set-up. Every item is marked Ready or N/A-with-a-reason, then timestamped. It is strongly recommended rather than enforced — an unconfirmed set-up is raised for review, not treated as a blocker.
- **Additional documents.** Tick the documents you want alongside the main report; they are described [below](#additional-documents).

The builder does not hold your assessment notes. Record observations however you normally do — paper, a notes app, whatever travels with you into the car — and write the report from them.

### Clinical reasoning

The value of a driver assessment is not the list of findings but the relationship between them. The builder models that relationship rather than leaving it to prose.

- **Convergence analysis.** Each cognitive domain is mapped to the on-road behaviours it typically shows up in — divided attention to scanning, mirror routines, blind-spot checks and gap selection; planning to route and manoeuvre set-up; insight to self-monitoring; lateralised inattention to detection on the affected side. The summary is then built from the *relationship* between the two halves: which off-road findings were corroborated on road, which were not evident (and what that implies), and which on-road behaviours had no off-road correlate and are therefore skill rather than capacity.
- **Severity.** Flagged issues are rated developmental, significant or critical. Severity orders the summary and the instructor handover, drives the suggested instruction hours, and blocks a supportive outcome sitting under a critical finding.
- **Suggested hours** are derived from the number and severity of findings and whether an underlying capacity difficulty was corroborated, not typed from habit. Departing from the suggestion is fine; a large gap raises an advisory asking the report to justify the figure.
- **Score interpretation reports the pattern, not just pass/fail.** Trail Making B distinguishes accurate-but-slow from fast-but-inaccurate, since these mean different things and have different remedies. The Bells Test takes omissions by side and distinguishes lateralised neglect from a general search deficit. DriveSafe is banded rather than binary.
- **Normative comparison.** Driving thresholds are cut-offs, not age norms. Each test carries a field for how the raw score compared with the manual's age-stratified data, which is reported alongside the threshold — distinguishing a result that is abnormal for this person from one that is normal for their age but still below the driving cut-off. The client's age at assessment is computed and shown.
- **Cross-checks.** A DSDA category that is hard to reconcile with the entered scores raises an advisory, on the assumption it is a transcription error — the DSDA report itself remains authoritative.

### Traceability

- On-road checklist items start as **not yet rated**. Nothing is pre-ticked as safe. Once you *have* rated one safe, a click writes the standard description of that item so a clean drive reads as a positive finding rather than an empty cell — per item, or for every safe item at once. The report falls back to the same wording for any safe item you leave blank, and prints a short paragraph per performance area naming what was safe. Items rated as an issue or not assessed are never auto-worded.
- Any item rated as an **issue** must carry a comment describing what you saw, and export is blocked while a flagged issue has nothing written against it.
- Items marked **not assessed** require a reason, which prints in the report rather than being silently dropped.

### How to conduct each assessment

Stage 2 is built to be worked from at the bench, not just recorded into afterwards. Every screen carries an expandable card covering technique, and each is written around the error that most often invalidates that particular screen.

**Vision.** A **record an unremarkable vision screen** button sets fields, ocular motility and the Austroads standard to their normal findings and inserts the standard wording, leaving the acuity figures to you. Then a lead card on what the three vision screens each measure — and what none of them measure (contrast sensitivity, glare recovery, useful field of view), so the limits of the screen are explicit. Then one card per test, each with a diagram:

- **Visual acuity** — chart set-up and the measured test distance, the R / L / binocular order, reading down to the smallest line with no more than one error, and what 6/12 means. The binocular figures are required, since they carry the Austroads comparison; the monocular ones are raised for review rather than blocking, so a screen you took binocularly does not hold up the report. No acuity figure is ever filled in for you — it has to be read off the chart. Carries the Austroads private-vehicle threshold and the common errors (pacing the distance, testing in reading glasses, recording "within normal limits" with no figure).
- **Visual fields by confrontation** — seating, testing each eye against your own field, the four quadrants, finger counting, the binocular pass, and double simultaneous stimulation for extinction. States plainly what confrontation cannot do, when to refer for formal perimetry, and what each pattern of field loss looks like on road.
- **Ocular motility** — the H pattern for pursuit, two-target saccades, convergence and diplopia, with the reasoning for why saccadic accuracy predicts the mirror and blind-spot checks you will be rating in Stage 3.

**Physical.** Sixteen screens in the order you would run them — set the seat first, because fit determines what every later measurement means, then upper limb, lower limb, trunk and mobility. Each carries a **how to screen this one** card with the procedure, what to record, and the error that most often makes the result meaningless. See [Physical screens](#physical-screens) below.

Then each of the twelve muscle groups has a **how to test this one** card: client position, what to stabilise, the words to say, where the resistance goes and in which direction, the substitution to watch for, and a link to the technique reference. Each carries a schematic showing the stabilised segment, the moving segment at its test position, the direction of the movement asked for, and the point of resistance.

**Hearing and communication** has its own card, since it comes first and everything after it depends on instructions landing.

### Test administration integrity

Every standardised test carries an **administration record**: administered per manual, sample item completed, prompting/cueing given, environment free of distraction.

Each test also carries two expandable cards. **How to conduct this test** covers what the test measures, what you need, roughly how long it takes, and the procedure step by step — including the process observations that are only capturable while the client is doing it. **What you may and may not say** sets out what you must do, what you may say, and what you must never say. Both are written for the tests that go wrong most easily (Trail Making Test B, Drive Home Maze, Bells, DriveSafe, DriveAware, Intersection Diagram), and both defer to the manual where they differ from it.

If answers, targets or route guidance were provided, or standard administration was departed from, the test is marked **not scoreable**. The score is then:

- excluded from the report's results table, which prints the reason instead of a number;
- excluded from the DriveSafe DriveAware combined outcome category;
- excluded from the auto-drafted summary, which states plainly that the result was not relied upon;
- blocked from export until you record what happened and what you are doing about it.

### Physical screens

Sixteen screens covering what the driving task actually demands of the body, grouped and ordered the way you would run them:

| Group | Screens |
| --- | --- |
| **Vehicle fit & access** | Seating position and fit to the vehicle; entry, exit and seatbelt |
| **Upper limb** | Active range of movement; functional grasp, release and sustained grip; coordination and dexterity; sensation and proprioception |
| **Lower limb** | Active range of movement; pedal transfer speed and accuracy; coordination and pedal modulation; sensation and proprioception |
| **Trunk, neck & mobility** | Cervical and trunk rotation for observation checks; sitting balance, posture and seated tolerance; functional mobility and Rapid Pace Walk; pain and its effect on the driving task |
| **Other factors** | Tone, tremor and involuntary movement; aids, orthoses, prostheses and existing modifications |

Every screen behaves like the rest of the builder rather than like a free-text box:

- **A status you have to set** — within functional limits / limitation identified / not tested / N/A. Nothing defaults to normal. A limitation must be described, and **not tested needs a reason**, which prints in the report. A blank is a blocker, because a reader cannot tell a clear screen from a skipped one. Where a run of screens was unremarkable, a **mark remaining WFL** button on each group heading (and one for the whole section) sets every screen you have not yet rated and inserts its standard wording for you to edit. It is scoped to blank rows only and never overwrites a status you have set.
- **Measurements where the screen produces one**, entered as figures: sternum-to-wheel clearance, accelerator-to-brake transfer time, cervical rotation in degrees each side, sitting tolerance in minutes, Rapid Pace Walk in seconds.
- **The figures are interpreted, not just stored.** Under 25 cm of wheel clearance raises the airbag problem and points at pedal extensions; under about 30° of cervical rotation raises wide-angle mirrors as a modification recommendation; a Rapid Pace Walk over 9 seconds is reported as the risk marker it is and explicitly not as a licensing test; a sitting tolerance shorter than the on-road drive is cross-checked against the duration you entered in Section 5 and flagged.
- **A how-to-screen card per row**: numbered procedure, what to record, and the error that most often makes that particular result meaningless — testing fit anywhere but the vehicle, prompting the seatbelt, accepting a head turn the trunk produced, timing a stroll, recording a pain score with no function attached.

The report prints a grouped table of what was screened with the measurements first, then states explicitly which screens were not performed and that nothing is concluded from their absence. Standard "within functional limits" wording is inserted on demand — per row or per group — rather than being the default.

### Manual muscle testing

On the MRC (Oxford) 0–5 scale across twelve groups relevant to vehicle control, each annotated with why it matters for driving and each with its own how-to card and diagram (above). Every group starts as **not tested**; a group left untested needs a documented reason, and the report states explicitly which groups were not tested and that no conclusion is drawn about them.

Where a section graded normally throughout, a **remaining → 5/5** button on each section heading (and one for the whole grid) marks the groups you have not touched yet as tested at grade 5. It is scoped to untouched groups only — a group you have already graded, or marked not tested with a reason, or marked N/A, is never changed. Comments are left empty, since the report's summary already states that power was 5/5 throughout the groups tested. An in-app reference card covers the grading scale, break-test technique and the grade-4-vs-5 error.

### Clinical interview

Sixteen occupational profile domains (thirteen core), each with prompt questions to ask. Core domains need at least 15 words or an explicit not-applicable with a reason. Covers roles, routine, work/study, community participation, transport reliance, goals, fatigue, medication timing, substance use, insight, supports for practice, learning style, incident history, sensory factors and communication needs.

### Report-writing quality gate

Two tiers, both enforced before export:

**Blockers** — must be fixed. Required client, referral and assessor fields, core profile domains, unrecorded physical screens, undescribed limitations, untested screens and muscle groups without reasons, incomplete administration records, unrated on-road items, flagged issues with no comment, unconfirmed summaries, unresolved `{tokens}` and `[placeholders]`, `[TBC]` in the licence expiry, outcome/finding contradictions (e.g. "fit to drive, no restrictions" alongside flagged issues; a vision standard recorded as not met alongside a supportive outcome), missing recommendations, missing consent, an enabled additional document missing something essential, and the documentation competency standards.

**Advisories** — each must be individually ticked as considered. The set-up layer (an unconfirmed equipment check, an empty practice name), monocular visual acuity, contractions, unsupported phrasing ("seemed fine", "no issues", "I think", "obviously"), sentences over 45 words, missing terminal punctuation, thin sections by word count, short on-road duration, flagged issues that do not appear in the summary, and unedited template blocks.

The set-up gates sit in the second tier deliberately: they are good discipline and the panel keeps asking about them, but not being able to issue a finished report is the wrong price for having skipped one.

### Additional documents

Tick any of these in **Section 0** and they appear as tabs above the preview, each exporting to Word separately. All four are generated from the same assessment data as the main report, so they cannot drift from it or contradict each other — and each carries an optional free-text paragraph for anything specific to that reader.

| Document | Written for | Contains |
| --- | --- | --- |
| **Letter to GP / treating practitioner** | The treating doctor | One-page clinical summary: outcome, findings bearing on medical fitness to drive, medication, and an explicit list of what you are asking them to do |
| **NDIS support recommendations** | Planner, support coordinator, plan manager | Participant goals the assessment relates to, current functional impact, what was assessed, and each recommended support with a reasonable-and-necessary rationale and expected outcome |
| **Handover to driving instructor** | The MDI | Licence status, priority focus areas drawn from the flagged on-road issues, strengths to build on, how the client learns, safety notes, and what to report back and when |
| **Summary for client, family or support person** | The client and whoever supervises their practice | Plain-language account of what was done, the outcome, what went well, what needs practice, how to help, and next steps |

Only what belongs in each document goes into it — the NDIS participant number, for instance, appears on the NDIS document and nowhere else. Enabling a document that is missing something essential (a GP name, an NDIS number) blocks export until it is supplied.

### Sign-off

A single confirmation in Section 8: that you have read the report end to end and every finding, interpretation and recommendation in it is supported by what you observed and recorded during the assessment. It is a hard blocker.

### Auto-draft discipline

Auto-drafted text is a skeleton, not a report. The summary, cognitive summary and physical summary each carry a confirmation bar — you tick that the text reflects what you observed. The tick stores a hash of the text, so **editing afterwards silently un-ticks it** and you confirm again. An untouched auto-draft summary is a hard blocker.

### Competency coverage

All 50 standards from the *Australian Competency Standards for Occupational Therapy Driver Assessors* (Fields, Unsworth & Harreveld, 2018), mapped to the report. Most are evidenced automatically from what you entered; the rest are confirmed manually; ones that do not apply to the outcome are marked N/A. The four documentation standards (4.1, 4.2, 4.4, 4.5) are hard blockers.

Fields exist for the competencies that previously had nowhere to be recorded: suitability screening, prior assessments, communication screen, MDI briefing, safety management during the drive, off-road and on-road feedback to the client, licensing/insurance information given, licence conditions considered, and report turnaround.

## On a tablet

The same page adapts — there is no separate mobile build to keep in sync. On any touch device up to desktop width (an iPad in either orientation, but not a 1280px laptop), the layout switches to **data entry first**:

- The four stage tabs stay pinned to the top of the form, sized for a thumb. On a phone they collapse to short labels so all four still fit across.
- The draft report is **hidden by default** and the form takes the full width. Tap **Report** in the toolbar to read it full-screen, and **✕ Close report** to get back. The choice is remembered, so it also works as a focus mode on desktop.
- While the report is hidden it is not re-rendered on every keystroke — it is marked stale and rebuilt when you open it, print or export, which keeps typing responsive.
- Controls are sized for fingers: 46px inputs, 42px buttons, 22px checkboxes, full-width rating selects on the on-road checklist. Inputs use 16px text so iOS does not zoom on focus.
- Secondary actions (load example, new, save/open draft, export, print) collapse into a **⋯** menu so the toolbar stays one row.
- Safe-area insets are respected on notched devices, and the page can be added to the home screen to run without browser chrome.

## Making it your own

The app ships configured with the Estus Health letterhead and colours, so it works out of the box. Rebranding is entirely optional and takes a couple of minutes — no code required.

Open the **⚙ Practice Profile & Branding** section at the top of the app. Everything there is set once, saved in your browser, and reused for every report — it is not part of any individual draft.

- **Logo** — upload a PNG, JPG or SVG (under 400 KB). It replaces the text wordmark on the letterhead and is embedded directly into the report, so exported files stay self-contained and work offline. Word handles PNG and JPG most reliably; if an SVG renders oddly in an exported `.doc`, use a PNG. A transparent PNG around 600px wide works well.
- **Wordmark & tagline** — used when no logo is set. The two name fields are styled differently (bold, then letter-spaced) so a two-word name reads as a wordmark; put the whole name in the first field if you prefer.
- **Letterhead contact details** — email, phone, website. Blank fields are omitted from the report entirely.
- **Brand colours** — four pickers driving the letterhead rule, section headings, sub-headings and table headers, in both the report and the app itself.
- **Default assessor details** — name, role, AHPRA number and usual location, pre-filled into each new report and overridable per report.

The report reference prefix is derived from your practice initials automatically.

**Export profile** writes the whole thing to a JSON file, so you can move it to another machine or hand it to colleagues in the same practice rather than having everyone set it up by hand. **Import profile** reads it back.

The profile overrides the shipped defaults per browser. If you are maintaining a fork and want to change what it ships with, edit the `BRAND_DEF` block near the top of the script — that is the only branded thing in the source.

## Adapting the clinical content

The data that drives the assessment lives in plain arrays at the top of the script, so most changes need no knowledge of the rest of the code:

| Constant | What it controls |
| --- | --- |
| `EQUIP` | Pre-assessment equipment and set-up checklist |
| `PROFILE_DOMAINS` | Occupational profile domains and their prompt questions |
| `MUSCLES` / `MRC` | Muscle groups tested, their how-to-test text and diagram geometry, and the grading scale |
| `PHYS_ROWS` / `PHYS_ST` | Physical screens — how-to-screen text, measurement fields, threshold interpretation and standard wording; and the status vocabulary |
| `CHECKLIST` | On-road performance areas and items |
| `TEST_META` / `ADMIN_SCRIPTS` | Standardised tests, and the procedure and administration rules shown for each |
| `STAGES` | The four assessment stages and which sections belong to each |
| `interp*()` | Score thresholds and interpretation wording |
| `REC_DEFS` | Recommendation library |
| `COMPETENCIES` | Competency standards and how each is evidenced |
| `BAD_PHRASES` / `CONTRACTIONS` | Writing-quality checks |
| `REFS` | Reference list |

If you adapt the thresholds for another jurisdiction, please check them against that jurisdiction's fitness-to-drive standard rather than trusting the defaults here.

## Contributing

Issues and pull requests are welcome. It is a single static file with no build step — edit `public/index.html`, open it in a browser, and click **Load example** to exercise a fully populated report. Please keep it dependency-free and buildless.

## Licence

MIT — see [LICENSE](LICENSE). Use it commercially, fork it, rebrand it. It comes with no warranty, and it is your professional responsibility to check that its outputs are accurate and appropriate for your clients and jurisdiction.

## Local preview

Open `public/index.html` directly in a browser, or serve it locally:

```
npx serve public
```

Click **Load example** for a fully worked de-identified sample — complete profile, muscle grades, administration records and rated on-road findings — which exports cleanly and shows what the finished discipline looks like. The sample client is fictional.

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
