---
name: create-coding-exercises
description: Generates a graded set of coding exercises for one concept, each with starter code, automated tests, staged hints and a reference solution. Use for teaching, practice sessions or self-study.
license: CC0-1.0
arguments:
  - concept
  - language
  - level
  - count
argument-hint: <concept> <language> [level] [count]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: learning
  source: https://hermes-ide.com/prompts/create-coding-exercises
  catalog: 2026.1003.1
---

# Create graded coding exercises

## Inputs

- `concept` (required): The concept to practise, for example "recursion on trees", "SQL window functions" or "async error handling".
- `language` (required): The programming language, and test framework if it matters, for example "Python with pytest".
- `level` (optional; one of: beginner, intermediate, expert; default: beginner): The learners' level.
- `count` (optional; default: 5): How many exercises to generate.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Good exercises isolate one skill, rise in difficulty in small steps, and give immediate, objective feedback through tests. Hints should unblock without giving the answer away, so they are staged from a nudge to a near-solution. Exercises fail learners when the tests do not match the instructions, when the starter code already passes, when a step jumps in difficulty, or when the "beginner" exercise quietly needs a concept that was never taught.
</context>

<task>
Create $count exercises on $concept in $language for $level learners.

1. State the learning objective and the prerequisites you assume for this level. If the concept is too broad for $count exercises, narrow it and say how.
2. Plan the progression: the first exercise applies the concept in its simplest form; each next one adds exactly one new difficulty (an edge case, a combination with another known concept, a performance or design constraint). The last one is a small realistic task.
3. For each exercise write:
   - a title and a one-line objective;
   - the problem statement with input, output and constraints, and one or two examples;
   - starter code: signatures, types and docstrings, with the body left for the learner (it must run, and the tests must fail against it);
   - tests in the language's standard test framework covering the examples, edge cases (empty, boundary, invalid input as specified) and one case that catches the most common wrong approach;
   - three staged hints: hint 1 points to the relevant idea, hint 2 outlines the approach, hint 3 gives the key line or structure without the full solution;
   - common mistakes the tests are designed to catch.
4. Write a reference solution for each, idiomatic for the language, with a short explanation and its time and space complexity where relevant.
5. Check every exercise by running it if you can, otherwise by tracing each test by hand: the reference solution passes all its tests, the starter code fails them, and the statement mentions every behaviour the tests check. Fix any mismatch before answering.
</task>

<constraints>
- Every test must follow from the problem statement. No hidden requirements.
- Use only the language's standard library unless the concept is about a library, and name the version if behaviour depends on it.
- Keep each exercise solvable in 10 to 30 minutes at the stated level.
- Keep solutions out of the exercise section so it can be handed out alone.
</constraints>

<output_format>
## Overview
Objective, assumed prerequisites, and a table: # | Title | New difficulty | Estimated time.
## Exercises
For each: title, objective, statement, starter code block, test code block, hints (labelled Hint 1, 2, 3), common mistakes.
## Solutions
For each: reference solution code block, explanation, complexity.
</output_format>
