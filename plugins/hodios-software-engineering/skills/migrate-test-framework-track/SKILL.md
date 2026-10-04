---
name: migrate-test-framework-track
description: Moves a test suite between frameworks, such as Jest to Vitest or unittest to pytest, in batches with codemods, manual fixes, pass-count parity checks and CI updates. Use for any test framework switch.
license: CC0-1.0
arguments:
  - from_framework
  - to_framework
  - test_command
  - batch_size
argument-hint: <from_framework> <to_framework> <test_command> [batch_size]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: migration
  source: https://hermes-ide.com/prompts/migrate-test-framework-track
  catalog: 2026.1004.0
---

# Migrate a test suite to another framework

## Inputs

- `from_framework` (required): The framework the suite uses today, for example Jest, Mocha, Jasmine, unittest, nose or JUnit 4.
- `to_framework` (required): The framework to move to, for example Vitest, Node's built-in test runner, pytest or JUnit 5.
- `test_command` (required): The command that runs the whole suite today.
- `batch_size` (optional; default: 25): How many test files to migrate per batch after the first, smaller batch.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Migrates the test suite from $from_framework to $to_framework without losing a single test along the way. The danger in a framework switch is silent loss: a test file the new runner never picks up, a test that now passes because a mock no longer applies, an assertion that changed meaning. So the whole track is organised around parity: the same tests, found by name, with the same results, before the old framework is removed.

Rules for every step:
- Record per-file test counts (passed, failed, skipped) from real runs of both frameworks, and compare them by test name, not just totals. When conversion renames tests (unittest methods to pytest functions, nested describe blocks flattened), keep an old-name to new-name map so every test can still be matched.
- Never change production code to suit the new framework. If a test only passed because of old-framework behaviour (auto-mocking, global leakage, fake timers enabled by default), say so and fix the test setup, not the assertion.
- Keep both frameworks runnable side by side until cutover.
- If both arguments name the same framework at different versions, this is an upgrade, not a migration: say so, and follow the framework's official migration notes with one before-and-after run instead of this track.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.

## Steps

Work through these steps in order. Do not skip a gate.

1. inventory (discover)
2. first-batch (build)
3. remaining-batches (build)
4. cutover (ship)

### Step 1: Baseline and inventory

1. Run `$test_command` and save per-file and per-test results (use the old framework's JSON or JUnit XML reporter). This is the parity baseline. Note tests that already fail or are skipped; they must end in the same state, not silently disappear.
2. Inventory every $from_framework feature the suite relies on, with counts and example files: globals and imports, mocking (module mocks, auto-mocking, spies, manual mocks folders), fake timers, snapshots and their serializers, setup and teardown files, custom matchers, fixtures, parametrisation, test discovery patterns, environment (jsdom, node, browser), path aliases and transforms, coverage config, reporters, watch mode, IDE and CI integration.
3. Check whether $to_framework can run the existing tests largely unchanged (for example, pytest collects unittest and nose-style tests, and Vitest offers Jest-compatible globals and APIs). If it can, plan to switch the runner first, prove parity on the unchanged tests, and convert idioms in later batches; this is safer than rewriting and running at the same time.
4. For each feature, write the $to_framework equivalent and whether a codemod handles it. Use an established codemod when one exists for this pair; list what it does not cover. Mark features with no equivalent.
5. Find every place the old framework is wired in: package scripts or task runners, CI workflows, pre-commit hooks, editor configs, docs.

Write the artifact: Baseline (files, tests, passed, failed, skipped), Feature map (Feature | Uses | Equivalent | Codemod | Notes), Wiring, Risks. Continue to step 2.

Save this step's result to `test-migration/01-inventory.md`.

### Step 2: Set up and migrate a first batch

1. Install $to_framework and write its config so it mirrors the old behaviour: discovery patterns limited to migrated files, environment, aliases, setup files, coverage paths. Add a separate script to run it.
2. Pick a first batch of five to ten files that is representative: include the hardest features from the inventory (module mocks, timers, snapshots, custom matchers), not only the easy files.
3. Run the codemod on the batch, then fix by hand what it missed. Regenerate snapshots only after checking that the diff is formatting (serializer differences), never content; list every regenerated snapshot.
4. Run the batch under the new framework and compare per test with the baseline: every test present by name, same pass, fail or skip state. Explain each difference.
5. Remove the batch from the old framework's discovery so no file runs twice, and confirm the old suite still passes for the rest.

Write the artifact: Config decisions, Batch files, Manual fixes by pattern, Parity table (File | Old counts | New counts | Differences explained), Snapshot changes. Stop and wait for approval; the patterns approved here are reused for every later batch.

Save this step's result to `test-migration/02-first-batch.md`.

**Gate:** stop here and wait for the user's approval before step 3 (remaining-batches).

### Step 3: Migrate the rest in batches

1. Migrate the remaining files in batches of $batch_size, applying the codemod and the fix patterns approved in step 2.
2. After each batch, run the new suite and the remaining old suite, and check parity for the batch by test name. A test missing from the new run is a blocker, not a footnote.
3. When a file needs a new kind of manual fix not seen in step 2, apply it, record it, and continue; if it would change what a test asserts, stop and ask.
4. Keep a running parity tally: migrated files, tests matched, differences explained.

Continue to step 4 when every file is migrated and parity holds.

### Step 4: Cut over and report

1. Point the main test script, CI workflows, pre-commit hooks and coverage upload at $to_framework. Make sure CI still fails on test failure and still publishes results in the same format if anything consumes them.
2. Remove $from_framework dependencies, config, setup files and type definitions only after a full green run of the new suite with parity confirmed.
3. Run the full new suite twice (to catch order-dependence the new runner's parallelism exposes) and once with coverage. Compare coverage with the old baseline.
4. Update contributor docs where they mention how to run tests.

Write the report:

#### Parity
Old totals vs new totals, by state, and every per-test difference with its explanation.

#### Changes
Config, scripts, CI and docs changed, one line each.

#### Manual fix patterns
The patterns used, so the team can apply them to new tests.

#### Snapshots regenerated
List, with why each change is formatting only.

#### Follow-ups
Anything left, such as features without an equivalent or tests that were already failing.

Save this step's result to `test-migration/04-report.md`.
