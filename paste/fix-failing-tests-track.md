Gets the suite run by `[TEST_COMMAND]` back to green without cheating. A red suite after an upgrade or merge usually holds a handful of root causes behind dozens of failures, plus a few failures that were already there or are flaky. This track finds those causes, fixes the code where the code is wrong, updates a test only when the intended behaviour really changed (and says why), and reports whatever it could not fix.

Rules for every step:
- Work from real command output only. Never report a test as passing, a cause as proven or a count without having run the command that shows it.
- Fix behaviour, not tests. A test may change only when you can point to the intended behaviour change: an upgrade note, a changelog entry, a commit message, a spec or a decision the user approved.
- Stay inside [SCOPE] when it is given, and stop and report before the run changes more than 20 files in total.
- Write artifacts to the paths listed, outside version control unless the user wants them kept. Commit nothing unless the user asked for commits.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.

## Steps

Work through these steps in order. Do not skip a gate.

1. triage (verify)
2. diagnose (plan)
3. fix (build)
4. verify (verify)

### Step 1: Run and cluster the failures

<recent_change>
[RECENT_CHANGE]
</recent_change>

1. Check the environment before the code: dependencies installed from the lockfile, the runtime version the project pins, caches cleared if the upgrade touched build tooling. Many "test failures" after an upgrade are a stale install.
2. Run `[TEST_COMMAND]` once on the whole suite (or on [SCOPE] when given) and save the raw output. Record total, passed, failed, errored and skipped.
3. Group the failures into clusters that share a cause signature: the same error message or exception type, the same failing import or fixture, the same module under test, the same assertion shape. Name each cluster by its signature, not by a guess at the cause.
4. Rerun each failing test, or one representative per cluster, in isolation three times. A test that passes sometimes is flaky: list it separately and leave it for `fix-flaky-test` style work rather than this run.
5. If the recent change is known, check whether the cluster also fails on the commit before it (for example in a separate worktree checked out at that commit, or with `git bisect` over a small range). Mark clusters that already failed before as pre-existing.

Write the artifact with sections Environment, Baseline counts, Clusters (Cluster | Signature | Tests | Isolated result | New or pre-existing), Flaky. Continue to step 2.

Save this step's result to `fix-failing-tests/01-triage.md`.

### Step 2: Prove root causes and plan the fixes

For each cluster from step 1, largest first:

1. Read the failing test, the code it exercises and the part of the recent change that touches either. Find the line where expected and actual first diverge.
2. Classify the cause, with the evidence that proves it:
   - **Code regression**: the code no longer does what the test rightly expects.
   - **Intended behaviour change**: the upgrade or merge deliberately changed behaviour, and the test still expects the old one. Cite the upgrade note, changelog or commit.
   - **Test infrastructure**: a fixture, mock, config or helper broke (renamed API in the test framework, changed default, removed global).
   - **Environment**: versions, missing services, time zone, locale, file paths.
   - **Unknown**: you could not prove it. Say what experiment would settle it.
3. Propose the smallest fix for each cluster and list the files it touches. Prefer one fix at the shared cause over many edits at the symptoms.
4. Count the files the whole plan touches.

Write the artifact with a table: Cluster | Cause class | Evidence | Proposed fix | Files | Test changes and justification. Stop and wait for approval. Approval is essential when the plan changes any test's expectations, touches more than five files, or exceeds the 20-file budget; mark those rows clearly.

Save this step's result to `fix-failing-tests/02-diagnosis.md`.

**Gate:** stop here and wait for the user's approval before step 3 (fix).

### Step 3: Fix, one cluster at a time

Work through the approved plan in order.

1. Apply the fix for one cluster. Keep the change minimal and in the style of the surrounding code.
2. Run that cluster's tests, then the tests of the touched modules. Record the real result.
3. If the fix does not turn the cluster green, or turns something else red, revert it, go back to diagnosis for that cluster, and do not pile a second guess on top of the first.
4. Change a test only where the approved plan says the intended behaviour changed. Update the expectation to the new intended behaviour, keep the assertion as strict as before, and add a one-line comment or commit message citing the reason. Never loosen an assertion, add a broad try/except, mark a test skip or xfail, or special-case a test input to get green.
5. Keep a running count of files changed. If the next fix would take the run past 20 files, or past the plan's file list by more than a file or two, stop and report instead.

Continue to step 4 when every planned cluster is fixed or explained.

### Step 4: Verify the whole suite and report

1. Run `[TEST_COMMAND]` on the full suite (or [SCOPE]) and compare with the step 1 baseline: no test that passed before may fail now, and the skipped count must not have grown.
2. Run the project's linter or type checker if it has one, since fixes can break them.
3. Write the report:

#### Result
Before and after counts from real runs, and the commands used.

#### Fixed
Table: Cluster | Cause | Fix | Files.

#### Tests changed
Table: Test | Old expectation | New expectation | Justification (cite the source).

#### Still failing
Table: Test or cluster | What is known | Next experiment | Why it was not fixed (unknown cause, out of scope, budget reached, needs a decision).

#### Flaky and pre-existing
The tests from step 1 that were left alone, and why.

#### Follow-ups
One line each for anything noticed but not changed.

Save this step's result to `fix-failing-tests/04-report.md`.
