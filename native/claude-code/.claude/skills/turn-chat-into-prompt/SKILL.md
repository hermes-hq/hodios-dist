---
name: turn-chat-into-prompt
description: Turns a successful chat conversation into a reusable prompt with named variables, the rules learned from your corrections, an output format and a worked example. Use for tasks you repeat with AI.
license: CC0-1.0
arguments:
  - conversation
argument-hint: <conversation>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/turn-chat-into-prompt
  catalog: 2026.1003.1
---

# Turn a chat into a reusable prompt

## Inputs

- `conversation` (required): The full chat that eventually got you the result you wanted, including your first request, the corrections you made and the final answer you were happy with.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
When a chat finally produces what you wanted, the valuable part is usually not the first request but the corrections: "shorter", "no bullet points", "use our product name, not the code name", "always include the price". Those corrections are the hidden requirements. A reusable prompt captures them up front so next time the first answer is already right, and turns the parts that change each time into named variables.

<conversation>
$conversation
</conversation>
</context>

<task>
1. Identify the repeatable task in one sentence, and the final answer the user accepted (usually the last one before they stopped correcting or said thanks). If the user never seemed satisfied, or the conversation contains several unrelated tasks, say so and ask which one to capture.
2. Mine the corrections. List every instruction the user gave after the first request: explicit corrections, rejected drafts and what replaced them, preferences revealed by the user's edits. Turn each into a positive, general rule ("Keep it under 120 words" rather than "not so long"). Drop corrections that only applied to that one instance.
3. Separate what changes from what stays: the specific inputs of this instance (a product name, a client, a draft, a date) become variables with snake_case names, a one-line description and a sensible default where one exists. Everything stable becomes instructions.
4. Write the reusable prompt, model-agnostic, in this structure: a short role and context, the task, each variable in its own labelled block holding an upper-case bracketed placeholder that matches its name (the variable product_notes becomes a product notes block containing [PRODUCT_NOTES]), the rules learned, the output format taken from the accepted answer's shape, and an instruction to ask for missing information rather than invent it.
5. Build one example from the accepted answer, shortened if long, with any private details replaced by realistic placeholders. Label it as an example of format and quality, not content to copy.
6. Suggest how to test it: two or three new inputs to run it on, including one tricky case, and what a good answer must contain.
</task>

<constraints>
- Every rule in the prompt must trace to something in the conversation or be marked "(added)" with a reason. Do not invent preferences.
- Remove personal data, credentials, customer names and confidential numbers from the prompt and example; replace them with placeholders and list what you removed.
- Keep the prompt under about 500 words; if the task needs more, say what could move into a separate reference document.
- Write instructions as what to do, not long lists of what to avoid; keep a "do not" only where the conversation shows the model kept doing it.
- Do not use tricks tied to one model or vendor.
</constraints>

<output_format>
## What the task is
One sentence, plus which answer you treated as the accepted one.
## What the corrections taught
A table: Correction in the chat | Rule in the prompt.
## Variables
A table: Name | Description | Default.
## Reusable prompt
The full prompt in one fenced code block, ready to copy.
## Example
The example input and output, fenced, labelled.
## How to test it
Numbered test inputs with what a good answer contains. Then a line listing anything removed for privacy.
</output_format>
