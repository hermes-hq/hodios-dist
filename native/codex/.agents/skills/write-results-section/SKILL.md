---
name: write-results-section
description: Writes a manuscript results section that reports findings in a logical order with exact statistics, effect sizes, confidence intervals and figure references, and no interpretation.
license: CC0-1.0
metadata:
  version: 1.1.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/write-results-section
  catalog: 2026.1004.3
---

# Write a results section

## Inputs

- [RESULTS_DATA] (required): Your analysis output - statistics, tables, model output, participant flow numbers - and the pre-specified primary and secondary outcomes or hypotheses in order.
- [REPORTING_GUIDELINE] (optional): The style or guideline to follow, for example "APA 7", "CONSORT", "STROBE", "AMA", or the journal's instructions. If empty, a neutral style is used and named.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A results section reports what was found, in the order the questions were asked, so a reader can check every claim against the numbers. Editors and statistical reviewers look for: participant flow and sample characteristics first; the primary outcome before secondary and exploratory ones; for each estimate, the effect size with its confidence interval, the test statistic, degrees of freedom and exact p value (p < .001 below that); the same precision throughout; non-significant results reported as fully as significant ones; and pre-specified and post hoc analyses clearly separated. Interpretation, comparison with other studies and speculation belong in the discussion.
</context>

<task>
Write the results section from this outputOnly if [REPORTING_GUIDELINE] was provided: , following [REPORTING_GUIDELINE].
<results_data>
[RESULTS_DATA]
</results_data>

1. Before writing, check the numbers for internal consistency: sample sizes that add up across groups and flow stages, percentages that match counts, p values consistent with the test statistic and degrees of freedom, confidence intervals that contain the point estimate, and means within the possible range of the scale. List every inconsistency instead of silently fixing it.
2. Order the section: sample and participant flow, baseline characteristics (refer to the table), primary outcome, secondary outcomes, then sensitivity and exploratory analyses, each labelled as pre-specified or post hoc.
3. For each result, write one or two sentences giving the direction and size of the effect in the outcome's units, the confidence interval, and the test details in the style required. Report non-significant results the same way, with their estimates and intervals.
4. Refer to tables and figures by number, using placeholders like (Table 2) and (Figure 1), and keep numbers that are in a table out of the text unless they are the key result.
5. Use subheadings that mirror the methods or hypotheses.
</task>

<constraints>
- No interpretation: no "this suggests", "importantly", "interestingly", "as expected", no comparisons with other studies, no explanations of why.
- Never describe a non-significant result as a "trend", "marginally significant" or "approaching significance". Report the estimate and interval and let the discussion handle it.
- Do not use "significant" except in the statistical sense.
- Do not round, recompute or change any number except to apply consistent decimal places, and say if you did. Do not invent any statistic that is not in the input; mark gaps as [MISSING: ...].
- Use the past tense for findings.
- If the primary outcome is not identified, ask for it, and order results by the hypotheses as given in the meantime.
- If the results are qualitative (themes or categories), report each theme with its definition, how widely it occurred in the terms the author used, and supporting quotes taken word for word from the input, labelled with the participant codes given; replace the statistical consistency checks with a check that every quote and code appears in the input.
</constraints>

<output_format>
## Results
The section with subheadings and figure and table references.
## Tables and figures referenced
List of each reference and what it must contain.
## Consistency checks
Each check and its outcome; inconsistencies first.
## Missing information
Each [MISSING] item and what is needed.
</output_format>
