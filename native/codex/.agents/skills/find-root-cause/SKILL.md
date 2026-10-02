---
name: find-root-cause
description: Reproduces a bug, tests ranked hypotheses with experiments, and fixes the root cause instead of the symptom. Use when something is broken and the reason is not obvious.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: debugging
  source: https://hermes-ide.com/prompts/find-root-cause
  catalog: 2026.1002.2
---

# Find the root cause of a bug

## Inputs

- [SYMPTOM] (required): What goes wrong, as observed. Include the error message, when it happens and what you expected instead.
- [EVIDENCE] (optional): Logs, stack traces, reproduction steps, and anything already tried or ruled out.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A fix that targets the symptom usually moves the bug instead of removing it: a null check where the null should never arrive, a retry around a race, a catch that hides the error. The root cause is the earliest point where the program's actual state diverges from what the code assumes. Debugging is finding that point with experiments, not guessing at it.
</context>

<task>
Find and fix the root cause of: [SYMPTOM]
Only if [EVIDENCE] was provided: 
Evidence so far:
[EVIDENCE]
1. **Reproduce.** Find the shortest reliable way to trigger the symptom, ideally a single command or a failing test. Record how often it fails. If you cannot reproduce it, say what you tried and what information would let you, then stop and ask.
2. **Collect facts.** Read the code on the failing path. Separate what you observed (outputs, logs, values) from what you assume.
3. **Hypothesise.** List two to five candidate causes. For each, state what you would expect to see if it were true and if it were false.
4. **Experiment.** Run the cheapest experiment that best separates the hypotheses: add a log or assertion, inspect a value, change one input, bisect the code path, the input data or the commit history. Change one thing at a time and record each result.
5. **Confirm.** You have the root cause when you can predict the failure, for example "with input X it fails; with Y it passes", and the prediction holds.
6. **Fix at the cause**, as the smallest correct change. Remove the temporary logs and assertions you added.
7. **Verify.** Run the reproduction again and the surrounding tests. Add a test that fails without the fix when the project has tests.
</task>

<constraints>
- Do not change code to "see if it helps" without a hypothesis that predicts the result.
- Do not stop at the first plausible explanation. Confirm it with an experiment whose result you predicted.
- Never fix the symptom by swallowing errors, adding retries or sleeps, or special-casing the failing input. If a symptom-level mitigation is needed urgently, label it as such and still name the root cause.
- If the cause is outside the code (configuration, data, environment, a dependency), say so and stop at a recommendation.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Reproduction
The command or steps, and the failure rate observed.
## Hypotheses
A table: Hypothesis | Experiment | Result | Verdict (confirmed, ruled out, open).
## Root cause
One paragraph: where the state first goes wrong (`path:line`), why, and how that produces the symptom.
## Fix
The diff, then one sentence on why it removes the cause.
## Verification
The commands you ran after the fix and their results, including the new test.
</output_format>
