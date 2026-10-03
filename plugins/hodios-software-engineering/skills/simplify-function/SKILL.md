---
name: simplify-function
description: Rewrites a hard-to-follow function into a clearer one with identical behaviour, using guard clauses, named steps and simpler conditions, verified by tests. Use on long or deeply nested code.
license: CC0-1.0
arguments:
  - target
argument-hint: <target>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: refactoring
  source: https://hermes-ide.com/prompts/simplify-function
  catalog: 2026.1003.0
---

# Simplify a complex function

## Inputs

- `target` (required): The function or method to simplify, with its file.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A function is hard to change when a reader has to hold too much in mind at once: deep nesting, flags that switch behaviour, long stretches doing several jobs, conditions that need a truth table. Simplifying means removing that load while keeping every observable behaviour, including the odd edge cases callers may depend on.
</context>

<task>
Simplify $target.
1. Read the function and its callers. Write down its observable behaviour: return values, errors raised, side effects and their order, and edge cases (empty, null, boundaries).
2. Make sure tests pin that behaviour. If they do not, add focused tests for the uncovered paths first, and run them against the original code.
3. Name what makes it hard to read, specifically: nesting depth, a boolean flag argument, mixed levels of abstraction, duplicated branches, a variable reused for different meanings.
4. Apply the smallest set of changes that addresses those points. Typical moves:
   - guard clauses and early returns instead of nested conditions;
   - extract a well-named helper for each distinct step;
   - split a flag argument into two functions when the flag selects different behaviour;
   - simplify boolean expressions and name complex conditions;
   - replace a long if/else chain over one value with a lookup table, when that is clearer.
5. Run the tests after each change. Then measure the before and after: lines, maximum nesting depth and number of branches, by counting rather than estimating.
</task>

<constraints>
- Behaviour stays identical, including error types and messages, side-effect order and edge-case results. If you believe an edge case is a bug, keep it and report it.
- Do not change the function's signature or public name unless asked.
- Prefer clear over clever: no dense one-liners, no new abstractions with a single use.
- Match the surrounding code's style and idioms.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## What made it hard
Two to four bullets.
## Diff
The diff, including any tests added first.
## Behaviour check
The test command and result, and the tests added to pin behaviour.
## Before and after
A table: Metric | Before | After, for lines, maximum nesting depth and branches.
</output_format>
