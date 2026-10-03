---
name: compress-prompt
description: Shortens a long prompt while preserving its behaviour, maps every original instruction to where it now lives, reports the real size reduction and lists test inputs to check nothing changed.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/compress-prompt
  catalog: 2026.1003.1
---

# Compress a prompt

## Inputs

- [PROMPT] (required): The full prompt to shorten, including examples and placeholders.
- [TARGET_REDUCTION] (optional; default: 40%): How much shorter it should be, as a percentage or a word or token budget.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Long prompts cost tokens and latency, and they often bury their important instructions under repetition and filler. But a shorter prompt is only better if it behaves the same. Compression is safe when every behaviour of the original is listed first and checked off at the end, and when test inputs exist to compare the two versions.

<original_prompt>
[PROMPT]
</original_prompt>
Target reduction: [TARGET_REDUCTION]
</context>

<task>
1. Build a behaviour inventory: every distinct thing the prompt makes the model do or avoid (role, steps, rules, edge-case handling, output format, tone, examples and what each example teaches). Number them B1, B2 and so on.
2. Find what can go without changing behaviour: repetition, filler and politeness, emphasis words, explanations that do not change behaviour, instructions that restate model defaults, and examples that teach the same thing as another example.
3. Keep what carries behaviour: reasons that shape judgement in unforeseen cases, edge-case rules, the output format, placeholders, and examples that cover distinct cases.
4. Rewrite the prompt more tightly: merge overlapping rules, turn paragraphs into short lists where that is clearer, and keep the original order of priority.
5. Map each inventory item to where it now lives in the compressed prompt, or mark it as deliberately removed with the reason.
6. Estimate the size before and after in words and approximate tokens (roughly 1.3 tokens per English word), rounded and marked as estimates, and the reduction as a percentage. If the target cannot be met without losing behaviour, stop at the safe size and say which behaviours you would have to drop to go further.
7. Write five to eight test inputs that exercise the behaviours most at risk, each with the observable result both versions must produce.
</task>

<constraints>
- Preserve every placeholder, variable, delimiter tag name and required output field exactly.
- Never drop a safety, privacy or honesty instruction to save space.
- Do not change what the prompt does. Improvements you notice go in a separate "Possible improvements" line, not into the compressed prompt.
- You cannot run the tests. Present them for the user to run on both versions side by side.
</constraints>

<output_format>
## Behaviour inventory
Numbered list B1, B2...
## Compressed prompt
Fenced code block.
## Behaviour map
Table: Behaviour | Where it lives now (quote the phrase) or "removed: reason".
## What was cut
Bullets: what and why it was safe.
## Size
One line: "About N words (~T tokens) → about M words (~U tokens), about P% shorter." If the target was not met, one more line on what would have to go to reach it.
## Test inputs
Table: Input | Behaviours tested | Expected in both versions.
Possible improvements: one line, or "None".
</output_format>
