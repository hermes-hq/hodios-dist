---
name: write-unit-tests
description: Writes unit tests that pin a unit's behaviour, covering boundaries, errors and edge inputs in the project's own test style, and proves each test can fail. Use for new or untested code.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: testing
  source: https://hermes-ide.com/prompts/write-unit-tests
  catalog: 2026.1004.3
---

# Write unit tests

## Inputs

- [TARGET] (required): The file, module, class or function to test.
- [FRAMEWORK] (optional): Test framework to use. Leave empty to use the one the project already uses.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Good unit tests describe what a unit does, not how it does it. They fail when behaviour breaks and keep passing through refactors. Tests that mirror the implementation, mock everything, or assert only that no exception was thrown add maintenance cost without catching bugs.
</context>

<task>
Write unit tests for [TARGET].
Only if [FRAMEWORK] was provided: Use [FRAMEWORK].
1. Read the target and its callers to learn its contract: inputs, outputs, side effects, errors. Read two or three existing test files to learn the project's conventions (framework, file location, naming, fixtures, assertion style) and follow them.
2. List the behaviours to cover before writing any test:
   - the main cases;
   - boundaries: empty, one element, maximum, zero, negative, off-by-one limits;
   - invalid input and every error path the code defines;
   - inputs that often break code: null or missing values, duplicates, Unicode, very large values, time zones and dates, floating-point amounts.
3. Write one test per behaviour, through the unit's public interface. Name each test after the behaviour (`returns empty list when no orders match`), not after the method.
4. Use fakes or mocks only at real boundaries: network, clock, file system, randomness, other services. Do not mock the code under test or plain data objects.
5. Run the tests. For each new test, confirm it can fail: break the behaviour temporarily or invert the assertion, watch it fail, then restore it.
</task>

<constraints>
- Do not change production code. If the code is hard to test, or you find a bug, report it under "Not covered" with the failing input and leave the code alone.
- Each test asserts specific values, not only that something is truthy or that no error was thrown.
- Keep tests independent: no shared mutable state and no dependence on run order.
- No snapshot tests unless the project already uses them for this kind of output.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Behaviours
A table: Behaviour | Test name | Kind (main, boundary, error, edge).
## Tests
The new or changed test files as a diff.
## Run
The command you ran and its result, plus how you confirmed the tests can fail.
## Not covered
Behaviours you did not test and why, and any bugs found (input, expected, actual). Or "None".
</output_format>
