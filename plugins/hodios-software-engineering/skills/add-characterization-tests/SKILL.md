---
name: add-characterization-tests
description: Pins down what untested legacy code does today with characterization and golden-master tests, bugs included, so it can be changed safely. Use before refactoring or modifying code with no tests.
license: CC0-1.0
arguments:
  - code
  - entry_points
argument-hint: <code> [entry_points]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: testing
  source: https://hermes-ide.com/prompts/add-characterization-tests
  catalog: 2026.1002.1
---

# Add characterization tests to legacy code

## Inputs

- `code` (required): The legacy code to pin down, pasted or as a path.
- `entry_points` (optional): Functions, endpoints, commands or jobs through which the code is used, if you know them.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A characterization test records what the code actually does, not what it should do. It is a safety net for a later change: if a refactor alters any output, a test fails. That means the tests must pin current behaviour exactly, including odd and probably wrong behaviour, and must fail when the behaviour changes. Tests that only check "no exception" or that assert what the author guessed the code does give false confidence.
</context>

<task>
Write characterization tests for:
$code
Only if entry_points was provided: Known entry points: $entry_points

1. Find the entry points (from the list above, or from callers in the repository) and test through the highest-level one that is practical to call. Avoid testing private helpers that a refactor will move.
2. Find the seams that make the code nondeterministic or hard to call: current time, randomness, generated ids, environment, file system, network, database, global state. For each, choose the least invasive way to control it: an existing parameter or injection point first, then a test double at the module boundary, then a minimal seam (extract a parameter with the current value as its default). Name any production change you need; keep it behaviour-preserving.
3. Choose inputs that exercise every branch you can see: typical values, boundaries, empty and missing values, error paths, and combinations of flags. Read the conditionals to derive them.
4. Capture current outputs:
   - for small outputs, assert exact values;
   - for large or structured outputs (reports, HTML, JSON, files), write a golden-master or approval test that stores the output in a snapshot file, with scrubbers that normalise timestamps, ids and unordered collections so the snapshot is stable;
   - record side effects too: calls to collaborators, rows written, messages sent, exceptions raised.
   Derive expected values by running the code where you can. If you cannot run it, derive them by tracing the code and mark those tests "traced, confirm on first run".
5. Check the net catches change: for each important branch, describe a small mutation (flip a comparison, drop a line) and confirm a test would fail. Add inputs where none would.
</task>

<constraints>
- Do not fix bugs. Pin the current behaviour and list it under "Suspicious behaviour", with the test name, so a human decides later.
- Do not refactor production code beyond the minimal seams named in step 2.
- Name tests by behaviour (`returns_zero_discount_when_cart_empty`), not by number.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
</constraints>

<output_format>
## Behaviour inventory
Table: Entry point | Input class | Current output or side effect.
## Seams
Bullets: the nondeterminism or dependency, and how the tests control it (including any production change).
## Tests
The complete test file or files, with snapshot files if any.
## Suspicious behaviour
Table: Behaviour | Test that pins it | Why it looks wrong. Or "None".
## Coverage and gaps
Branches covered, branches not covered and why, and the mutations you checked.
</output_format>
