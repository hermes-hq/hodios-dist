---
name: give-essay-feedback
description: Gives rubric-based feedback on a student essay covering thesis, evidence, structure and style, with prioritized revisions, without rewriting it. Use before a draft is submitted.
license: CC0-1.0
arguments:
  - essay
  - assignment
  - rubric
  - grade_level
argument-hint: <essay> [assignment] [rubric] [grade_level]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: tutoring
  source: https://hermes-ide.com/prompts/give-essay-feedback
  catalog: 2026.1003.1
---

# Give feedback on an essay

## Inputs

- `essay` (required): The full essay text.
- `assignment` (optional): Optional assignment prompt or question the essay answers.
- `rubric` (optional): Optional rubric or mark scheme. Without one, the feedback uses thesis, evidence, structure and style.
- `grade_level` (optional): Optional grade or course level, e.g. "Grade 10", "first-year university". Calibrates expectations.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Useful essay feedback is specific, prioritised and leaves the writing to the writer. Writers can act on two or three big changes per draft; a list of thirty edits gets ignored, and rewritten sentences teach nothing and blur whose work it is. Fix higher-order concerns (argument, evidence, organisation) before lower-order ones (sentences, mechanics), because revising the argument often deletes the sentences you would have polished.
</context>

<task>
Give feedback on the essay belowOnly if grade_level was provided:  for a $grade_level writer.
Only if assignment was provided: 
<assignment>
$assignment
</assignment>
Only if rubric was provided: 
<rubric>
$rubric
</rubric>
Use this rubric's criteria, level names and points exactly.

<essay>
$essay
</essay>

1. Read the whole essay once without judging. Then restate its thesis and line of argument in two sentences. If you cannot find a thesis, say that; it is the most important finding.
2. Assess each criterion. Without a rubric, use:
   - **Thesis:** arguable, specific, and answers the assignment.
   - **Evidence:** relevant, sufficient, accurately represented, and analysed rather than dropped in; quotations are introduced and explained.
   - **Structure:** each paragraph has one job, signalled by its topic sentence; the order builds the argument; transitions show logical relationships.
   - **Style:** clear, concise, appropriate register; mechanics only as recurring patterns.
   Support every judgement with a short quotation or a paragraph reference.
3. Choose the 3 to 5 revisions that would most improve the essay, ordered by impact, higher-order first. For each, say where, what the problem is, why it matters to a reader, and a strategy or question to fix it.
4. Identify up to 3 recurring sentence-level patterns, each with one example from the essay and the principle behind the fix, not the fixed sentence.
5. Start with genuine, specific strengths: name what works so they keep doing it.
</task>

<constraints>
- Do not rewrite the essay or any sentence of it, and do not write replacement paragraphs. You may show a technique on an invented sentence about a different topic.
- If the assignment is given, check that the essay actually answers it; drifting off the question outranks every other issue.
- With a rubric that has points, give a level and points per criterion and say they are an estimate. Without one, do not give a grade.
- Calibrate to the grade level: do not expect graduate-level nuance from a Grade 8 writer, and do not praise a university essay for basics.
- Do not invent facts about the sources; if you suspect a factual error or a misquotation, say "check this" rather than asserting.
- If the essay is shorter than a paragraph, or is not an essay, say what you need and stop.
</constraints>

<output_format>
## Your argument as I read it
Two sentences.
## Rubric feedback
A table: Criterion | Level (or Strong / Developing / Needs work) | Evidence from the essay | Comment. Strengths first in each comment.
## Top revisions
Numbered, most important first. Each: Where — Problem — Why it matters — Try this.
## Sentence-level patterns
Up to 3 bullets, each with one quoted example.
## A question for you
One question that pushes the argument further.
</output_format>
