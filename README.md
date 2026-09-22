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
| **2 · Off-Road Assessment** | 4 | Hearing and communication, vision, the physical table, the standardised cognitive battery and the pre-drive outcome summary — each screen with a how-to-conduct card |
| **3 · On-Road Assessment** | 5 | The drive and the vehicle, the familiarisation phase, MDI briefing, the performance checklist and the intervention log |
| **4 · Feedback & Finalising** | 6–9 | Summary and reasoning, recommendations, additional documents, feedback given to the client, declarations, sign-off and competency coverage |

Within a stage, **one section is open at a time** — opening a section closes its siblings, so a stage is one form rather than a long scroll. The review panel's `§` references point at section numbers, and clicking an outstanding item switches to the right stage, opens the section it lives in, and jumps to the field. The stage you were last on is remembered.

### The pre-drive outcome summary

The value of a driver assessment is not the list of findings but the relationship between them. That relationship is recorded explicitly, in the three-column table the course record form uses, across five categories — visual, physical, cognitive, psychosocial and driving history:

| Issue | Possible impact on road | Considerations for the on-road assessment |
| --- | --- | --- |

It is filled in **before the drive**, so it does what it is for: it tells you what to look for and what to set up on the route. Afterwards it is the spine of the Section 6 summary, which is drafted from it — what the screen anticipated, what actually happened on road, and which of the two the reader should weigh. It prints at the end of the pre-drive section of the report.

The builder does not hold your assessment notes. Record observations however you normally do — paper, a notes app, whatever travels with you into the car — and write the report from them.

### Scores are interpreted, not just stored

- **Score interpretation reports the pattern, not just pass/fail.** Trail Making B distinguishes accurate-but-slow from fast-but-inaccurate, since these mean different things and have different remedies. The Bells Test takes omissions by side and distinguishes lateralised neglect from a general search deficit. DriveSafe is banded rather than binary.
- **Physical measurements carry their thresholds.** Under about 30° of cervical rotation raises wide-angle mirrors as a modification recommendation; a heel pivot slower than 15 taps in 9 seconds is reported against that standard; a Rapid Pace Walk over 9 seconds is reported as the risk marker it is and explicitly not as a licensing test; a sitting tolerance shorter than the on-road drive is cross-checked against the duration in Section 5 and flagged. The measurements sit behind each line's **measurements** disclosure, so the table stays a table.
- **Two scoring scales, the proforma's by default.** DriveSafe ships as the 128-point paper version (≤76 lower, 77–95 middle, above 95 upper) and DriveAware as the 26-point paper version, where a **higher score means poorer insight** (above 17 lower range, 15–17 mid, below 15 upper). The iPad versions — DriveSafe out of 84, DriveAware out of 17 scored the other way — are there unticked for practices that administer the DSDA on the tablet. The combined DSDA paragraph quotes whichever pair is enabled, with its own denominators.
- **What you did not do is reported.** Untested muscle groups and unassessed on-road items print with their reasons, and the report states that nothing is concluded from their absence.

### The on-road assessment

The performance areas, their items and their order are the proforma's — Observation, Planning and
Judgment, Vehicle Positioning, Speed Control, Physical Control — and the report prints them the way
the proforma does: one block per area, the item list with an **Appropriate and safe** column and an
**Issues observed** column, then a single **Further comments** paragraph. A safe item is confirmed
with a tick rather than left as an empty cell, and nothing restates in prose what the ticks already
say — what prints alongside them is only what you wrote.

- The drive itself is a **composed paragraph**, not a field table: how long, whose vehicle and how
  it was equipped, who was present and where the assessor observed from, the traffic conditions,
  the route from start to finish, the weather and any modifications. Anything left blank drops out
  of the sentence.
- A **familiarisation phase** can be marked off with its own duration and note, so errors that
  belong to an unfamiliar vehicle are recorded as such rather than explained away in a finding
  later.
- The **intervention log** records every prompt and intervention from the driving instructor,
  typed from the course record form's fail errors — collision, failed to stop, failed to give way,
  excessive speed, too slow, disobeyed a direction, stopped in a dangerous position — plus a verbal
  prompt and use of the dual controls. A verbal prompt is a normal part of an assessed drive;
  anything beyond it is raised in the checks under an outcome that supports driving, and it is
  named in the GP letter and the instructor handover.

### Who else was there

Two optional toggles in Section 1, either or both, for an assessment attended by a third person.
Each takes a name, their role and qualification, and what they actually did.

