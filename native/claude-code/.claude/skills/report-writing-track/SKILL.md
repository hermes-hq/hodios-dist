---
name: report-writing-track
description: Takes a work report from purpose and audience to an answer-first outline, an evidence check, a full draft, an executive summary and a final edit, pausing for approval between steps.
license: CC0-1.0
arguments:
  - report_purpose
  - source_material
  - audience
argument-hint: <report_purpose> <source_material> [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: business-writing
  source: https://hermes-ide.com/prompts/report-writing-track
  catalog: 2026.1003.2
---

# Report writing track

## Inputs

- `report_purpose` (required): Why the report is being written and what should happen after it is read, for example "recommend whether to renew the cleaning contract" or "report the results of the customer survey to the board".
- `source_material` (required): The data, notes, interview findings, documents and figures the report must be built from. Label sources if you can.
- `audience` (optional): Who reads it, what they already know, and who decides anything.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Writes a work report one approved step at a time, as an experienced report writer and editor would: brief, answer-first outline, evidence check, draft, executive summary, then a final edit.

<report_purpose>
$report_purpose
</report_purpose>

<source_material>
$source_material
</source_material>
Only if audience was provided: 

Audience: $audience

Each step produces one artifact and stops for approval or edits. Later steps build on the approved versions and do not reopen them unless the writer asks. If the source material is unlabelled, label the sources S1, S2, … in the order given and use those labels throughout. Use only facts, figures and quotes from the source material; mark anything missing as `[NEEDED: …]` instead of inventing data, results, quotes or names. If the writer asks to skip the approvals, confirm once that later steps will build on unreviewed choices; if they agree, run the remaining steps in one reply and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. brief (plan)
2. outline (design)
3. evidence (verify)
4. draft (build)
5. summary (build)
6. edit (review)

### Step 1: Purpose and audience brief

Pin down what the report must do before any structure exists.

1. Two things are essential: what the reader should decide, do or understand after reading, and enough source material to support it. If either is missing, ask for it in one message, with the audience, deadline, template or length and who signs off, then stop. Otherwise do not ask: write the brief and list your assumptions.
2. Write a brief of no more than one page:
   - **Purpose:** "After reading this, [reader] will …", one sentence. If a decision is wanted, name it exactly.
   - **Readers:** who acts, who is informed, what they know and care about, and how much they will read.
   - **Key questions:** the three to five questions the report must answer, in the reader's words.
   - **Scope:** what is in and out, and the period or population the data covers.
   - **Constraints:** length, template, house style, deadline, confidentiality.
   - **Material on hand:** the sources by label and what each can answer.
   - **Assumptions to confirm:** each default you chose, one line each.

Stop and wait for approval or edits. Do not outline yet.

**Gate:** stop here and wait for the user's approval before step 2 (outline).

### Step 2: Answer-first outline

Build the argument before the prose, from the approved brief.

1. State the governing message: the one sentence that answers the purpose. If the material does not yet support one, give the most likely answer, mark it provisional and say what would confirm it.
2. Group the support pyramid-style: three to five key points, each a full sentence supporting the message, with the findings beneath each. Points at one level are of the same kind and do not overlap.
3. Choose the section order and say why: answer first for decision-makers; situation, complication, resolution when context is needed; chronological only for an account of events.
4. For each section, write the heading as a takeaway ("Repeat contacts drive half of support cost", not "Support analysis"), the source labels it draws on, any table or chart it needs, and a target word count.
5. Mark what goes in appendices (method, full tables) so the body stays lean.

Stop and wait for approval or edits. Do not check evidence or draft yet.

**Gate:** stop here and wait for the user's approval before step 3 (evidence).

### Step 3: Evidence check

Test every claim in the approved outline against the sources before writing.

1. Table every claim (message, key points, findings): Claim · Sources · What the source actually says · Strength · Issue.
2. Strength: **strong** (directly stated by a reliable source, figures match), **adequate** (indirect, small sample or one source), **weak** (inferred or anecdotal), **unsupported** (no source).
3. Recompute totals, percentages and changes from raw figures where given; check units and periods; flag any figure that differs between sources.
4. Flag conflicts between sources, overreach (correlation as cause, a sample generalised to everyone) and data too old for the decision.
5. For each weak or unsupported claim, recommend: soften it, find the evidence (say what and where), or drop it. If the governing message itself is weak, say so and propose a reframe.

Stop and wait for approval or edits. The draft will use only claims the writer keeps.

**Gate:** stop here and wait for the user's approval before step 4 (draft).

### Step 4: Draft

Write the body from the approved outline and evidence decisions.

1. Follow the approved order and takeaway headings. Open each section with its takeaway, then the support, then what it means for the reader.
2. State each claim at the strength the evidence check allowed, with its limits ("in the 40 stores surveyed"); leave out dropped claims.
3. Cite sources by label or in the writer's template format. Keep figures exactly as checked, with units and periods.
4. Build the planned tables and charts, each titled with its message.
5. End with conclusions and, if the purpose asks, recommendations: each a specific action with an owner role and timing, traced to its findings.
6. Keep to the word targets: short paragraphs, plain language, active voice, terms defined once. Method and long tables go in appendices.
7. Do not write the executive summary yet.

Stop and wait for approval or edits.

**Gate:** stop here and wait for the user's approval before step 5 (summary).

### Step 5: Executive summary

Write the summary from the approved draft, for a reader who reads nothing else.

1. About 10% of the body, at most one page.
2. Open with the governing message and, if a decision is wanted, the decision and the date it is needed.
3. Then the key points by importance, each with its strongest figure; the main recommendation or next steps; the main risk or limitation.
4. Add nothing that is not in the draft, and keep figures and certainty exactly as in the body. State findings; do not describe the report ("This report examines…").

Stop and wait for approval or edits.

**Gate:** stop here and wait for the user's approval before step 6 (edit).

### Step 6: Final edit

Edit the approved summary and draft into the final report.

1. **Consistency:** figures, names, dates and terms match across summary, body, tables and appendices.
2. **Clarity:** cut throat-clearing and stacked hedges, break sentences over about 30 words, replace jargon, and fix any sentence a reader could read two ways.
3. **Honesty:** no claim stronger than the evidence check allowed; limitations stated once, where they matter.
4. **Mechanics:** spelling, numbers, capitalisation and citations consistent with the house style if given.
5. Return the final report in full, a short change log by type, and the remaining `[NEEDED: …]` items to fill before sending.

This is the last step.
