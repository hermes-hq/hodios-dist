---
name: analyze-ab-test-results
description: Analyses A/B test results with a sample-ratio-mismatch check, effect sizes, confidence intervals and guardrail metrics, ending in a ship, iterate or stop call. Use when an experiment ends.
license: CC0-1.0
metadata:
  version: 1.1.0
  kind: prompt
  category: statistics
  source: https://hermes-ide.com/prompts/analyze-ab-test-results
  catalog: 2026.1003.1
---

# Analyse A/B test results

## Inputs

- [RESULTS] (required): The results per variant (units assigned, such as users; conversions, or metric means with standard deviations), the randomisation unit, the intended traffic split, the test dates and any pre-registered minimum detectable effect.
- [PRIMARY_METRIC] (required): The single metric the test was designed to move, for example "checkout conversion rate".
- [GUARDRAILS] (optional): Metrics that must not get worse, with the largest acceptable drop, for example "refund rate, no worse than +0.2 percentage points".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Experiment readouts go wrong in predictable ways: analysing a test whose traffic split is broken (a sample ratio mismatch usually means a bug in assignment or logging, and invalidates the result), reporting a p-value without the size and uncertainty of the effect, calling a win after peeking or after testing many metrics and segments, and ignoring guardrails. A good readout checks validity first, then estimates the effect with an interval, then decides against criteria that were set before the test.
</context>

<task>
Analyse this experiment. Primary metric: [PRIMARY_METRIC].
<results>
[RESULTS]
</results>
Only if [GUARDRAILS] was provided: 
Guardrail metrics and thresholds: [GUARDRAILS]

1. Data quality: run a sample-ratio-mismatch check with a chi-square goodness-of-fit test against the intended split (assume an equal split if none is given, and say so). Treat p < 0.001 as a mismatch. Also note anything else suspicious: very short duration, less than one full weekly cycle, or a metric that is implausibly different.
2. If there is a mismatch, stop the effect analysis, give the decision "Do not trust: investigate assignment", and list likely causes to check.
3. Primary metric: compute each variant's value, the absolute difference and relative lift, a two-sided 95% confidence interval for the difference (two-proportion z-interval for rates; Welch's t-interval for means), and the p-value. Compare the interval with the minimum detectable or practically meaningful effect if one was given.
   - Check the unit of analysis. If the metric's denominator is not the randomisation unit (for example conversion per session or revenue per order while users were randomised), observations are not independent and the naive interval is too narrow. Use per-unit aggregates with the delta method, or ask for per-user data, and say which you did.
4. Guardrails: for each, compute the difference and its interval and say whether the interval rules out a breach of the threshold (non-inferiority), shows a breach, or is inconclusive.
5. Caveats: multiple variants or metrics (apply a correction such as Holm and say so), early stopping or peeking, novelty effects, segment results (exploratory only), and whether the test was powered for the observed effect.
6. Decide, using the first rule that applies:
   - Do not trust: the SRM check failed or another data-quality problem invalidates the comparison.
   - Stop: the primary metric is worse, or its whole interval lies below the smallest effect worth having (flat, or too small to matter).
   - Ship: the interval's lower bound is above zero, the effect is large enough to matter (judged against the stated minimum effect, or say that none was given), and every guardrail passes.
   - Iterate: anything else, such as an interval that includes zero but leaves a worthwhile effect possible, or a primary win with a guardrail that is breached or inconclusive.
</task>

<constraints>
- Show the formulas and the arithmetic so the reader can check them. If you can run code, compute the numbers with it and say so; otherwise compute carefully by hand and round only in the final line.
- Use only the numbers provided. If you need a value that is missing (for example standard deviations for a mean metric, or the number of users per variant), ask for it and do not estimate it. In that case write "Cannot decide yet" under Decision, name the missing values, and complete only the sections the given numbers support.
- Never call a result significant or not on the p-value alone; always report the interval.
- Treat segment results and secondary metrics as hypotheses for a follow-up test, not as grounds to ship.
- Use the decision words exactly: Ship, Iterate, Stop, Do not trust, or Cannot decide yet.
</constraints>

<output_format>
## Decision
The decision word, then two or three sentences on why.
## Data quality
The SRM result (observed vs expected counts, chi-square, p) and any other warnings.
## Primary metric
A table: variant | n | value | absolute difference | relative lift | 95% CI | p-value. After a failed SRM check, write "Not analysed: sample ratio mismatch" here and under Guardrails.
## Guardrails
A table: metric | difference | 95% CI | threshold | status (pass / breach / inconclusive).
## Caveats
Bullets.
## Calculations
The formulas and arithmetic.
</output_format>
