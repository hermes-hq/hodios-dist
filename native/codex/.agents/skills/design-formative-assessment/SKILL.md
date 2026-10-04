---
name: design-formative-assessment
description: Designs in-lesson formative checks (hinge questions, mini-whiteboard prompts, exit tickets) that reveal specific misconceptions, with a decision rule for what to do next.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/design-formative-assessment
  catalog: 2026.1004.0
---

# Design formative checks for a lesson

## Inputs

- [LESSON_OBJECTIVE] (required): What students should be able to do by the end of the lesson, e.g. "add fractions with unlike denominators" or "explain why the Treaty of Versailles angered Germany".
- [GRADE_LEVEL] (required): Grade, age or course, e.g. "Grade 4", "Year 10 chemistry", "adult ESOL entry 3".
- [SUBJECT] (optional): Optional subject, if the objective does not make it obvious.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A formative check is only useful if the teacher can read the whole class's answers in under a minute and each wrong answer tells them something different. "Any questions?" and "thumbs up if you get it" fail both tests. Strong checks are diagnostic: a hinge question placed at the point where the lesson turns, whose wrong options each map to one known misconception; mini-whiteboard prompts with short answers the teacher can scan; and an exit ticket that sorts students into groups for the next lesson. The check is half the job. The other half is the decision the teacher makes from it.
</context>

<task>
Design the formative checks for one lesson.

Objective: [LESSON_OBJECTIVE]
Grade level: [GRADE_LEVEL]
Only if [SUBJECT] was provided: Subject: [SUBJECT]

1. Rewrite the objective as 2 or 3 student-facing success criteria ("I can…") with observable verbs.
2. List the 3 to 5 misconceptions or errors students at this level most commonly have with this objective. For each, say what the student believes and why it is tempting. Use known, documented misconceptions for the subject where they exist; do not invent exotic ones.
3. Plan where checks go in the lesson: one after the opener (prior knowledge), one hinge point at the moment the lesson moves from teaching to practice, and the exit ticket at the end.
4. Write one hinge question: multiple choice with 3 or 4 options, answerable in under a minute, with exactly one correct answer and every wrong option mapped to one misconception from step 2. Students who hold the misconception should find their option convincing. Avoid "all of the above", trick wording and options that are obviously silly.
5. Write 4 to 6 mini-whiteboard prompts with short answers (a number, a word, a sketch, a choice) the teacher can scan at a glance. For each, give the correct answer and the most likely wrong answer with what it reveals.
6. Write a 2 or 3 question exit ticket tied to the success criteria, with answers and a sorting rule: which responses mean "secure", "nearly" and "not yet".
7. Give decision rules for the hinge question and the exit ticket: what the teacher does when roughly 80% or more answer correctly, when the class is split, and when most are wrong. Make each response concrete (re-teach with a different representation, pull a small group, a worked example to show), not "review the concept".
</task>

<constraints>
- Every item must assess the objective as stated, not a neighbouring skill, and be answerable without reading-heavy context unless reading is the objective.
- Keep language at the reading level of [GRADE_LEVEL]. For younger students, prefer pictures, number lines or choices over written explanations.
- Check every correct answer before you finish. If the objective is ambiguous or too broad for one lesson (for example "understand fractions"), say how you narrowed it and design for the narrowed version.
- If you are unsure that a misconception is common at this level, mark it "possible" rather than presenting it as established.
- No formats that need technology or purchased materials unless the teacher mentioned them. Paper, mini whiteboards, fingers and cards are fine.
</constraints>

<output_format>
## Success criteria
"I can…" bullets.
## Likely misconceptions
Numbered: the misconception, what the student believes, why it is tempting.
## Check plan
Table: When in the lesson | Check | Time needed | What it tells you.
## Hinge question
The question and options, then a table: Option | Correct? | Misconception it reveals (by number).
## Mini-whiteboard prompts
Numbered: prompt · correct answer · likely wrong answer → what it reveals.
## Exit ticket
Questions with answers, then the sorting rule (secure / nearly / not yet).
## Decision rules
For the hinge question and the exit ticket: ≥80% correct · split · most wrong → what the teacher does next, in one or two sentences each.
</output_format>
