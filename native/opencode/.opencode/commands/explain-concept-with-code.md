---
description: Explains a programming concept through the problem it solves, a minimal runnable example, a common mistake and a quick self-check, pitched at the learner's level. Use to learn or teach a concept.
---

# Explain a concept with code

## Inputs

- [CONCEPT] (required): The concept to explain, for example closures, database indexes, async/await or dependency injection.
- [LANGUAGE] (optional): The language or stack for the examples. Leave empty to use the one the learner is working in, or the most common one for the concept.
- [LEVEL] (optional; one of: beginner, intermediate, expert; default: intermediate): The learner's level.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
People understand a concept when they see the problem it solves before the solution, run a small example, and then see it break in a realistic way. Definitions alone do not stick, and analogies mislead when they are stretched. The example is the core of the explanation, so it has to run exactly as written.
</context>

<task>
Explain [CONCEPT] to a learner at the [LEVEL] levelOnly if [LANGUAGE] was provided: , with examples in [LANGUAGE].

1. Give a one-sentence definition in plain words.
2. Show the problem first: a few lines of code that are awkward, buggy or slow without the concept.
3. Show the same code using the concept: a minimal, complete, runnable example with imports and a `main` or entry point if the language needs one, and the expected output as a comment.
4. Walk through how it works, step by step, referring to specific lines. For beginner, define every new term; for expert, go to the mechanism (memory, scheduling, complexity, the spec) and skip the basics.
5. Show one common mistake with the concept, what happens, and the fix.
6. Say when not to use it, and what to use instead.
7. End with two short questions the learner can answer to check understanding, with answers after a separator.
</task>

<constraints>
- The examples must run as written on a current stable version of the language. State the version or runtime if behaviour depends on it.
- If the concept is used differently in different languages, say so in one line and stay with the language of the examples.
- Use at most one analogy, and say where it stops being accurate.
- Do not claim performance numbers without saying they depend on the workload.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Markdown with these `##` headings, in order: In one sentence, Why it exists, Example, How it works, Common mistake, When not to use it, Check yourself.
Code blocks have a language tag. Keep each example under 30 lines.
</output_format>

Arguments: $ARGUMENTS
