---
description: Writes an LLM-as-judge grading prompt with a calibrated scale, anchored examples for each score, ordered criteria and a structured verdict, plus checks for common judge biases.
agent: agent
argument-hint: task_and_good_output criteria scale
---

# Write an LLM-as-judge prompt

<context>
A model grading another model's output is useful only if its scores agree with careful human judgement. Published work on LLM judges and provider eval guidance point to the same failure modes: vague criteria ("is it helpful?"), unanchored numeric scales where 6 and 7 mean nothing, several criteria merged into one score, verdicts written before the reasoning, and systematic biases: preferring longer answers (verbosity bias), the first of two options (position bias), answers that sound like the judge's own style (self-preference), confident tone over correctness, and leniency. Reliable judges grade one clearly defined criterion at a time, describe what each score looks like with concrete anchors, reason briefly from evidence before the verdict, return a fixed structured output, and are calibrated against a small human-labelled set before anyone trusts them.
</context>

<task>
Write a judge prompt on a ${input:scale:The scoring scale. binary is pass/fail per criterion and is usually the most reliable.} scale.

<task_and_good_output>
${input:task_and_good_output:The task being graded (the original prompt or a description), one or more outputs you consider good, and ideally one you consider bad, with why.}
</task_and_good_output>
Only if criteria was provided (leave it empty to skip): 
<criteria>
${input:criteria:Optional: what matters, in priority order, for example "factually correct against the source, answers the question, under 150 words, polite". Derived from the examples if left empty.}
</criteria>

1. If there is no way to tell what a good output is (no task description or no good example), ask for one and stop.
2. Define the criteria: from the given criteria, or derived from the examples (label these as assumptions). Make each one observable and testable, put them in priority order, and mark any hard gate (for example "factually wrong against the source fails regardless of other scores"). Recommend splitting into one judge call per criterion when there are more than three, or when criteria trade off against each other.
3. Write anchors for every point on the scale for each criterion: what an output at that score looks like, with a short concrete example drawn from the task. For 1-10, anchor at least 1, 4, 7 and 10 and say what separates neighbours; recommend binary or 1-5 if fine distinctions are not needed.
4. Write the judge prompt: the judge's role and what it must not do (reward length, style or confidence), the inputs in delimiters (the original task, any reference or source, the output to grade), the criteria in order, the anchors, an instruction to quote evidence and reason in two or three sentences before scoring, and a structured verdict.
5. List bias checks and how to run them, and a calibration plan.
</task>

<constraints>
- The verdict must be machine-readable: JSON with, per criterion, `evidence` (short quote), `reasoning` (at most three sentences), and `score`, then an `overall` field defined by an explicit rule (for example "fail if any gate fails, otherwise the mean").
- Instruct the judge to grade only against the criteria and reference given, to treat "I don't know" or a refusal according to an explicit rule, and to score an output the same regardless of length beyond what the criteria require.
- For pairwise comparison, require running both orders and counting only consistent preferences.
- Do not invent ground truth: if correctness needs a reference answer or source, add a slot for it in the judge prompt.
- Keep the judge prompt model-agnostic and under about 700 words.
</constraints>

<output_format>
## Criteria
A table: # | Criterion | Definition | Gate? (yes/no). Then any assumptions.
## Judge prompt
The full judge prompt in one fenced block, including the anchors and the JSON verdict schema.
## Bias checks
A table: Bias | How to test it | Mitigation in this prompt.
## Calibration plan
Numbered steps: label 30 to 50 outputs by hand, run the judge, measure agreement (percent agreement for binary, a rank or kappa statistic for scales), read every disagreement, adjust anchors, and re-run; the agreement level to reach before relying on it.
</output_format>
