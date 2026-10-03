---
name: write-agent-handoff
description: Writes a self-contained handoff note so a fresh agent or a teammate can continue the current task without the conversation history. Use before ending a long session, switching tools or delegating.
license: CC0-1.0
arguments:
  - reader
  - focus
argument-hint: "[reader] [focus]"
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: meta
  source: https://hermes-ide.com/prompts/write-agent-handoff
  catalog: 2026.1003.1
---

# Write an agent handoff

## Inputs

- `reader` (optional; default: a fresh agent with no memory of this session): Who picks up the work.
- `focus` (optional): Anything the handoff must stress, such as a deadline or a decision still pending.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
The next reader has none of this session's context: not the conversation, not the files you read, not the dead ends you already ruled out. A handoff fails when it says "as discussed", when it reports work as done that was never verified, or when it leaves out the approaches that did not work, so the next agent repeats them. It should let $reader start working within a minute.
</context>

<task>
Write a handoff for the task in this session.
Only if focus was provided: 
Stress this: $focus

1. Check the actual state before writing: `git status`, the current branch, uncommitted changes, and the last commands and test results in this session. Do not rely on memory of what you intended to do.
2. Separate what is done and verified (with the evidence), what is done but unverified, and what is in progress (the exact point where work stopped).
3. Write the next steps as concrete, ordered actions with file paths and commands, so they can be executed without interpretation.
4. Record decisions with their reasons, and the approaches that were tried and rejected, with why.
5. Note gotchas: environment quirks, flaky tests, commands that need special flags, files not to touch, constraints the user gave.
</task>

<constraints>
- Self-contained: no "as discussed", "the earlier approach" or references to messages the reader cannot see. Name files, functions, branches and commands explicitly.
- Never mark something verified unless a command in this session showed it. Say "not verified" plainly.
- Include the user's explicit instructions and preferences that still apply, quoted briefly.
- Never include secrets, tokens, passwords or personal data, even if they appeared in the session. Refer to where they are stored instead.
- Keep it under about 600 words; link to files for detail instead of pasting them.
</constraints>

<output_format>
A Markdown note with a one-line title, then:
## Goal
What the task is and what done looks like.
## State
Three lists: Done and verified (with evidence) / Done, not verified / In progress (where it stopped).
## Next steps
Numbered, concrete actions.
## Decisions
Decision and reason; rejected approaches and why.
## Gotchas
Bullets.
## Verify
Commands that prove the task is complete.
## Open questions
For the user, or "None".
</output_format>
