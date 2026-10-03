---
name: understand-assignment-brief
description: Decodes an assignment brief and rubric into what is actually being asked, the hidden expectations, a dated step plan and a pre-submission checklist. Use when starting coursework.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: studying
  source: https://hermes-ide.com/prompts/understand-assignment-brief
  catalog: 2026.1003.1
---

# Understand an assignment brief

## Inputs

- [BRIEF] (required): The assignment brief exactly as given, including the title or question, word count, format, referencing style and submission instructions.
- [RUBRIC] (optional): Optional marking rubric, criteria or grade descriptors. Without one, hidden expectations are inferred from the brief and labelled as such.
- [DUE_DATE] (optional): Optional due date and time, plus today's date so the plan can be dated, for example "14 March 23:59; today is 20 February".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Students lose more marks to misreading the brief than to weak writing: answering "describe" when the brief says "critically evaluate", missing a required section, ignoring the weighting of the criteria, or writing an essay when a report was asked for. Briefs also carry expectations they never state outright, such as "use of literature" meaning peer-reviewed sources rather than websites. The job is to make every requirement explicit, separate what is stated from what is inferred, and turn the deadline into a plan.
</context>

<task>
Decode this assignment brief.

<brief>
[BRIEF]
</brief>
Only if [RUBRIC] was provided: 
<rubric>
[RUBRIC]
</rubric>
Only if [DUE_DATE] was provided: Due: [DUE_DATE].

1. State the core task in one plain sentence: what the student must produce and what it must do.
2. Analyse the command words (analyse, discuss, evaluate, critically assess, compare, justify, reflect). For each, say what it demands in practice and how it differs from the weaker thing students usually do instead.
3. Extract every explicit requirement: deliverable type, word count and whether references count, sections, format, sources, referencing style, submission method and file type, collaboration and AI-use rules if stated.
4. Infer the hidden expectations: what the top grade band needs that a pass does not, how the marks are weighted across criteria, the genre conventions of the deliverable (a report has headings and an executive summary; a literature review synthesises rather than lists). Base each inference on the brief's or rubric's wording and quote it. Mark each as inferred.
5. List ambiguities that only the tutor can settle, phrased as short questions the student can send.
6. Build a step plan working back from the due date: understand and question, research, plan or outline, draft, revise against the rubric, proofread and reference check, submit early. Size each step to the deliverable and leave a buffer of about 15 percent. Use real dates if the due date and today's date are given; otherwise use "D-14"-style countdowns and say so.
7. Write a pre-submission checklist tied to the rubric's criteria and the explicit requirements, each item checkable as yes or no.
</task>

<constraints>
- Do not write any part of the assignment: no thesis, paragraphs or answers. Planning steps can name what each section must achieve.
- Never invent a requirement. Anything not in the brief or rubric is labelled "inferred" with its reason, or goes in the questions for the tutor.
- If the brief is too thin to decode (only a topic, no task or format), say what is missing and give the questions to ask, rather than guessing a word count or format.
- Use the rubric's own words when referring to criteria, so the student can match them.
</constraints>

<output_format>
## The task in one sentence
## What the brief requires
A checklist of stated requirements, each with the brief's wording quoted.
## What the marker is really looking for
Command words first, then inferred expectations, each marked "(inferred)" with its evidence. If a rubric is given, a table: Criterion | Weight | What top band needs | Common way to lose marks.
## Questions to ask your tutor
## Plan
A table: Step | What to do | Done by.
## Pre-submission checklist
Checkboxes.
</output_format>
