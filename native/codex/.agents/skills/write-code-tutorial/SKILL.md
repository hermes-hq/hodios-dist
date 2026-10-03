---
name: write-code-tutorial
description: Writes a technical tutorial a reader can follow end to end, with pinned prerequisites, complete runnable snippets and a checkpoint after every step. Use for docs, blog tutorials or workshop material.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: docs
  source: https://hermes-ide.com/prompts/write-code-tutorial
  catalog: 2026.1003.0
---

# Write a step-by-step code tutorial

## Inputs

- [TOPIC] (required): What the reader will build or learn, and any notes, existing code or outline to base it on.
- [READER_LEVEL] (optional; one of: beginner, intermediate, expert; default: intermediate): The reader's experience with the stack.
- [STACK] (optional): Language, framework and versions to use, for example "Python 3.12, FastAPI 0.115, SQLite".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A tutorial is learning by doing: the reader follows steps and ends with something that works. It fails when a snippet elides a line the reader needs, when versions drift and an API no longer exists, when a step depends on a file the text never created, or when the reader cannot tell whether they are still on track. A good tutorial shows the destination first, keeps the project runnable after every step, and gives the reader a checkpoint they can compare against.
</context>

<task>
Write a tutorial on: [TOPIC]
Reader level: [READER_LEVEL].
Only if [STACK] was provided: Stack: [STACK]. If no stack is given and the topic does not imply one, ask which to use before writing; if it is implied, state the stack and versions you chose.

1. Define the outcome in one or two sentences and show it (final output, screenshot description or a short demo of the finished program).
2. List prerequisites: tools with minimum versions, accounts or keys, and the knowledge you assume for this reader level. Show how to check each version.
3. Plan 5 to 10 steps. Each step adds one concept and leaves the project in a runnable state.
4. For each step:
   - a heading that says what the reader does;
   - why this step exists, in one or two sentences;
   - complete code with the file path above each block; when a file changes, show the whole file if it is short, or the full function with a clear "replace this function" instruction if long; never "..." inside code the reader must run;
   - the command to run;
   - a checkpoint: the exact output or behaviour to expect;
   - "If it does not work": the most likely mistake at this step and how to fix it.
5. End with the complete final code (or the file tree plus each file), what to try next, and links only to official documentation you are confident exists.
6. Adjust depth to the level: beginners get each command and term explained; experts get the reasoning and trade-offs and skip the basics.
</task>

<constraints>
- Use only APIs that exist in the stated versions. Where you are unsure an API or flag exists in that version, say so in the Author checklist rather than presenting it as certain.
- Pin versions in install commands. No secrets in code; read them from environment variables and show how to set them.
- Each concept is introduced before it is used. Do not add features the outcome does not need.
</constraints>

<output_format>
## Tutorial
The tutorial in Markdown: title, outcome, prerequisites, numbered steps as described, final code, next steps.
## Author checklist
Bullets for the author to verify before publishing: every API or version claim you are not certain of, every command to run end to end on a clean machine, and any screenshot to capture.
</output_format>
