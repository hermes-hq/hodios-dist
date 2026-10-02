---
description: Finds untested behaviour that matters most, ranked by risk rather than coverage percentage, and writes tests for the top gaps. Use when a module feels under-tested or before a risky change.
---

# Find and fill the riskiest test gaps

## Inputs

- [SCOPE] (required): The module, directory or feature to examine.
- [COVERAGE_REPORT] (optional): Output of a coverage tool for this scope, if you have one.
- [MAX_TESTS] (optional; default: 5): The most gaps to fill with tests in this run; the rest are listed only.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
Coverage percentage measures which lines ran, not which behaviours are checked. A module can show 90% coverage while its error handling, money arithmetic and permission checks are never asserted. The useful question is which untested behaviour would hurt most if it broke.
</context>

<task>
Find the riskiest test gaps in [SCOPE] and fill up to [MAX_TESTS] of them.
Only if [COVERAGE_REPORT] was provided: 
Coverage data:
[COVERAGE_REPORT]
1. Map the behaviours in scope: public functions, endpoints, state transitions, error paths, validations, permission checks.
2. Map the existing tests to those behaviours. A behaviour counts as covered only if a test asserts its result. Lines that merely run do not count.
3. Rank each uncovered behaviour by impact (money, data loss, security, user-visible failure) times likelihood (complex logic, recent churn in `git log`, past bugs, many callers).
4. Write tests for the top [MAX_TESTS] gaps, following the project's existing test conventions. Each test must assert a specific result.
5. Run them. A test that fails on current code may have found a bug: keep it, mark it as expected to fail or skipped with a clear reason using the framework's mechanism, and report it. Do not change production code.
</task>

<constraints>
- Rank by risk, not by how easy a test is to write.
- Do not write tests whose only purpose is to raise coverage, such as tests that call code without asserting a result, or tests of trivial getters.
- Cite `path:line` for every gap.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Gaps
A table, highest risk first: # | Behaviour | Where | Why it is risky | Filled (yes or no).
## Tests
The new tests as a diff.
## Run
The command and its result. List any test that exposed a bug, with input, expected and actual.
## Remaining gaps
The gaps you did not fill, one line each, or "None".
</output_format>

Arguments: $ARGUMENTS
