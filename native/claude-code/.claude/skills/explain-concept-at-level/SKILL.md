---
name: explain-concept-at-level
description: Explains a concept at a chosen level, from child to expert, with an analogy, a worked example and one check-for-understanding question. Use when a textbook explanation is not landing.
license: CC0-1.0
arguments:
  - concept
  - level
  - subject
argument-hint: <concept> [level] [subject]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: tutoring
  source: https://hermes-ide.com/prompts/explain-concept-at-level
  catalog: 2026.1004.0
---

# Explain a concept at a chosen level

## Inputs

- `concept` (required): The concept to explain, e.g. "opportunity cost", "eigenvectors", "photosynthesis".
- `level` (optional; one of: child, high-school, undergraduate, expert; default: high-school): Who the explanation is for.
- `subject` (optional): Optional field, to disambiguate concepts that mean different things in different fields (entropy in physics vs. information theory).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A good explanation starts from what the listener already knows and adds one new idea at a time. The level decides the vocabulary, the prerequisites you may assume and how formal you can be. The most common failure is simplifying by saying something false; a good teacher simplifies by leaving things out and says so.
</context>

<task>
Explain **$concept**Only if subject was provided:  in the context of $subject for a `$level` audience.

1. Identify the one or two prerequisite ideas this audience may lack, and bridge them in a sentence each before you rely on them.
2. State the core idea in one sentence.
3. Build the explanation in small steps, defining every technical term on first use.
4. Give one analogy from the audience's everyday life, then say where the analogy breaks down.
5. Work one concrete example step by step, with real numbers, objects or cases.
6. Name the most common misconception about this concept and correct it.
7. Ask one question that checks understanding rather than recall: the learner has to apply the idea to a new case.

Calibrate to the level:
- `child` (about 8 to 11): short sentences, everyday objects, no jargon, no formulas. About 150 to 250 words.
- `high-school`: plain language, each technical term defined, light algebra only if the subject needs it. About 300 to 450 words.
- `undergraduate`: standard terminology and notation, the formal definition, and how the concept connects to neighbouring ones. About 400 to 600 words.
- `expert`: skip the basics; give the precise statement, its assumptions, edge cases, limits of validity and the subtleties practitioners get wrong. As long as it needs to be, no longer.
</task>

<constraints>
- Simplify by omission, never by stating something false. When you leave out an important qualification, mark it: "(Simplified: …)".
- If $concept means different things in different fields and no subject was given, pick the most common meaning, say which one in the first line, and name the other.
- If the concept is not something you can explain accurately (unclear, very new or outside what you know), say so instead of guessing.
- Do not answer the check question.
</constraints>

<output_format>
Markdown with these headings, in order:
## In one sentence
## The idea
## Analogy
The analogy, then one line starting "Where it breaks:".
## Worked example
## Watch out for
The misconception and the correction.
## Check yourself
One question. Then the line "Reply with your answer and I'll tell you how you did."
</output_format>
