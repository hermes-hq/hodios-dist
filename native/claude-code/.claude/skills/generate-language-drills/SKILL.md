---
name: generate-language-drills
description: Generates a mixed set of cloze, transformation and translation drills for one grammar point, graded by level, with an answer key. Use to practise a rule after learning it.
license: CC0-1.0
arguments:
  - grammar_point
  - target_language
  - level
  - count
  - native_language
argument-hint: <grammar_point> <target_language> [level] [count] [native_language]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: language-learning
  source: https://hermes-ide.com/prompts/generate-language-drills
  catalog: 2026.1004.3
---

# Generate grammar drills

## Inputs

- `grammar_point` (required): The grammar point to drill (for example "passé composé with être", "Russian genitive plural").
- `target_language` (required): Language being practised.
- `level` (optional; one of: A1, A2, B1, B2, C1, C2; default: B1): Learner's CEFR level; controls vocabulary and sentence complexity.
- `count` (optional; default: 15): Total number of drill items.
- `native_language` (optional; default: English): Learner's first language; used for the translation items and the instructions.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You write practice material for learners of $target_language. Good drills move from controlled to freer use, test only the target point, and include a few items where the point does not apply, because knowing when not to use a form is half of learning it. Items with two defensible answers, obscure vocabulary or the same sentence frame repeated teach very little.

Grammar point: $grammar_point
Learner level (CEFR): $level
Number of items: $count
Learner's first language: $native_language
</context>

<task>
1. State in one line how you are interpreting the grammar point. If the name could mean several things, choose the use most relevant at $level.
2. Split the $count items into three parts, in this order:
   - Part A, cloze (about 40%): a sentence with one gap and the base form in brackets.
   - Part B, transformation (about 30%): rewrite a sentence following an instruction (change the tense, make it negative, combine two sentences, replace the noun with a pronoun).
   - Part C, translation from $native_language (about 30%): short sentences that force the target structure.
3. Make about one item in five a contrast item, where a neighbouring form is correct instead. Do not label which ones.
4. Vary the vocabulary, subjects and contexts; keep all vocabulary at or below $level.
5. Write the answer key: the answer, any accepted alternatives, and a reason of at most 12 words for each item.
</task>

<constraints>
- Each item must have one correct answer, or every accepted alternative must be listed in the key.
- Sentences must be natural and plausible; no trick questions and no rare exceptions unless the level is C1–C2.
- Instructions for each part are in $native_language and one line long.
- Check every answer against the rule before writing the key. If a sentence turns out ambiguous, rewrite it.
</constraints>

<output_format>
Interpretation: one line.
## Part A
Instruction, then numbered items.
## Part B
Instruction, then numbered items continuing the numbering.
## Part C
Instruction, then numbered items continuing the numbering.
## Answer key
Numbered: answer · alternatives if any · reason.
</output_format>
