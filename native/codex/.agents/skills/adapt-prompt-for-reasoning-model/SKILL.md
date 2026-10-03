---
name: adapt-prompt-for-reasoning-model
description: Rewrites a prompt for reasoning-capable models by removing step-by-step micromanagement, stating goals, constraints and success criteria, and keeping the output format exact.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/adapt-prompt-for-reasoning-model
  catalog: 2026.1003.2
---

# Adapt a prompt for a reasoning model

## Inputs

- [PROMPT] (required): The current prompt, including any system prompt, examples and output format, with placeholders kept as they are.
- [FAILURE_EXAMPLES] (optional): Optional: what goes wrong when you run it on a reasoning model, for example "ignores the JSON format", "overthinks simple cases", "prints its reasoning in the answer".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Prompts written for earlier chat models often compensate for weak reasoning: "think step by step", a rigid ten-step procedure, a scratchpad section to fill in, many few-shot examples showing the reasoning. Models that reason internally before answering are guided differently. Provider guidance for these models agrees on the main points: state the goal, the constraints and what success looks like, and let the model plan; prefer high-level instructions to think carefully over prescriptive steps; start zero-shot and add examples only if needed, keeping them consistent with the instructions; use delimiters for inputs; and be exact about the final output, since internal reasoning should not leak into a parsed answer. Hard rules (formats, policies, tool limits) still need stating explicitly; what goes is the micromanagement of how to think.
</context>

<task>
Adapt this prompt for a reasoning-capable model.

<prompt>
[PROMPT]
</prompt>
Only if [FAILURE_EXAMPLES] was provided: 
<failure_examples>
[FAILURE_EXAMPLES]
</failure_examples>

1. Work out the prompt's goal, inputs, deliverable and hard requirements. If the goal cannot be inferred, ask one question and stop.
2. Classify every instruction as one of:
   - goal or success criterion (keep, sharpen);
   - hard constraint: format, policy, length, tool or safety rule (keep, state once, clearly);
   - reasoning scaffolding: "think step by step", forced scratchpads, prescribed reasoning order, reasoning-heavy examples (remove or turn into a success criterion);
   - procedure that encodes real domain knowledge, such as a required check or a business rule (keep as a requirement, not as a thinking order);
   - filler or emphasis (remove).
3. Rewrite the prompt: context and goal first, then inputs in delimiters, constraints, explicit success criteria (what a correct answer must satisfy, how to handle ambiguity), and the exact output format with an instruction to return only the final answer in that format.
4. Address each failure example with a specific change.
5. Propose test inputs that compare old and new, including a simple case (to catch overthinking) and a hard one.
</task>

<constraints>
- Keep every placeholder, hard constraint, policy and output field exactly. Changing the output schema breaks whatever consumes it.
- Do not ask the model to show its reasoning in the final answer unless the original output requires an explanation for the user; then ask for a short justification, not the reasoning trace.
- Keep few-shot examples only if they show the output format or a subtle judgement that instructions cannot; trim their reasoning to the answer.
- Model-agnostic: no model names or vendor-only parameters in the prompt. Mention reasoning-effort or thinking-budget settings only as a note for the operator.
- The rewrite is usually shorter. Do not add new requirements.
- Do not claim the new prompt performs better; say how to test it.
</constraints>

<output_format>
## Diagnosis
A table: Instruction (quoted, shortened) | Type | Action (keep, rewrite, remove).
## Rewritten prompt
The full prompt in one fenced block.
## Changes
At most six bullets, most important first, each tied to a failure example where one applies.
## Kept on purpose
Bullets for procedures or examples kept, and why.
## Test it
Three test inputs, what to compare, and one note on reasoning-effort settings to try.
</output_format>
