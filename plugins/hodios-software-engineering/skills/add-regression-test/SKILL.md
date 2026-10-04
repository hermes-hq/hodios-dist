---
name: add-regression-test
description: Writes the smallest test that fails on the buggy code and passes with the fix, and proves both by running it. Use after fixing a bug, or before fixing one, so it cannot return.
license: CC0-1.0
arguments:
  - bug
  - fix
argument-hint: <bug> [fix]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: testing
  source: https://hermes-ide.com/prompts/add-regression-test
  catalog: 2026.1004.3
---

# Add a regression test for a bug

## Inputs

- `bug` (required): The bug, as an issue link or text, with the input that triggers it and the expected result.
- `fix` (optional): The commit, branch or diff that fixes it. Leave empty if the bug is not fixed yet.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A regression test is only worth its place in the suite if it fails without the fix. Many "regression tests" pass on the broken code too, because they test a neighbouring path or assert too little. The proof is running the test against both versions.
</context>

<task>
Add a regression test for: $bug
Only if fix was provided: The fix is in $fix.
1. State the bug as one triggering input and one expected result.
2. Find the lowest level where the bug can be observed (unit before integration before end-to-end), and the existing test file where a test for that code belongs.
3. Write one focused test with that input and the expected result. Name it after the behaviour, and reference the issue in a comment if there is one.
4. Prove it:
   - On the code without the fix, the test must fail, and fail for the right reason (the assertion on the bug, not an import or setup error). If the fix is already applied, revert it temporarily, for example with `git stash` or by checking out the parent commit of the fix in a separate worktree.
   - On the code with the fix, the test must pass.
   - If the bug is not fixed yet, the test fails now; report that and leave the fix to the user.
5. Run the surrounding test file or suite to confirm nothing else broke, and restore the work tree to the state you found it in.
</task>

<constraints>
- One bug, one test. Add a second test only for a distinct boundary of the same bug, and say why.
- Do not change production code, except to temporarily revert the fix during the proof.
- Never leave the work tree with the fix reverted or with stashed changes the user did not make.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
</constraints>

<output_format>
## Test
The file path and the test code as a diff.
## Proof
Two results with commands: without the fix (failing, with the assertion message) and with the fix (passing). If the bug is not fixed yet, the failing run only.
## Notes
Anything that limits the test, such as a bug that is only observable end to end, or "None".
</output_format>
