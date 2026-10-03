---
name: differentiate-lesson
description: Adapts an existing lesson for mixed abilities, English learners and students with documented accommodations while keeping the same learning goal. Use when one lesson must reach a varied class.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/differentiate-lesson
  catalog: 2026.1003.0
---

# Differentiate a lesson

## Inputs

- [LESSON] (required): The existing lesson plan or activity, as written.
- [LEARNER_NEEDS] (required): The groups of learners to plan for, described without names, e.g. "4 students reading two years below grade; 3 newcomer English learners (Spanish, Arabic); 1 student with an IEP for extended time and text-to-speech; 5 students who finish early".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Differentiation goes wrong in two directions: lowering the goal for some students ("they'll just colour the diagram"), or making three separate lessons the teacher cannot run. The workable approach keeps one shared learning goal and changes the route: scaffolds that can be removed, extension that goes deeper rather than producing more of the same, language supports that let English learners do the full thinking, and accommodations applied exactly as documented.
</context>

<task>
Adapt this lesson for the learners described.

<lesson>
[LESSON]
</lesson>

<learner_needs>
[LEARNER_NEEDS]
</learner_needs>

1. State the lesson's core learning goal in one sentence. Every adaptation must still lead to it.
2. Break the lesson into its segments and, for each, plan:
   - **Support:** scaffolds such as worked examples, sentence starters, partially completed organisers, chunked instructions, pre-taught vocabulary, manipulatives. Say when each scaffold is faded.
   - **Extension:** depth, not more volume: a harder case, a "why does this work", a transfer task, or a role explaining to peers.
   - **English learners:** a language objective for the lesson, key vocabulary with visuals, sentence frames matched to proficiency (beginning, intermediate, advanced), and opportunities to talk before writing. Allow home-language use for thinking where it helps.
   - **Accommodations:** apply exactly what is documented in the learner needs (extended time, text-to-speech, seating, reduced copying). Do not add, remove or reinterpret accommodations, and do not modify the learning goal unless a modification is documented.
3. List every material to prepare, with a one-line description so the teacher can make it quickly.
4. Recommend grouping for each segment, kept flexible: groups change by task, not fixed ability tracks.
5. Plan a check for understanding that every group can show, with how the teacher reads the results across groups.
</task>

<constraints>
- Keep the lesson runnable by one teacher in the same time. If an adaptation would need extra adults or time, say so and offer a lighter alternative.
- Refer to learners only by the group descriptors given. If names or health details appear in the input, do not repeat them.
- Do not infer or name diagnoses from the needs described.
- If the lesson or the needs are too vague to adapt (no activities listed, or "some kids struggle"), ask up to three specific questions and stop.
</constraints>

<output_format>
## Core goal
One sentence, plus the language objective.
## Adaptations by segment
A table: Segment (time) | Core activity | Support | Extension | English learners | Accommodations.
## Materials to prepare
Checklist.
## Grouping
One line per segment.
## Check
The check, and what the teacher looks for in each group's responses.
</output_format>
