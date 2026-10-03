---
name: create-few-shot-examples
description: Builds a small set of diverse, representative few-shot examples for a task, including tricky and negative cases, balanced so the model learns the rule rather than copying surface patterns.
license: CC0-1.0
arguments:
  - task
  - count
  - format
argument-hint: <task> [count] [format]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/create-few-shot-examples
  catalog: 2026.1003.2
---

# Create few-shot examples

## Inputs

- `task` (required): The task the examples will teach, the input it receives, the expected output, and if possible a few real inputs.
- `count` (optional; default: 4): How many examples to write.
- `format` (optional): Optional - the output format each example must show, such as a label, JSON with given fields, or a short reply.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Few-shot examples are the strongest signal in a prompt: models copy what they see, including things the author did not intend, such as length, wording, label order or a habit of always answering. Good example sets are diverse, look like the real inputs, cover the hard boundary cases, show what to do when the answer is "none" or "not enough information", and use exactly the output format required.

<task_description>
$task
</task_description>
Number of examples: $count
Only if format was provided: 
Required output format: $format
</context>

<task>
1. If the task, its input or its expected output is unclear, ask up to three questions and stop. Ask for real sample inputs if none are given and the domain is specialised; otherwise write realistic ones and say they are synthetic.
2. List the dimensions along which real inputs vary (length, tone, language quality, category, ambiguity, missing fields) and the decision boundaries where mistakes are likely.
3. Plan $count examples so that together they cover the main categories, at least one tricky boundary case, and at least one negative case (none of the categories apply, or not enough information) when the task allows one. If $count is too few to cover the essentials, say what is left uncovered and suggest a number.
4. Write the examples: realistic inputs, and outputs in exactly the required format. Vary length and phrasing so no surface feature predicts the answer. Balance labels and shuffle their order.
5. Explain why each example is in the set and what it teaches.
6. Note risks: patterns the model might over-copy, and how to check that the examples help (run the prompt with and without them on held-out inputs).
</task>

<constraints>
- Examples must be correct. For tricky cases, give the reasoning in the "why" section, not inside the example output, unless the format includes reasoning.
- Never reuse the user's test or evaluation inputs as examples; that hides real performance.
- No real personal data. Use invented names and details.
- Wrap each example in <example> tags with <input> and <output> inside, so it can be pasted into any prompt.
</constraints>

<output_format>
## Coverage plan
Table: Example | Category or case | Dimension it covers.
## Examples
One fenced code block containing all examples, ready to paste.
## Why each is here
Numbered, one or two sentences each.
## Watch for
Bullets: over-copying risks, gaps, and how to test.
</output_format>
