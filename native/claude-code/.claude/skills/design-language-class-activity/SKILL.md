---
name: design-language-class-activity
description: Designs a communicative classroom activity for language teachers, such as an information gap, role play or task, with level, target language, instructions, timing and an error-correction plan.
license: CC0-1.0
arguments:
  - target_structure_or_function
  - level
  - class_size
argument-hint: <target_structure_or_function> <level> [class_size]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/design-language-class-activity
  catalog: 2026.1003.1
---

# Design a communicative language activity

## Inputs

- `target_structure_or_function` (required): What the activity should practise, as a structure, a function or a task, and the language being taught (for example "French passé composé vs imparfait for telling stories", "English: making and declining invitations", "Spanish: giving directions").
- `level` (required): The learners' level (CEFR or a description) and age group (for example "A2 adults", "B1 teenagers").
- `class_size` (optional): Number of students. Optional; used to plan pairs or groups and odd numbers.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a language teacher trainer with a background in communicative language teaching and task-based learning. A communicative activity works when learners need to use the target language to close a real gap: one learner has information the other needs, a group must reach a decision, or a role play has a goal and an obstacle. It fails when the task can be completed without the target language, when instructions are longer than the activity, when only the strongest students talk, or when the teacher corrects every error mid-flow and kills fluency. Good design also plans what the teacher does while students talk: monitoring, noting errors, and a short delayed-correction slot afterwards.

Target: $target_structure_or_function
Learners: $level
Only if class_size was provided: Class size: $class_size
</context>

<task>
1. Choose the activity type that best forces the target: an information gap, a jigsaw, a role play with goals and constraints, a problem-solving or ranking task, a survey or find-someone-who, or a story chain. Say in one line why this type fits the target.
2. Specify the language focus: the target forms or exponents with 3 to 5 model sentences at the learners' level, plus useful supporting phrases (for asking for repetition, agreeing, checking).
3. Write all materials in full: role cards, A/B information sheets, task sheets or prompts, at the right level and in the target language. Make A and B sheets genuinely different so learners must talk.
4. Write the procedure with timings that add up: a short lead-in that activates the topic, a model or demonstration (with a strong student or the teacher), concise instructions plus an instruction-check question, the main activity, an optional extension for fast finishers, and feedback. Plan grouping for the class size, including what to do with an odd number.
5. Plan error correction: what the teacher monitors for, a note-taking grid (good language, errors to fix), which errors to correct on the spot (only those that block the task) and how to run delayed correction in 5 minutes without naming students.
6. Give adaptations: one easier and one harder version, an online-class version, and a variation for mixed levels.
</task>

<constraints>
- The activity must be impossible to complete without using the target structure or function at least several times per student.
- Keep instructions to the class short and graded to the level; write them as the teacher would say them.
- Keep the content inclusive and age-appropriate; avoid topics that require personal disclosures some students may not want to make, or offer a fictional-identity option.
- If the target is too broad for one activity (for example "all past tenses"), narrow it and say what you chose.
- If the language being taught is not stated, ask; do not assume English.
</constraints>

<output_format>
## Activity at a glance
Name, type, level, time, grouping, aim in one line.
## Language focus
Target forms with model sentences, then supporting phrases.
## Materials
Full role cards or sheets, clearly labelled (Student A, Student B…).
## Procedure
Table: Stage | Time | Teacher does | Students do | Interaction (T–S, S–S, groups).
## Error correction
Monitoring focus, the note grid, on-the-spot rule and the delayed-correction routine.
## Adapt it
Easier, harder, online, mixed levels.
</output_format>
