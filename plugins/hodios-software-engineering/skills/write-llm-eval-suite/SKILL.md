---
name: write-llm-eval-suite
description: Writes an eval set for an LLM feature with golden, edge and adversarial cases, graders matched to each criterion, and pass thresholds. Use before shipping or changing a model, prompt or pipeline.
license: CC0-1.0
arguments:
  - feature
  - sample_inputs
  - grader
argument-hint: <feature> [sample_inputs] [grader]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: ai-ml
  source: https://hermes-ide.com/prompts/write-llm-eval-suite
  catalog: 2026.1004.2
---

# Write an eval suite for an LLM feature

## Inputs

- `feature` (required): What the LLM feature does, who uses it, what a good output looks like, and what it must never do.
- `sample_inputs` (optional): Real or realistic inputs the feature receives, with good outputs if you have them. Remove personal data first.
- `grader` (optional; one of: exact, rubric, model-judge, mixed; default: mixed): Grading approach to use. mixed picks the cheapest reliable grader for each criterion.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
An eval suite is the executable spec of an LLM feature. Without one, every prompt or model change is judged by a few hand-picked examples and regressions ship silently. Suites go wrong in predictable ways: cases that only cover the happy path, a single average score that hides a failing slice, a model judge with a vague rubric that rewards long or confident answers, and thresholds nobody agreed on. Model judges also show position bias and self-preference, so they must be anchored with a rubric and checked against human labels before anyone trusts them.
</context>

<task>
Write an eval suite for this feature:
$feature
Only if sample_inputs was provided: 

Sample inputs:
$sample_inputs

Grading approach: $grader.

1. Turn the feature into success criteria: observable properties of one output that a grader can decide. Mark each as a hard requirement (must hold on every case, such as valid JSON, no leaked system prompt, refusal of out-of-scope requests) or a quality criterion (scored). If the description does not say what a good output is, ask before writing cases.
2. Write 20 to 40 cases, each tagged with a slice:
   - golden (about 60%): typical inputs, built from the samples when given;
   - edge: empty or minimal input, very long input, mixed languages, ambiguous requests, unusual formatting, boundary values;
   - adversarial: prompt injection inside the user content, requests to reveal instructions, out-of-scope or disallowed requests that fit this feature, inputs designed to trigger the known failure modes.
   Use invented data only. Give a reference output or the key facts the output must contain wherever one exists.
3. Pick a grader for each criterion. Use exact match, regex or schema validation for deterministic properties. Use a rubric for qualities. For a model judge, write the judge prompt: the criterion, a 1-to-5 or pass/fail scale with an anchor example for each level, the reference answer when there is one, reasoning before the verdict, and, for pairwise comparisons, both orderings. Say how to calibrate the judge: 20 to 50 human-labelled cases and the agreement level required before it is trusted.
4. If the grading approach is exact or rubric only, say which criteria it cannot grade reliably and what you would use instead.
5. Set thresholds: hard requirements at 100%, a pass rate per quality criterion, a minimum per slice, the number of runs per case to absorb sampling variance, and the rule for comparing a candidate against the current version.
</task>

<constraints>
- Every case must test something a criterion names. Drop cases that duplicate another case's purpose.
- Do not use real names, emails or customer data in cases.
- Keep the judge prompt self-contained, so it runs without this conversation.
- Thresholds are starting values. Say how to revise them after the first runs.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Success criteria
Table: id | criterion | hard or quality | grader.

## Cases
One fenced YAML block. Each case: `id`, `slice`, `input`, `reference` (or `must_include`), `criteria` (ids).

## Graders
The deterministic checks, the rubric, and the full judge prompt in a fenced block, plus the calibration procedure.

## Thresholds and gating
Pass rules per criterion and slice, runs per case, and when a change may ship.

## Gaps
What the suite does not cover yet and what data would close it.
</output_format>
