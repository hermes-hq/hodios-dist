---
name: improve-prompt
description: Diagnoses why a prompt gives weak or inconsistent results and rewrites it with clear context, task, constraints and output format while keeping its intent. Use on any prompt for any AI assistant.
license: CC0-1.0
arguments:
  - prompt
  - problem
  - target
argument-hint: <prompt> [problem] [target]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/improve-prompt
  catalog: 2026.1003.0
---

# Improve a prompt

## Inputs

- `prompt` (required): The prompt to improve, including any system prompt and example inputs.
- `problem` (optional): What goes wrong today (for example "ignores the word limit" or "invents sources"), and what a good output looks like.
- `target` (optional; default: any modern AI assistant): Where the prompt runs, such as a chat assistant, a coding agent, an API call or an automation.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most weak prompts fail for a few reasons that current guidance from the major model providers agrees on: the task is implicit, the context the model needs (audience, purpose, what good looks like) is missing, instructions conflict or are buried, the output format is undefined, inputs are not separated from instructions, and there are no examples where the format is subtle. Modern models follow instructions literally, so vague requests get generic answers. Shouting (ALL CAPS, "CRITICAL", "NEVER EVER") now tends to cause over-application rather than compliance. A better prompt is usually clearer and more specific, not longer.
</context>

<task>
Improve this prompt for $target:
<prompt>
$prompt
</prompt>
Only if problem was provided: 
What goes wrong today: $problem

1. Work out the prompt's intent: the task, the audience of the output and what a good result looks like. If the intent is ambiguous in a way that changes the rewrite, list the question and state the reading you chose.
2. Diagnose it against this checklist, citing the exact phrase for each problem:
   - task stated explicitly, as an action and a deliverable;
   - context: why, for whom, and what the model must know;
   - success criteria and a definition of done;
   - output format, length and structure;
   - constraints phrased as what to do, with the reason when it is not obvious;
   - conflicting, duplicated or buried instructions;
   - variable inputs separated from instructions (delimiters or tags) and placeholders kept;
   - examples, when the format or tone is hard to describe, varied enough not to be copied literally;
   - guardrails for facts: what to do when information is missing instead of guessing;
   - filler, vague role-play ("you are a world-class expert") and emphasis that does not change behaviour.
3. Rewrite the prompt: keep every requirement and placeholder the author had, fix each diagnosed problem, and order it as context, task, constraints, output format, then examples.
4. Propose two or three test inputs, including one edge case, that would show whether the new version beats the old one.
</task>

<constraints>
- Keep the author's intent, scope and placeholders exactly; do not add features, tools or requirements they did not ask for. Put suggestions for extra scope under What changed, labelled as optional.
- Make the prompt as short as it can be while still complete. Do not pad it with generic advice.
- Stay model-agnostic unless the target names a specific tool; then use that tool's conventions only where they matter.
- Do not claim the new prompt will perform better; say how to test it.
</constraints>

<output_format>
## Diagnosis
A table: problem | evidence (quoted phrase) | fix.
## Improved prompt
The full rewritten prompt in one fenced block, ready to paste.
## What changed
At most six bullets, most important first.
## Test it
Two or three test inputs and what a good output should do for each.
</output_format>
