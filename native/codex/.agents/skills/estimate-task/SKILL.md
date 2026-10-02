---
name: estimate-task
description: Estimates a software task as a range with a three-point breakdown, the assumptions behind it and the unknowns that drive the spread. Use when someone asks how long a piece of work will take.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: planning
  source: https://hermes-ide.com/prompts/estimate-task
  catalog: 2026.1002.1
---

# Estimate a task

## Inputs

- [TASK] (required): The task or ticket to estimate, with acceptance criteria if there are any.
- [CONTEXT] (optional): Who does the work, how well they know the codebase, the tech involved, and similar past work with its actual duration.
- [UNIT] (optional; one of: hours, days, points; default: days): Unit for the estimate.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A single-number estimate hides the information people need to plan: how uncertain it is and why. A three-point estimate per part (optimistic, most likely, pessimistic) makes the uncertainty visible, and naming the unknowns tells the team what to investigate to narrow it.
</context>

<task>
Estimate: [TASK]
Only if [CONTEXT] was provided: 
Context:
[CONTEXT]
Unit: [UNIT].

1. Break the task into parts small enough to reason about, including the work people forget: reading existing code, tests, code review rounds, data migration, documentation, deployment and verification in a real environment.
2. For each part, give optimistic, most likely and pessimistic values in [UNIT].
3. Compute the expected value per part as (optimistic + 4 × most likely + pessimistic) / 6 and sum them. Report the total as a likely value with a range from the summed optimistic to the summed pessimistic values. Show the arithmetic.
4. State the assumptions the numbers rest on.
5. Name the unknowns that widen the range most, and for each the cheapest way to shrink it (a question to ask, code to read, a short spike).
6. Give a confidence level (low, medium or high) with one reason.
</task>

<constraints>
- Never give a single number without a range.
- Do not pad silently. If you add buffer, show it as its own line with a reason.
- For points, estimate relative to a reference task from the context. If there is none, say that points cannot be calibrated and give days as well.
- If the task is too vague for a meaningful range, say so, give the questions that would make it estimable, and give a rough order of magnitude only.
- An estimate is not a commitment; do not phrase it as one.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Estimate
One line: likely X [UNIT], range A to B [UNIT], confidence level.
## Breakdown
Table: part, optimistic, most likely, pessimistic, expected, notes. Then the totals with the arithmetic.
## Assumptions
Bullets.
## Biggest unknowns
Bullets: unknown — effect on the range — how to shrink it.
## Not included
Bullets.
</output_format>
