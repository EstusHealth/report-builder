# OT Driving Assessment Report Builder

A single-page, client-side tool for drafting occupational therapy driving assessment reports. Free and open source under the [MIT licence](LICENSE) — fork it, rebrand it, adapt it to your own practice. It ships set up for Estus Health; [swapping in your own logo, colours and letterhead](#making-it-your-own) takes a couple of minutes and no code.

The entire app lives in `public/index.html` (HTML/CSS/vanilla JS, no build step, no backend, no dependencies).

**Nothing leaves the browser.** There is no server, no analytics and no network call except the Google Fonts stylesheet. Client data, drafts, your practice profile and your logo all live in `localStorage` on the machine you are using. Drafts move between machines as files you save yourself. That also means clearing site data deletes your drafts, so keep file copies of anything you need.

> ⚠️ This tool encodes **Australian** practice: Austroads *Assessing Fitness to Drive*, AHPRA registration, state driver licensing authorities, and the Australian competency standards for OT driver assessors. The test cut-offs and licensing wording will not be correct in other jurisdictions without review. It supports clinical documentation — it does not make clinical decisions, and the assessor remains responsible for every word that goes out.

## What this tool is for

It is built to the depth of a real driver assessment report, measured against the Flinders Medical Centre driver assessment proformas and the record forms from the Australian OT driver assessment course. The core principle:

> **The report is written from what you observed. Not the other way round.**

The builder does not hold your assessment notes — keep those however you normally do. What it does is refuse to invent the parts only you can supply. The general design rule is that **the builder never sets a clinical judgement for you**. Nothing starts as normal, nothing is pre-ticked as safe, and every status is one the assessor sets. Where a status *has* been set, the builder will write the standard wording for it in one click so you are editing a sentence rather than typing one — but the judgement behind it is always yours, and a quick fill never touches a row you have already rated.

## The four stages

The form follows the four phases of the assessment itself rather than presenting one long document. Only the stage you are in is on screen, and each tab carries its own outstanding-item count, so you can see what a phase still owes you before you leave it.

| Stage | Sections | What it covers |
| --- | --- | --- |
| **1 · Initial Interview** | ⚙, 1–3 | Practice profile, client and referral details, reports reviewed, and the clinical interview and occupational profile |
| **2 · Off-Road Assessment** | 4 | Hearing and communication, vision, physical, the standardised cognitive battery and the pre-drive outcome summary — each screen with a how-to-conduct card |
| **3 · On-Road Assessment** | 5 | Vehicle, conditions, route, MDI briefing, safety management and the performance checklist |
| **4 · Feedback & Finalising** | 6–9 | Summary and reasoning, recommendations, additional documents, feedback given to the client, declarations, sign-off and competency coverage |

Within a stage, **one section is open at a time** — opening a section closes its siblings, so a stage is one form rather than a long scroll. The validation panel's `§` references point at section numbers, and clicking an outstanding item switches to the right stage, opens the section it lives in, and jumps to the field. The stage you were last on is remembered.

### The pre-drive outcome summary

The value of a driver assessment is not the list of findings but the relationship between them. That relationship is recorded explicitly, in the three-column table the course record form uses, across five categories — visual, physical, cognitive, psychosocial and driving history:

| Issue | Possible impact on road | Considerations for the on-road assessment |
| --- | --- | --- |

It is filled in **before the drive**, so it does what it is for: it tells you what to look for and what to set up on the route. Afterwards it is the spine of the Section 6 summary, which is drafted from it — what the screen anticipated, what actually happened on road, and which of the two the reader should weigh. It prints at the end of the pre-drive section of the report.

The builder does not hold your assessment notes. Record observations however you normally do — paper, a notes app, whatever travels with you into the car — and write the report from them.

### Scores are interpreted, not just stored

- **Score interpretation reports the pattern, not just pass/fail.** Trail Making B distinguishes accurate-but-slow from fast-but-inaccurate, since these mean different things and have different remedies. The Bells Test takes omissions by side and distinguishes lateralised neglect from a general search deficit. DriveSafe is banded rather than binary.
- **Physical measurements carry their thresholds.** Under 25 cm of wheel clearance raises the airbag problem and points at pedal extensions; under about 30° of cervical rotation raises wide-angle mirrors as a modification recommendation; a heel pivot slower than 15 taps in 9 seconds is reported against that standard; a Rapid Pace Walk over 9 seconds is reported as the risk marker it is and explicitly not as a licensing test; a sitting tolerance shorter than the on-road drive is cross-checked against the duration in Section 5 and flagged.
- **What you did not do is reported.** Untested lines, untested muscle groups and unassessed on-road items print with their reasons, and the report states that nothing is concluded from their absence.

### Traceability

- On-road checklist items start as **not yet rated**. Nothing is pre-ticked as safe. Rate what you saw first; then one click marks the items still sitting unrated as safe and appropriate and inserts each one's standard description, so a clean drive reads as a positive finding rather than an empty cell. The report falls back to the same wording for any safe item you leave blank, and prints a short paragraph per performance area naming what was safe. Items rated as an issue or not assessed are never touched by it.
- Any item rated as an **issue** must carry a comment describing what you saw, and export is blocked while a flagged issue has nothing written against it.
- Items marked **not assessed** require a reason, which prints in the report rather than being silently dropped.

### How to conduct each assessment

Stage 2 is built to be worked from at the bench, not just recorded into afterwards. Every screen carries an expandable card covering technique, and each is written around the error that most often invalidates that particular screen.

**Vision.** A **record an unremarkable vision screen** button sets fields, ocular motility and the Austroads standard to their normal findings and inserts the standard wording, leaving the acuity figures to you. Then a lead card on what the three vision screens each measure — and what none of them measure (contrast sensitivity, glare recovery, useful field of view), so the limits of the screen are explicit. Then one card per test, each with a diagram:

- **Visual acuity** — chart set-up and the measured test distance, the R / L / binocular order, reading down to the smallest line with no more than one error, and what 6/12 means. The binocular figures are required, since they carry the Austroads comparison; the monocular ones are raised for review rather than blocking, so a screen you took binocularly does not hold up the report. No acuity figure is ever filled in for you — it has to be read off the chart. Carries the Austroads private-vehicle threshold and the common errors (pacing the distance, testing in reading glasses, recording "within normal limits" with no figure).
- **Visual fields by confrontation** — seating, testing each eye against your own field, the four quadrants, finger counting, the binocular pass, and double simultaneous stimulation for extinction. States plainly what confrontation cannot do, when to refer for formal perimetry, and what each pattern of field loss looks like on road.
- **Ocular motility** — the H pattern for pursuit, two-target saccades, convergence and diplopia, with the reasoning for why saccadic accuracy predicts the mirror and blind-spot checks you will be rating in Stage 3.

**Physical.** Thirteen lines in the order the Flinders proforma reports them. Each carries a **how to screen this one** card with the procedure, what to record, and the error that most often makes the result meaningless. See [Physical screens](#physical-screens) below.

Then each of the twelve muscle groups has a **how to test this one** card: client position, what to stabilise, the words to say, where the resistance goes and in which direction, the substitution to watch for, and a link to the technique reference. Each carries a schematic showing the stabilised segment, the moving segment at its test position, the direction of the movement asked for, and the point of resistance.

**Hearing and communication** has its own card, since it comes first and everything after it depends on instructions landing.

### Test administration integrity

The default battery is six tests — Trail Making B, OT Drive Home Maze, DriveSafe, DriveAware, the Intersection Diagram Test and the Bells Test. Eight more are there, unticked, for when the referral question calls for them: Trail Making A, Clock Drawing (Freund scoring, 4/7 cut-off), the Snellgrove Maze, the Road Law Slide Test, the Written Road Law Test, the MoCA, Addenbrooke's, and the 128-point paper DriveSafe. Each carries its own threshold from the course record form.

Each test carries two expandable cards. **How to conduct this test** covers what the test measures, what you need, roughly how long it takes, and the procedure step by step — including the process observations that are only capturable while the client is doing it. **What you may and may not say** sets out what you must do, what you may say, and what you must never say. Both are written for the tests that go wrong most easily (Trail Making Test B, Drive Home Maze, Bells, DriveSafe, DriveAware, Intersection Diagram), and both defer to the manual where they differ from it.

One tick per test records that **standard administration was departed from**. The test is then marked **not scoreable**, and the score is:

- excluded from the report's results table, which prints the reason instead of a number;
- excluded from the DriveSafe DriveAware combined outcome category;
- excluded from the auto-drafted summary, which states plainly that the result was not relied upon;
- blocked from export until you record what happened and what you are doing about it.

### Physical screens

Thirteen lines, in the order and the wording the Flinders proforma reports them — a status you select, a comment where there is something to say, and a measurement where the line produces one:

| Line | Measurement it carries |
| --- | --- |
| Range of movement | Cervical rotation, degrees each side |
| Strength (Oxford scale) | — (the MRC grid below) |
| Muscle tone | Modified Ashworth grade |
| Coordination — upper limb | — |
| **Coordination — lower limb** | **Heel pivot test** (taps and seconds), foot taps per 10 s, simulated accelerator/brake sequence |
| Speed of movement | Accelerator-to-brake transfer, seconds |
| Sensation & proprioception | — |
| Sitting balance & posture | Sitting tolerated, minutes |
| Mobility, transfers & Rapid Pace Walk | Rapid Pace Walk seconds, walking aid |
| Fine manipulation | — |
| Endurance | — |
| Pain | VAS 0–10 |
| Vehicle fit, aids & modifications | Sternum to wheel centre, cm |

Plus hand dominance. The status vocabulary is the proforma's: *no issues reported or observed* · *mild* · *moderate* · *significant difficulty* · *not tested* · *N/A*. Nothing defaults to normal, a difficulty must be described, and **not tested** and **N/A** need reasons, which print in the report. A blank is a blocker, because a reader cannot tell a clear screen from a skipped one — but where a run of lines was unremarkable, one button sets everything you have not recorded yet and inserts each one's standard wording for you to edit. It is scoped to blank lines and never overwrites a status you have set.

Each line carries a **how to screen this one** card: numbered procedure, what to record, and the error that most often makes that particular result meaningless — testing fit anywhere but the vehicle, prompting the seatbelt, accepting a head turn the trunk produced, timing a stroll, letting the whole leg lift instead of pivoting at the heel, recording a pain score with no function attached.

The report prints the thirteen lines with their measurements first, then states explicitly which were not tested and that nothing is concluded from their absence.

### Manual muscle testing

On the MRC (Oxford) 0–5 scale across twelve groups relevant to vehicle control, each annotated with why it matters for driving and each with its own how-to card and diagram (above). This is what the **Strength** line points at. Every group starts as **not tested**, and the report states explicitly which groups were not tested and that no conclusion is drawn about them.

Where a section graded normally throughout, a **remaining → 5/5** button on each section heading (and one for the whole grid) marks the groups you have not touched yet as tested at grade 5. It is scoped to untouched groups only — a group you have already graded, or marked not tested with a reason, or marked N/A, is never changed. Comments are left empty, since the report's summary already states that power was 5/5 throughout the groups tested. An in-app reference card covers the grading scale, break-test technique and the grade-4-vs-5 error.

### Clinical interview

Eight occupational profile domains (six core), each with prompt questions to ask. Core domains need content, or an explicit not-applicable with a reason. Covers roles, work and study and social history; current transport and reliance on others; the purpose of driving and what the client expects from the assessment; insight into their own abilities and risk; fatigue, sleep, pain, medication timing and substance use; crashes, near-misses and infringements; and — where relevant — supports for supervised practice and learning style. Medical history, symptoms and driving history are recorded separately in Sections 1 and 3.

### Report-writing quality gate

Two tiers, both enforced before export:

**Blockers** — must be fixed. Identity, licensing, referral and assessor fields, `[TBC]` in the licence expiry, core profile domains, unrecorded physical lines, undescribed difficulties, untested lines without reasons, binocular visual acuity, test scores, unrated on-road items, flagged issues with no comment, the unconfirmed summary, unresolved `{tokens}` and `[placeholders]`, outcome/finding contradictions (e.g. "fit to drive, no restrictions" alongside flagged issues; a vision standard recorded as not met alongside a supportive outcome), missing recommendations, missing consent, sign-off, an enabled additional document missing something essential, and the documentation competency standards.

**Advisories** — each must be individually ticked as considered. The competency-prompt fields (communication screen, MDI briefing, safety management, feedback given, licensing information, suitability decisions), an empty practice name, monocular visual acuity, contractions, unsupported phrasing ("seemed fine", "no issues", "I think", "obviously"), sentences over 45 words, missing terminal punctuation, thin sections by word count, short on-road duration, flagged issues that do not appear in the summary, and unedited template blocks.

The competency prompts sit in the second tier deliberately: they are good discipline and the panel keeps asking about them, but not being able to issue a finished report is the wrong price for having skipped one. Standard wording still sitting verbatim as inserted is exempt from the phrasing checks — it is flagged as unedited, not as sloppy writing.

Using each one-click fill where it applies, a complete assessment reaches **ready to export** in roughly the number of decisions the Flinders proforma itself takes.

### Additional documents

Tick any of these in **Section 6** and they appear as tabs above the preview, each exporting to Word separately. All four are generated from the same assessment data as the main report, so they cannot drift from it or contradict each other — and each carries an optional free-text paragraph for anything specific to that reader.

| Document | Written for | Contains |
| --- | --- | --- |
| **Letter to GP / treating practitioner** | The treating doctor | One-page clinical summary: outcome, findings bearing on medical fitness to drive, medication, and an explicit list of what you are asking them to do |
| **NDIS support recommendations** | Planner, support coordinator, plan manager | Participant goals the assessment relates to, current functional impact, what was assessed, and each recommended support with a reasonable-and-necessary rationale and expected outcome |
| **Handover to driving instructor** | The MDI | Licence status, priority focus areas drawn from the flagged on-road issues, strengths to build on, how the client learns, safety notes, and what to report back and when |
| **Summary for client, family or support person** | The client and whoever supervises their practice | Plain-language account of what was done, the outcome, what went well, what needs practice, how to help, and next steps |

Only what belongs in each document goes into it — the NDIS participant number, for instance, appears on the NDIS document and nowhere else. Enabling a document that is missing something essential (a GP name, an NDIS number) blocks export until it is supplied.

### Sign-off

A single confirmation in Section 8: that you have read the report end to end and every finding, interpretation and recommendation in it is supported by what you observed and recorded during the assessment. It is a hard blocker. Section 8 also carries a declared position on AI or dictation use, which prints with the declaration when it is anything other than *None*.

### Auto-draft discipline

Auto-drafted text is a skeleton, not a report. The Section 6 summary carries a confirmation bar — you tick that the text reflects what you observed. The tick stores a hash of the text, so **editing afterwards silently un-ticks it** and you confirm again. An untouched auto-draft summary is a hard blocker.

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
| `PROFILE_DOMAINS` | Occupational profile domains and their prompt questions |
| `MUSCLES` / `MRC` | Muscle groups tested, their how-to-test text and diagram geometry, and the grading scale |
| `PHYS_ROWS` / `PHYS_ST` / `MAS` | Physical lines — how-to-screen text, measurement fields, threshold interpretation and standard wording; the status vocabulary; the Modified Ashworth scale |
| `CHECKLIST` | On-road performance areas, items and their standard wording |
| `PREDRIVE_CATS` | Categories in the pre-drive outcome summary |
| `TEST_META` / `ADMIN_SCRIPTS` | Standardised tests (including which are on by default), and the procedure and administration rules shown for each |
| `STAGES` | The four assessment stages and which sections belong to each |
| `interp*()` | Score thresholds and interpretation wording |
| `REC_DEFS` | Recommendation library |
| `COMPETENCIES` | Competency standards and how each is evidenced |
| `REQ_FIELDS` | Required fields — a fourth `'soft'` element makes one an advisory rather than a blocker |
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

Click **Load example** for a fully worked de-identified sample — complete profile, physical lines with their measurements, muscle grades, test scores, a pre-drive outcome summary and rated on-road findings — which exports cleanly and shows what a finished report looks like. The sample client is fictional.

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
