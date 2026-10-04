---
name: test-coverage-campaign-track
description: Raises test coverage where it reduces risk, measuring first, writing behaviour tests for risky untested code and checking them with sampled mutation testing. Use for a coverage push that must count.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: testing
  source: https://hermes-ide.com/prompts/test-coverage-campaign-track
  catalog: 2026.1004.0
---

# Raise meaningful test coverage across a codebase

## Inputs

- [COVERAGE_COMMAND] (required): The command that runs the tests with coverage, for example "npm test -- --coverage", "pytest --cov=src --cov-report=json" or "go test -coverprofile=cover.out ./...".
- [TARGET] (optional; default: risk-based): What success means. "risk-based" ranks untested code by risk; or give a goal such as "branch coverage of src/billing to 80%".
- [BUDGET_FILES] (optional; default: 15): The most test files the campaign may add or change before it stops and reports.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs a coverage campaign that buys real safety. Line coverage is easy to inflate with tests that execute code but assert nothing, and a campaign judged by percent drifts there. This track measures, picks the untested code where a bug would hurt most, writes tests that pin down behaviour, then checks a sample with mutation testing to prove the tests would catch a real change. Target: [TARGET].

Rules for every step:
- Every number in an artifact comes from a command actually run: `[COVERAGE_COMMAND]`, git history, or the mutation tool.
- Tests go through public behaviour (inputs, outputs, side effects at boundaries), not private helpers or call counts, unless the boundary itself is the behaviour.
- When a new test exposes a bug, do not write the test to expect the buggy result. Mark it as a known failure in the way the project allows (or leave it out), record the bug, and do not fix production code in this campaign unless the user asks.
- Stop and report before adding or changing more than [BUDGET_FILES] test files.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.

## Steps

Work through these steps in order. Do not skip a gate.

1. measure (discover)
2. risk-map (plan)
3. write-tests (build)
4. mutation-check (verify)
5. report (verify)

### Step 1: Measure

1. Run `[COVERAGE_COMMAND]` and record overall line and branch coverage, and coverage per file or package. If the suite fails, stop and report: a coverage campaign on a red suite measures nothing.
2. Gather risk signals for each source file with low coverage:
   - Churn: commits touching the file in the last six to twelve months (`git log --since=... --name-only`).
   - Bug history: commits or issues mentioning fix, bug or revert for that file.
   - Complexity: branch count or cyclomatic complexity from an existing tool, or a rough count of conditionals.
   - Criticality: money, auth, permissions, data deletion, external integrations, anything the README or architecture docs call core.
3. Note what the existing tests look like: framework, helpers, fixtures, factories, how external services are faked. New tests must match.

Write the artifact: Baseline (overall and per package), Risk table (File | Coverage | Churn | Bug fixes | Complexity | Criticality), Test conventions. Continue to step 2.

Save this step's result to `coverage-campaign/01-measure.md`.

### Step 2: Choose targets

1. Rank the files by risk: high criticality and churn with low branch coverage first. When [TARGET] names a path or a percentage, rank within it and compute how many uncovered branches the goal needs.
2. For the top targets, list the specific untested behaviours: the uncovered branches and what each one means in domain terms ("refund larger than the original charge", "expired token with a valid refresh token"), the error paths, and the boundary values.
3. Drop code that is not worth testing here (generated code, trivial getters, dead code, thin wrappers over a library) and say why. Dead code goes on the follow-up list rather than getting tests.
4. Fit the plan inside [BUDGET_FILES] test files.

Write the artifact: Targets (File | Behaviours to test | Why risky | Test file), Skipped and why, Expected coverage change. Stop and wait for approval.

Save this step's result to `coverage-campaign/02-targets.md`.

**Gate:** stop here and wait for the user's approval before step 3 (write-tests).

### Step 3: Write behaviour tests

For each approved target:

1. Write one test per behaviour, named for the behaviour in the project's style. Arrange the minimum setup with existing factories and fakes; assert on the observable outcome, including error types and messages where callers depend on them.
2. Cover the boundaries listed in step 2, not only the happy path.
3. Avoid assertion-free tests, snapshot tests of large structures that nobody reads, tests that assert mocks were called as a stand-in for outcomes, and sleeps.
4. Run the new tests and the surrounding suite. Each new test must pass for the right reason: temporarily break the behaviour (flip a condition locally, never committed) and confirm the test fails, at least for the riskiest ones.
5. Keep count of test files touched against [BUDGET_FILES].

Continue to step 4.

### Step 4: Check a sample with mutation testing

1. Use the project's mutation tool if it has one, or the standard tool for the stack (for example Stryker, mutmut, cosmic-ray, PIT, cargo-mutants or go-mutesting). If none can be run, apply five to ten manual mutations per sampled file (negate a condition, change a boundary, drop a statement, return early) and run the tests against each, reverting every one.
2. Limit the run to the target files so it finishes in reasonable time.
3. Triage surviving mutants: equivalent (no behaviour change, ignore), unimportant, or important. Strengthen or add tests for the important survivors and rerun.
4. Rerun `[COVERAGE_COMMAND]` for the final numbers.

Continue to step 5.

### Step 5: Report risk reduced

#### Behaviours now protected
Table: Target | Behaviours covered | Why it mattered.

#### Mutation check
Tool or manual method, files sampled, mutants killed / survived / equivalent, and what was strengthened.

#### Coverage
Before and after, overall and for the targets, from real runs. Present it after the behaviours, as supporting evidence.

#### Bugs found
Table: File and line | Behaviour | How the test shows it | Status.

#### Remaining risk
The next targets from the ranking, and anything skipped.

#### Checks
Commands run and real results.

Save this step's result to `coverage-campaign/05-report.md`.
