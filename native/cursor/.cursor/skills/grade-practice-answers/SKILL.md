---
name: grade-practice-answers
description: Marks practice answers against a mark scheme or rubric, giving per-question feedback and the marks a strict examiner would award. Use after attempting past papers or practice questions.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: exam-prep
  source: https://hermes-ide.com/prompts/grade-practice-answers
  catalog: 2026.1002.0
---

# Grade practice answers like a strict examiner

## Inputs

- [QUESTIONS] (required): The questions, numbered, with the marks available for each if known.
- [ANSWERS] (required): Your answers, numbered to match the questions.
- [MARK_SCHEME] (optional): Optional official mark scheme or rubric. Without one, a scheme is drafted first and the marks are labelled estimates.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Students over-mark their own practice answers: they read in what they meant, not what they wrote. Real examiners award marks only for creditworthy points that appear on the page, in the terms the mark scheme accepts, and they penalise answers that ignore the command word ("explain" answered with a description). Practice is only useful if the marking is as strict as the real exam.
</context>

<task>
Mark these practice answers.

<questions>
[QUESTIONS]
</questions>

<answers>
[ANSWERS]
</answers>

Only if [MARK_SCHEME] was provided: 
<mark_scheme>
[MARK_SCHEME]
</mark_scheme>
Mark strictly to this scheme.

1. Settle the scheme. If none was given, draft one per question: the creditworthy points, the mark for each, and what a full-mark answer needs. Use the marks shown in the questions; if none are shown, assume a sensible tariff and say so.
2. Mark each answer as a strict but fair examiner:
   - Award a mark only when the point is clearly stated. Vague, contradictory or "hedged list" answers do not earn the point.
   - Check the command word: "explain" needs a reason or mechanism, "evaluate" needs a judgement, "calculate" needs working and units if the scheme credits them.
   - Apply error carried forward in calculations where the scheme allows it: a later step done correctly from an earlier wrong value can still earn method marks.
   - Accept correct alternatives that the scheme would accept in substance, and say when you did.
3. For each question, give the marks, which points were credited, which were missed, and one sentence on what would have earned the missing marks, phrased as a point to include, not as a model answer.
4. Total the marks, give a percentage, and identify patterns across questions.
</task>

<constraints>
- Be strict: when in doubt between two marks, give the lower one and say why.
- Do not invent marking points beyond what the scheme, or your drafted scheme, contains. Without an official scheme, label every mark as an estimate.
- If an answer is missing, give 0 and move on. If the numbering does not match, ask which answer belongs to which question.
- If a question in the mark scheme itself looks wrong, flag it rather than marking against it.
- Keep feedback specific to what was written; quote the answer where it helps.
</constraints>

<output_format>
## Mark scheme used
"Official scheme" or the drafted scheme as a compact list per question.
## Results
A table: Q | Marks | Credited | Missed. Then a line: Total x / y (z%), followed by "(estimated)" if no official scheme was given.
## Question by question
For each question: marks, a short justification quoting the answer, and "To gain the missing marks: …".
## Patterns
Up to 3 bullets on recurring issues (command words, missing units, unsupported claims, timing), each with the questions it affected.
</output_format>
