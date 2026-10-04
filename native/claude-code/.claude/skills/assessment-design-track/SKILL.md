---
name: assessment-design-track
description: Takes an assessment from blueprint and objectives to items, mark scheme or rubric, accessibility review and a pilot check, pausing for teacher approval between steps.
license: CC0-1.0
arguments:
  - objectives_and_content
  - grade_level
  - assessment_type
argument-hint: <objectives_and_content> <grade_level> [assessment_type]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: teaching
  source: https://hermes-ide.com/prompts/assessment-design-track
  catalog: 2026.1004.3
---

# Assessment design track

## Inputs

- `objectives_and_content` (required): The objectives or standards the assessment must cover, and the content taught (unit outline, key topics, texts used).
- `grade_level` (required): Grade, age or course, e.g. "Grade 6", "Year 11 chemistry", "first-year undergraduate statistics".
- `assessment_type` (optional): Optional type and conditions, e.g. "40-minute end-of-unit test", "take-home essay", "practical exam", "oral presentation". If omitted, step 1 recommends one.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Builds an assessment for $grade_level covering these objectives and content:

<objectives_and_content>
$objectives_and_content
</objectives_and_content>
Only if assessment_type was provided: Assessment type and conditions: $assessment_type.

The assessment is built one approved step at a time: a blueprint that decides what is assessed, how much and at what depth; the items or tasks; the mark scheme or rubric; an accessibility and bias review; and a pilot check that rehearses marking on sample answers. Each step produces one document and stops for the teacher's approval or edits, and later steps build on the approved versions instead of re-asking. If the teacher asks to skip the approvals, say in one sentence that each step builds on the approved one before it, and continue only once they confirm; even then, produce the steps in order under their own headings so each can still be checked. The teacher decides what is assessed and how it is graded; the assistant drafts, checks alignment and flags problems. Every answer and mark must be checked for correctness before it is shown, and nothing is invented about the curriculum beyond what the teacher supplied.

## Steps

Work through these steps in order. Do not skip a gate.

1. blueprint (plan)
2. items (build)
3. marking (build)
4. accessibility-review (review)
5. pilot-check (verify)

### Step 1: Blueprint

Decide what the assessment measures, in what proportion and at what depth, before writing any item.

1. Ask the teacher, in one message, for anything missing that changes the design: the purpose (diagnostic, formative, end-of-unit, exam practice), the time and conditions, the total marks or grading scale, any required question types or exam board format, and students with access arrangements. If the assessment type was not given, recommend one that fits the objectives and say why.
2. When you have the answers, break the objectives into assessable parts, each with its cognitive demand (recall, apply, analyse, evaluate, create), using the verb in the objective.
3. Write the blueprint as a table: Objective part | Demand | Item or task type | Number of items | Marks | % of total. Weight by the importance and teaching time of each objective, and make sure the demands in the assessment match the demands in the objectives (an "evaluate" objective is not assessed only by recall items).
4. Check the timing: estimate minutes per item type and show that the total fits the time available, with reading and checking time.
5. List what is deliberately not assessed, and any assumptions.

Stop and wait for approval or edits. Do not write items yet.

**Gate:** stop here and wait for the user's approval before step 2 (items).

### Step 2: Items and tasks

Write the items or tasks exactly as the approved blueprint specifies.

1. Write each item or task in the blueprint's order or in a sensible order for students (easier items first within each section), numbered, with marks shown.
2. Follow item-writing rules:
   - each item assesses one blueprint part, at the stated demand;
   - multiple choice: one clearly correct answer, plausible distractors drawn from real misconceptions, no "all of the above", no grammatical or length clues, options in a logical order;
   - constructed response: the command word matches the demand (state, explain, compare, evaluate), and the question says how much is expected (marks, lines or length);
   - extended tasks and performance tasks: a clear brief, the conditions, and what the final product must include;
   - no item gives away another item's answer; contexts are familiar and inclusive.
3. Under each item, note privately for the teacher: the blueprint part it assesses, the correct answer or key points, and for distractors the misconception each represents.
4. Provide a student-facing version (items only, with instructions and space to answer) and a teacher version (with the notes).
5. Show a short coverage check: blueprint row → item numbers, and the total marks and estimated time.

Stop and wait for approval or edits. Do not write the mark scheme yet.

**Gate:** stop here and wait for the user's approval before step 3 (marking).

### Step 3: Mark scheme or rubric

Write how the approved items will be marked so that two markers would give the same score.

1. For short items: the accepted answers, acceptable alternatives, what does not earn the mark, and how to treat units, spelling or follow-through errors.
2. For multi-mark constructed responses: a points-based scheme (each creditable point and its mark) or a levels-based scheme (level descriptors with mark ranges and indicative content), whichever fits the item, and say which and why.
3. For extended or performance tasks: an analytic rubric with 3 to 6 non-overlapping criteria and level descriptors that name observable features of the work, tied to the blueprint's objective parts.
4. Write one short exemplar answer at the top level for each extended response, labelled as illustrative.
5. Add marking guidance: how to handle borderline answers, answers that are correct but unexpected, and blank or off-task responses; and how marks convert to the grading scale from step 1.
6. Check every key answer and total. Confirm the marks per item match the approved items and the totals match the blueprint.

Stop and wait for approval or edits.

**Gate:** stop here and wait for the user's approval before step 4 (accessibility-review).

### Step 4: Accessibility and bias review

Review the approved items and mark scheme so the assessment measures the objectives, not reading speed, background or access.

Check and report:
1. **Language load:** sentences, vocabulary and layout harder than the objective requires; suggest plainer wording that keeps the demand (subject vocabulary that is being assessed stays).
2. **Construct-irrelevant barriers:** items that depend on cultural knowledge, family circumstances, or experiences some students will not have; idioms; unnecessary context.
3. **Format and layout:** font and spacing, items split across pages, diagrams that need colour, tables without headers, insufficient answer space, and readability for screen readers if delivered digitally.
4. **Access arrangements:** how the assessment works with the arrangements mentioned in step 1 (extra time, reader, scribe, word processor, enlarged print, rest breaks), and whether any item conflicts with them (for example a reader would give away a vocabulary item).
5. **Bias and representation:** names, roles and contexts are varied and free of stereotypes.

Output a table: Item | Issue | Severity (must fix / should fix / consider) | Suggested change. Then list the revised wording for must-fix items. Make no other edits; the teacher decides.

Stop and wait for approval or edits.

**Gate:** stop here and wait for the user's approval before step 5 (pilot-check).

### Step 5: Pilot check

Rehearse the assessment before students take it, using the approved items and mark scheme.

1. **Sample answers:** for 4 to 6 items, including the extended ones, write three short simulated student answers (strong, middling, a common misconception), clearly labelled as simulated. Mark each against the scheme and show the marks awarded with reasons.
2. **Marking problems:** list any place where the scheme was ambiguous, gave credit for a wrong idea, or could not separate the middling from the strong answer, with a fix.
3. **Timing and difficulty:** estimate whether the assessment fits the time and whether the difficulty curve is reasonable for the class; identify items likely to be too easy or too hard to tell students apart.
4. **Final checks:** totals add up, numbering is continuous, instructions match the items, and every blueprint row is covered.
5. **After the real sitting:** suggest what to look at once results are in (items most students missed, items strong students missed, distractors nobody chose) and how to use that to improve the next version.

End with a short summary of what is ready and what still needs the teacher's decision. Make no further edits yourself.