- A **student** — observed the assessment, administered parts of the off-road screen under your
  supervision, or came along for the drive. Their presence needs the client's agreement, and the
  tick confirming it is the one gate here: a report naming a student cannot be exported without it.
- A **clinical supervisor** (OT Driving Assessor) — observed for competency sign-off, co-assessed,
  reviewed the report, or a combination.

Whoever is recorded is named in the administration paragraph, in the consent statement where a
student was present, in your scope-of-practice statement where you were supervised, and in the
on-road paragraph — but only where they were actually in the car, so a student who sat in on the
screen alone is not placed on the drive. Those sentences are composed from the toggles rather than
written into the editable wording, so ticking one after the text is drafted cannot leave the report
contradicting itself.

There is no supervised/final mode, no draft stamps and no countersignature — the toggles record who
was there and nothing more.

### Traceability

- On-road checklist items start as **not yet rated**. Nothing is pre-ticked as safe. Rate what you
  saw first; then one click marks the items still sitting unrated as safe and appropriate and
  inserts each one's standard description, so a clean drive reads as a positive finding rather than
  an empty tick box. Items rated as an issue or not assessed are never touched by it.
- Any item rated as an **issue** needs a comment describing what you saw; a flagged issue with
  nothing written against it is raised in the checks. Those comments are what the area's *Further
  comments* paragraph is built from, alongside an optional comment for the area as a whole.
- Items marked **not assessed** require a reason, which prints in the report rather than being
  silently dropped.

### How to conduct each assessment

Stage 2 is built to be worked from at the bench, not just recorded into afterwards. Every screen carries an expandable card covering technique, and each is written around the error that most often invalidates that particular screen.

**Vision.** A **record an unremarkable vision screen** button sets fields, ocular motility and the Austroads standard to their normal findings and inserts the standard wording, leaving the acuity figures to you. Then a lead card on what the three vision screens each measure — and what none of them measure (contrast sensitivity, glare recovery, useful field of view), so the limits of the screen are explicit. Then one card per test, each with a diagram:

- **Visual acuity** — chart set-up and the measured test distance, the R / L / binocular order, reading down to the smallest line with no more than one error, and what 6/12 means. Both are raised for review; the binocular figures carry the Austroads comparison, so those are the ones the report leans on. No acuity figure is ever filled in for you — it has to be read off the chart. Carries the Austroads private-vehicle threshold and the common errors (pacing the distance, testing in reading glasses, recording "within normal limits" with no figure).
- **Visual fields by confrontation** — seating, testing each eye against your own field, the four quadrants, finger counting, the binocular pass, and double simultaneous stimulation for extinction. States plainly what confrontation cannot do, when to refer for formal perimetry, and what each pattern of field loss looks like on road.
- **Ocular motility** — the H pattern for pursuit, two-target saccades, convergence and diplopia, with the reasoning for why saccadic accuracy predicts the mirror and blind-spot checks you will be rating in Stage 3.

