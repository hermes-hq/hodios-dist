---
name: diagnose-prompt-failures
description: Diagnoses why a prompt produces bad answers from failing examples, traces each failure to a root cause, proposes targeted fixes and a quick regression test set.
license: CC0-1.0
arguments:
  - prompt
  - bad_outputs
  - expected
argument-hint: <prompt> <bad_outputs> [expected]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/diagnose-prompt-failures
  catalog: 2026.1003.2
---

# Diagnose prompt failures

## Inputs

- `prompt` (required): The full prompt as sent, including the system prompt and any examples.
- `bad_outputs` (required): The inputs that went wrong and the outputs the model gave, as many as you have.
- `expected` (optional): Optional - what a correct output would have been for those inputs, or the rule it broke.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
When a prompt misbehaves, people tend to rewrite it from scratch or pile on capital-letter warnings. Both make things worse: the rewrite breaks what used to work, and the warnings make the model overcorrect elsewhere. Debugging a prompt works like debugging code: look at the failures, form hypotheses, find the root cause, make the smallest change that addresses it, and check that nothing else broke.

<prompt_under_test>
$prompt
</prompt_under_test>
<bad_outputs>
$bad_outputs
</bad_outputs>
Only if expected was provided: 
<expected>
$expected
</expected>
</context>

<task>
1. Describe each failure precisely: what was expected, what happened, and the exact part of the output that is wrong. If no expectation is given and it is not obvious, infer it and say so.
2. Group failures into patterns.
3. For each pattern, test these causes against the evidence and name the most likely root cause:
   - The instruction is missing, ambiguous, or only implied.
   - Instructions conflict, or one buried late or deep is outweighed by an earlier one.
   - Examples are being copied (length, wording, labels) or do not cover the failing case.
   - Input is not delimited, so the model treats data as instructions or mixes it into the answer.
   - The output format is underspecified, or the reasoning and the final answer are mixed.
   - Missing context or knowledge, so the model fills gaps by guessing.
   - Too many jobs in one prompt.
   - Not a prompt problem: a capability limit (exact counting, long arithmetic, very long inputs), missing retrieval or tools, settings such as temperature or maximum length, or the pipeline around the model.
4. Propose the smallest targeted fix for each root cause, show it as a before and after, and say which failures it should fix and what it might break.
5. Give the revised prompt with all fixes applied and nothing else changed.
6. Build a quick test set: every failing input, three to five inputs that worked before (to catch regressions), and two new edge cases, each with a pass condition that can be checked.
</task>

<constraints>
- Base every diagnosis on evidence in the outputs or the prompt. If the evidence is too thin to tell causes apart, say so and propose a small experiment that would (for example, remove the examples and rerun).
- Prefer explaining the reason behind a rule over adding emphasis.
- Do not claim a fix works; you cannot run it. Say what result would confirm it.
- If a cause is outside the prompt, say so plainly and recommend the right fix (a tool, retrieval, validation code, a setting) rather than more instructions.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Failure patterns
Table: Failure | Expected | Got | Pattern.
## Root causes
One short paragraph per pattern with the evidence.
## Fixes
Numbered. Each: Before, After, Fixes which failures, Risk.
## Revised prompt
Fenced code block.
## Test set
Table: Input | Why it is in the set | Pass condition.
## If this does not fix it
The next hypothesis to test, and how.
</output_format>
