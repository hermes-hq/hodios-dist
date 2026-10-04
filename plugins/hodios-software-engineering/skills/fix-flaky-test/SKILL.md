---
name: fix-flaky-test
description: Finds why a test passes and fails intermittently and fixes the cause instead of adding retries. Use when a test fails only sometimes, locally or in CI.
license: CC0-1.0
arguments:
  - test
  - failure_log
argument-hint: <test> [failure_log]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: testing
  source: https://hermes-ide.com/prompts/fix-flaky-test
  catalog: 2026.1004.3
---

# Fix a flaky test

## Inputs

- `test` (required): Test name, file or failing CI job to investigate.
- `failure_log` (optional): Output from a failing run, if you have one.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A flaky test passes and fails on the same code. Retries and longer timeouts hide the defect and teach the team to ignore red builds, so the goal is the cause, not a green run. Sometimes the flakiness is in the product code rather than the test, and then it is a real bug that users can hit.
</context>

<task>
Investigate $test.
Only if failure_log was provided: Start from this failing output:
$failure_log
1. Read the test, its fixtures and setup, and the code it exercises before running anything.
2. List the sources of nondeterminism you can see:
   - time: the current date or time, time zones, timers, timeouts that are too tight;
   - randomness: random data, unseeded generators, generated ids;
   - ordering: unordered collections, query results without ORDER BY, parallel tests, test order;
   - shared state: globals, singletons, caches, databases, files or ports used by other tests;
   - concurrency: unawaited promises, background work, sleeps used for synchronisation;
   - the outside world: network, external services, environment variables, locale.
3. Reproduce the failure: run the test repeatedly, in random order, in parallel, or alongside the tests that run before it in CI. Report how often it fails.
4. Fix the cause: wait on the condition instead of a duration, inject the clock or the seed, isolate the state, sort before comparing. If the race is in the product code, fix it there and say so.
5. Run the test enough times to show the failure is gone, using the same method that reproduced it.
</task>

<constraints>
- Never add retries, sleeps or longer timeouts as the fix.
- Never delete, skip or quarantine the test as the fix. If quarantine is needed while the fix lands, say so separately.
- If you cannot reproduce the failure, say so, report the most likely causes ranked with evidence, and do not claim a fix.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Cause
One paragraph: the nondeterminism and how it makes the test fail. Say whether it is in the test or in the product code.
## Fix
The diff, then one sentence on why it removes the cause.
## Evidence
Runs before and after, with the method used and failure counts (for example "7 of 200 failed before, 0 of 200 after").
</output_format>