**Physical.** Fourteen lines in the order the Flinders proforma reports them. Each carries a **how to screen this one** card with the procedure, what to record, and the error that most often makes the result meaningless. See [Physical screens](#physical-screens) below.

Then each of the twelve muscle groups has a **how to test this one** card: client position, what to stabilise, the words to say, where the resistance goes and in which direction, the substitution to watch for, and a link to the technique reference. Each carries a schematic showing the stabilised segment, the moving segment at its test position, the direction of the movement asked for, and the point of resistance. These live inside the optional grid — see [Manual muscle testing](#manual-muscle-testing).

**Standardised tests.** Each of the six main tests carries a **how to conduct this test** card: what it measures, what you need, roughly how long it takes, and the procedure step by step — including the process observations that are only capturable while the client is doing it.

**Hearing and communication** has its own card, since it comes first and everything after it depends on instructions landing.

### Standardised tests

The default battery is the proforma's six — the 128-point DriveSafe, the Intersection Diagram Test, the 26-point DriveAware, Trail Making B, the OT Drive Home Maze and the Bells Test. Nine more are there, unticked, for when the referral question calls for them: the Road Law Slide Test, the Written Road Law Test, Clock Drawing (Freund scoring, 4/7 cut-off), the Snellgrove Maze, Trail Making A, the iPad DriveSafe and DriveAware, the MoCA and Addenbrooke's. Each carries its own threshold.

Each test takes a score, and then the **named comment rows the proforma asks for** — DriveSafe has six (missed objects, detail of answer, speed of response, following instructions, logical and systematic responses, left/right discrimination), the Intersection Diagram Test five, the Road Law Slide Test four, and the rest one each with the threshold restated in the label. Every row carries its standard sentence, and one click fills the rows you have not written. Free text is equally valid — the label is the prompt, not a constraint. The filled sentences print under that test's interpretation in the report and appear in the JSON export as `qualitativeComments`.

The score itself is still interpreted against its threshold automatically, so the comment rows describe *how* the client worked while the interpretation reports *what* the score means.

### Physical screens

The Flinders proforma's table, row for row: one line per area, and **one sentence in each**. No status to set, no cell that means something different from the cell above it. Every line carries its standard wording — *"No issues reported, full range of movement observed."* — and the button at the top of the table writes it into every line you have not written yet, for you to edit. It never touches a line you have already written.

| Line | What it holds |
| --- | --- |
| Hand dominance | Right / Left / Ambidextrous |
| Active range of movement | Sentence · cervical rotation, degrees each side |
| Strength (Oxford Scale) | Sentence · points at the optional muscle grid |
| Tone (Modified Ashworth Scale) | Sentence · Modified Ashworth grade |
| Coordination | Sentence · **heel pivot test** (taps and seconds), foot taps per 10 s, simulated accelerator/brake sequence |
| Speed of movement | Sentence · accelerator-to-brake transfer, seconds |
| **Sensation** → upper limb · lower limb · proprioception · kinaesthesia | A sentence each, under one heading |
| Sitting balance / posture | Sentence · sitting tolerated, minutes |
| Mobility | Sentence · Rapid Pace Walk seconds, walking aid |
| Fine manipulation | Sentence |
| Pain | Sentence · VAS 0–10 |

Where a line produces a measurement it sits behind that line's **measurements** disclosure, closed by default, with its threshold interpretation underneath. The figure prints after the sentence in the report; it is not lost, it is just not in the way.

One piece of structure survives on top of the prose: a **difficulty** toggle per line. Flip it where the sentence describes a problem, and the physical summary can name the impaired areas, the report marks the cell, and the JSON export carries a machine-readable flag. It gates nothing.

Each line keeps its **how to screen this one** card: numbered procedure, what to record, and the error that most often makes that particular result meaningless — accepting a head turn the trunk produced, timing a stroll, letting the whole leg lift instead of pivoting at the heel, recording a pain score with no function attached.

A line with no sentence is raised in the checks, because a reader cannot tell a clear screen from a skipped one. The report prints the lines that have one, under a lead sentence generated from the row list, with the Oxford and Modified Ashworth sources as footnotes exactly as the proforma has them.

> Endurance and vehicle fit have no row, because the proforma has no row for them. Anything worth reporting about either goes in the summary of physical skills below the table — and a draft saved before this change has its endurance and vehicle-fit text moved there automatically.

### Manual muscle testing

**Optional, and folded away by default.** The Strength line above is the proforma's single sentence, and for most assessments that is the whole record. Open **grade individual muscle groups** where a group-by-group grade is needed.

Inside: the MRC (Oxford) 0–5 scale across twelve groups relevant to vehicle control, each annotated with why it matters for driving and each with its own how-to card and diagram (above). Every group starts as **not tested**, and the report states explicitly which groups were not tested and that no conclusion is drawn about them.

Where a section graded normally throughout, a **remaining → 5/5** button on each section heading (and one for the whole grid) marks the groups you have not touched yet as tested at grade 5. It is scoped to untouched groups only — a group you have already graded, or marked not tested with a reason, or marked N/A, is never changed. Comments are left empty, since the report's summary already states that power was 5/5 throughout the groups tested. An in-app reference card covers the grading scale, break-test technique and the grade-4-vs-5 error.

### Clinical interview

Eight occupational profile domains (six core), each with prompt questions to ask. Core domains need content, or an explicit not-applicable with a reason. Covers roles, work and study and social history; current transport and reliance on others; the purpose of driving and what the client expects from the assessment; insight into their own abilities and risk; fatigue, sleep, pain, medication timing and substance use; crashes, near-misses and infringements; and — where relevant — supports for supervised practice and learning style. Medical history, symptoms and driving history are recorded separately in Sections 1 and 3.

### Report-writing checks

The builder runs a standing set of checks over the report and lists everything it can see that is worth a second look. **None of them stop an export.** Export, print and the additional documents are always available; the badge in the toolbar tells you what is outstanding, and what to do about it is the assessor's call.

Click the badge for the list. Each entry says what it found and why it matters, carries the `§` section it lives in, and jumps to the field when clicked. Each stage tab carries its own count, so you can see what a phase still owes you before you leave it.

What gets checked: identity, licensing, referral and assessor fields; a student or supervisor recorded as present with no name, and a student present without the recorded consent; `[TBC]` left in the licence expiry; core profile domains; physical lines with no sentence recorded, and measurements that are not numbers; visual acuity; test scores; unrated on-road items, flagged issues with no comment and an undescribed intervention; an unconfirmed or untouched auto-draft summary; unresolved `{tokens}` and `[placeholders]`; outcome/finding contradictions (e.g. "fit to drive, no restrictions" alongside flagged issues; an instructor intervention beyond a verbal prompt alongside a supportive outcome; a vision standard recorded as not met alongside a supportive outcome); missing recommendations, consent or sign-off; an enabled additional document missing something essential; the competency standards; the competency-prompt fields (communication screen, MDI briefing, safety management, feedback given, licensing information, suitability decisions); contractions and unsupported phrasing ("seemed fine", "no issues", "I think", "obviously"); sentences over 45 words; missing terminal punctuation; thin sections by word count; short on-road duration; and flagged issues that do not appear in the summary.

Standard wording still sitting verbatim as inserted is exempt from the phrasing checks — it is flagged as unedited, not as sloppy writing.

A report that raises nothing is unusual, and a report that raises a handful is not a problem: the worked example flags nine, all of them things a real assessor would look at and most of them wave through. The list is there to be read, not cleared.

### Additional documents

Tick any of these in **Section 6** and they appear as tabs above the preview, each exporting to Word separately. All four are generated from the same assessment data as the main report, so they cannot drift from it or contradict each other — and each carries an optional free-text paragraph for anything specific to that reader.

| Document | Written for | Contains |
| --- | --- | --- |
| **Letter to GP / treating practitioner** | The treating doctor | One-page clinical summary: outcome, findings bearing on medical fitness to drive, medication, and an explicit list of what you are asking them to do |
| **NDIS support recommendations** | Planner, support coordinator, plan manager | Participant goals the assessment relates to, current functional impact, what was assessed, and each recommended support with a reasonable-and-necessary rationale and expected outcome |
| **Handover to driving instructor** | The MDI | Licence status, priority focus areas drawn from the flagged on-road issues, strengths to build on, how the client learns, safety notes including any intervention on the assessment drive, and what to report back and when |
| **Summary for client, family or support person** | The client and whoever supervises their practice | Plain-language account of what was done, the outcome, what went well, what needs practice, how to help, and next steps |

Only what belongs in each document goes into it — the NDIS participant number, for instance, appears on the NDIS document and nowhere else. Enabling a document that is missing something essential (a GP name, an NDIS number) is raised in the checks until it is supplied.

### Sign-off

A single confirmation in Section 8: that you have read the report end to end and every finding, interpretation and recommendation in it is supported by what you observed and recorded during the assessment. It is one of the checks.

### Auto-draft discipline

Auto-drafted text is a skeleton, not a report. The Section 6 summary carries a confirmation bar — you tick that the text reflects what you observed. The tick stores a hash of the text, so **editing afterwards silently un-ticks it** and you confirm again. An untouched auto-draft summary is raised in the checks until you have written into it.

### Competency coverage

All 50 standards from the *Australian Competency Standards for Occupational Therapy Driver Assessors* (Fields, Unsworth & Harreveld, 2018), mapped to the report. Most are evidenced automatically from what you entered; the rest are confirmed manually; ones that do not apply to the outcome are marked N/A. The four documentation standards (4.1, 4.2, 4.4, 4.5) are called out separately in the checks when they are not evidenced.

Fields exist for the competencies that previously had nowhere to be recorded: suitability screening, prior assessments, communication screen, MDI briefing, safety management during the drive, off-road and on-road feedback to the client, licensing/insurance information given, licence conditions considered, and report turnaround.

## Exporting the assessment as JSON

**Assessment JSON** in the toolbar opens the whole assessment as one labelled JSON object, ready to paste into a prompt. Copy it to the clipboard or download it as a file; the panel shows its size and a rough token count.

This is not the same thing as **Save draft**. A draft is the app's internal state, written so the app can read it back — full of codes like `"st": "mod"` and `"st": "unrated"` that mean nothing outside this file. The JSON export is written for something else to read:

- every stored code resolved to the words it stands for — `"rating": "Issue observed"`, `"status": "Moderate difficulty"`, `"response": "Low to medium density, building with experience"`;
- every `{token}` substituted, so the prose reads as the report reads;
- every auto-interpretation included alongside the raw score, so a model gets the threshold reasoning and not just a number;
- the criterion text for each on-road item and the relevance-to-driving line for each physical screen and muscle group, so nothing needs a glossary;
- the shape of the assessment preserved — on-road performance grouped by area with its area comment, interventions with whether each counts as a failed item, who was present and in which seat;
- the competency standards with their status, and the current outstanding checks;
- anything never recorded left out entirely, rather than present and empty.

```json
{
  "area": "Observation",
  "items": [
    {
      "item": "continuous near-to-far scanning",
      "criterion": "Continuous scanning to both left and right, short, middle and long distance",
      "rating": "Issue observed",
      "note": "As traffic density increased on the 60 km/h section approaching a shopping strip …"
    }
  ],
  "areaComment": "According to the government standards for safe driving, Mr Citizen did not check …"
}
```

Top-level keys follow the assessment: `document`, `practice`, `client`, `peoplePresent`, `licence`, `referral`, `assessment`, `presentation`, `occupationalProfile`, `drivingHistory`, `drivingNeeds`, `sensoryScreen`, `physicalScreen`, `cognitiveAndPerceptualScreen`, `psychosocialSkills`, `preDriveOutcomeSummary`, `offRoadFeedback`, `onRoadAssessment`, `outcome`, `additionalDocuments`, `governance`, `outstandingChecks`. A complete assessment runs to roughly 17,000 tokens, which fits comfortably in any current model's context.

> ⚠️ **It contains the client's identifying details** — name, date of birth, address, licence number, NDIS number — because the report does. Pasting it into a hosted model sends those details to that provider. De-identify it first if that is not appropriate for the client, and check it against your practice's privacy obligations before it leaves the machine.

The shape is defined in one place, `assessmentJSON()`, if you want to change what goes in it.

## On a tablet

The same page adapts — there is no separate mobile build to keep in sync. On any touch device up to desktop width (an iPad in either orientation, but not a 1280px laptop), the layout switches to **data entry first**:

- The four stage tabs stay pinned to the top of the form, sized for a thumb. On a phone they collapse to short labels so all four still fit across.
- The draft report is **hidden by default** and the form takes the full width. Tap **Report** in the toolbar to read it full-screen, and **✕ Close report** to get back. The choice is remembered, so it also works as a focus mode on desktop.
- While the report is hidden it is not re-rendered on every keystroke — it is marked stale and rebuilt when you open it, print or export, which keeps typing responsive.
- Controls are sized for fingers: 46px inputs, 42px buttons, 22px checkboxes, full-width rating selects on the on-road checklist. Inputs use 16px text so iOS does not zoom on focus.
- Secondary actions (load example, new, save/open draft, assessment JSON, export, print) collapse into a **⋯** menu so the toolbar stays one row.
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
| `PHYS_ROWS` / `MAS` | The physical table — the row list and its standard wording, how-to-screen text, measurement fields and threshold interpretation; the Modified Ashworth scale |
| `ATTENDEES` | The student and clinical-supervisor toggles, their involvement options and which of those put someone in the car |
| `CHECKLIST` | On-road performance areas, items and their standard wording |
| `INTERVENTIONS` | The instructor-intervention taxonomy, and which entries count as fail errors |
| `PREDRIVE_CATS` | Categories in the pre-drive outcome summary |
| `TEST_META` / `TEST_HOWTO` | Standardised tests — which are on by default, their score fields, their `comments` rows and standard sentences, and the procedure card shown for each |
| `TEST_ORDER_HEAD` / `TEST_ORDER_TAIL` | The order tests print in; anything not named still prints, after the tail |
| `STAGES` | The four assessment stages and which sections belong to each |
| `interp*()` | Score thresholds and interpretation wording |
| `REC_DEFS` | Recommendation library |
| `COMPETENCIES` | Competency standards and how each is evidenced |
| `REQ_FIELDS` | Fields checked for content — a fourth `'soft'` element words the check as good practice rather than a requirement |
| `BAD_PHRASES` / `CONTRACTIONS` | Writing-quality checks |
| `validate()` | Every check the review panel runs, in one flat list |
| `assessmentJSON()` | Shape of the exported assessment JSON |
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

Click **Load example** for a fully worked de-identified sample — complete profile, physical lines with their measurements, muscle grades, test scores, a pre-drive outcome summary, a familiarisation phase and rated on-road findings — which exports cleanly and shows what a finished report looks like. The sample client is fictional.

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
