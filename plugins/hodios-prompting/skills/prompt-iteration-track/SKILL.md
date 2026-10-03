---
name: prompt-iteration-track
description: Improves a prompt in gated steps - define success, build test cases, run and grade, diagnose failures, revise, then compare versions on the same cases before adopting the change.
license: CC0-1.0
arguments:
  - prompt_or_task
  - sample_inputs
argument-hint: <prompt_or_task> [sample_inputs]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: prompt-engineering
  source: https://hermes-ide.com/prompts/prompt-iteration-track
  catalog: 2026.1003.0
---

# Prompt iteration track

## Inputs

- `prompt_or_task` (required): The current prompt to improve (with placeholders), or a description of the task if there is no prompt yet, plus who uses it and what goes wrong today.
- `sample_inputs` (optional): Optional: real inputs the prompt receives, and outputs you judged good or bad. Remove personal data first.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Improves a prompt the way a careful prompt engineer does: decide what success means, fix a test set, measure, diagnose, change one thing at a time, and adopt the new version only if it wins on the same cases without breaking others.

<prompt_or_task>
$prompt_or_task
</prompt_or_task>
Only if sample_inputs was provided: 
<sample_inputs>
$sample_inputs
</sample_inputs>

Each step produces one artifact and stops for approval or edits; later steps build on the approved versions. Keep every version of the prompt labelled (v1, v2…) and never edit a test case after seeing results, except to fix a case that was itself wrong, which you must say. Outputs are graded by running the prompt in the tool the person actually uses: either the person runs each case there and pastes the outputs, or, if they ask, you run the cases yourself in this conversation and say clearly that your own outputs may differ from the target tool's. Never report a result you did not see. If the person asks to skip the approvals, confirm once that later steps will build on unreviewed choices; if they agree, continue without stopping and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. success (plan)
2. cases (design)
3. run (verify)
4. diagnose (review)
5. revise (build)
6. compare (verify)

### Step 1: Define success

Decide what "better" means before changing a word of the prompt.

1. If there is no prompt yet, draft v1 from the task description in the usual structure (context, task, constraints, output format) and treat it as the baseline. If the task itself is unclear, ask up to three questions and stop.
2. Write down:
   - **Job:** one sentence: input, deliverable, who uses it.
   - **Requirements:** numbered R1, R2… covering format, length, content rules, tone, and what to do with missing, ambiguous or out-of-scope input. Mark each as a hard requirement (a failure is a failure) or a quality goal (graded).
   - **Current problems:** what goes wrong today, from the description and any bad sample outputs, each linked to a requirement.
   - **Done when:** the bar for adopting a new version, for example "passes every hard requirement on all cases and improves the quality score, with no previously passing case now failing".
   - **Run settings:** the tool or model tier, and whether to run each case once or several times (several when outputs vary a lot between runs).

Stop and wait for approval or edits before building test cases.

**Gate:** stop here and wait for the user's approval before step 2 (cases).

### Step 2: Build test cases

Fix the inputs every version will be judged on.

1. Write 8 to 15 cases: about half realistic happy-path inputs spread across the variety the prompt really sees, about a third edge cases (empty or very short input, very long input, ambiguous requests, unusual formatting, boundary values in any rule), and the rest negative cases (out of scope, missing information, input the prompt should decline or flag). Include at least one case for every current problem from Step 1.
2. Base cases on the sample inputs where given, varied rather than copied; mark synthetic ones. Use fictional names and data.
3. Write each input in full, exactly as it would be pasted, for every placeholder.
4. For each case give the requirements it tests, the expected behaviour, and a pass criterion that someone else would check the same way: exact value, contains or does-not-contain, a pattern, a word or item count, valid structure, or a one-sentence rubric.
5. Add a scoring sheet: one row per case with columns for each version.

Stop and wait for approval. Once approved, the cases are frozen.

**Gate:** stop here and wait for the user's approval before step 3 (run).

### Step 3: Run and grade the baseline

Measure v1 on the frozen cases.

1. Give the person a run sheet: the exact v1 prompt and each case's input ready to paste, and ask them to paste back the outputs labelled by case ID. If they asked you to run the cases yourself, do so here, one case at a time, and label the results as run in this conversation.
2. Grade each output against its pass criterion. Quote the part of the output that decides the grade. For rubric criteria, give a short reason; for hard requirements, a plain pass or fail.
3. Fill in the scoring sheet for v1: passes per case type (happy, edge, negative), hard-requirement failures, and the quality score if one was defined.
4. List the failing cases grouped by the requirement they break, and anything surprising in passing cases (for example a correct answer in the wrong format).

Do not diagnose or change the prompt yet. Stop and wait for approval of the grades; the person may disagree with a grade, and their judgement wins.

**Gate:** stop here and wait for the user's approval before step 4 (diagnose).

### Step 4: Diagnose failures

Find the cause of each failure in the prompt, not in the output.

1. For each group of failures, trace it to a cause in v1, quoting the line or naming the gap. Typical causes: the requirement is missing or implicit; it is buried or contradicted by another line; the output format is underspecified; there is no rule for missing or ambiguous input; an example teaches the wrong pattern; emphasis causes over-application; inputs are not separated from instructions; the task needs information the prompt does not provide.
2. Separate prompt problems from problems a prompt cannot fix (the model lacks the knowledge, the input lacks the information, the task needs a tool or a second step), and say which is which.
3. Propose one targeted fix per cause, the smallest change that should address it, and predict which cases it should flip and which passing cases it could put at risk.
4. Order the fixes by expected impact. Recommend applying them together only if they touch unrelated parts of the prompt; otherwise suggest which to try first.

Stop and wait for approval of the fixes to apply.

**Gate:** stop here and wait for the user's approval before step 5 (revise).

### Step 5: Revise

Write v2 with the approved fixes and nothing else.

1. Apply only the approved fixes. Keep every placeholder, every requirement that already passed, and the author's wording where it was not part of a problem.
2. Show v2 in full in one fenced block, ready to paste.
3. Show a change list: each change, the fix and cause it implements, and the cases it is meant to flip.
4. State the size change in words, and note anything removed and why.
5. Give the run sheet for v2: the same frozen cases, the same settings as v1.

Stop and wait for approval of v2, and for the v2 outputs (or a request that you run them yourself).

**Gate:** stop here and wait for the user's approval before step 6 (compare).

### Step 6: Compare and decide

Decide on evidence whether v2 replaces v1.

1. Grade the v2 outputs with the same criteria and the same strictness as in Step 3, quoting evidence.
2. Compare in a table: case ID | v1 | v2 | change (fixed, regressed, unchanged). Then totals per case type and hard-requirement failures for each version.
3. Read every regression: say whether it is a real regression, noise from a variable output (rerun that case before concluding), or a case whose criterion was wrong.
4. Decide against the "done when" bar from Step 1:
   - **Adopt v2** if it meets the bar.
   - **Iterate** if it improved but did not meet the bar: name the remaining failures and return to Step 4 with them.
   - **Keep v1** if v2 regressed on any negative case or hard requirement that v1 passed, or did not improve.
5. Hand over: the adopted prompt, the frozen test set and scoring sheet to rerun after any future change, and a one-line changelog entry for the version.

This is the last step.
