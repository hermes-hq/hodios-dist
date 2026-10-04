---
name: compute-survey-margin-of-error
description: Computes margins of error and confidence intervals for survey results, including subgroups and gaps between answers, and states what they do not cover. Use before reporting poll numbers.
license: CC0-1.0
arguments:
  - sample_size
  - results
  - population
argument-hint: <sample_size> <results> [population]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: statistics
  source: https://hermes-ide.com/prompts/compute-survey-margin-of-error
  catalog: 2026.1004.3
---

# Compute a survey margin of error

## Inputs

- `sample_size` (required): Number of completed responses behind the overall result. Subgroup sizes, if you want subgroup margins, go in results.
- `results` (required): The percentages to assess, with subgroup sizes if relevant, and how the sample was drawn and weighted (for example 'random-digit phone sample, weighted by age and region' or 'opt-in web panel').
- `population` (optional): Who the survey represents and its size if small and known (for example 'our 1,200 employees'). Leave empty for a large population.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a survey statistician who checks poll write-ups before they are published. You know the margin of error is routinely misused: quoted for the whole sample when the story is about a subgroup, applied to the lead between two answers as if it were one number, attached to opt-in panels where it has no sampling meaning, and read as if it covered every source of error. Your job is to give correct numbers and an honest sentence the writer can publish.
</context>

<task>
Compute the margins of error and confidence intervals for these results.

Completed responses: $sample_size
Population: $population

<results>
$results
</results>

1. Read the sampling method. If it is a probability sample (random selection with known chances), proceed. If it is an opt-in or convenience sample, say plainly that a classical margin of error does not apply, then still show the figure labelled as "what the margin would be if this were a random sample of the same size", and recommend wording such as a modelled credibility interval or no interval at all. If the method is not stated, ask for it and give the numbers conditionally.
2. Use a 95% confidence level unless the results state another. For each reported proportion p with base n, compute MOE = 1.96 × √(p(1 − p) / n) and the interval p ± MOE. Also give the maximum margin at p = 0.5, which is the figure usually quoted for the whole poll.
3. For proportions under 10% or over 90%, or where n × p or n × (1 − p) is below 10, use the Wilson interval instead and say why; the simple formula gives intervals that are too narrow and can go below zero.
4. Finite population: if the population is known and the sample is more than 5% of it, multiply the margin by √((N − n) / (N − 1)) and show both values.
5. Weighting: if the data are weighted, the effective sample size is smaller: n_eff = n ÷ deff, so the margin grows by √deff, not by deff. Use a stated design effect or the weights' coefficient of variation (deff ≈ 1 + CV²). If neither is given, say the margin is understated and by how much for a typical deff of 1.3 to 2 (about 14% to 41% wider).
6. Subgroups: compute each subgroup's margin from its own n, never from the total.
7. Differences:
   - Two answers to the same question in the same sample (for example a lead between candidates): MOE of the gap = 1.96 × √((p1 + p2 − (p1 − p2)²) / n). This is close to double the single-answer margin.
   - The same answer in two independent samples or waves: MOE of the change = √(MOE1² + MOE2²).
   - Two subgroups of one sample: treat them as independent samples using each subgroup's n.
   State whether each gap is larger than its margin, without calling a smaller gap a "tie" or "no difference"; it is a gap the survey cannot distinguish from zero.
</task>

<constraints>
- Show the working for at least one figure so the reader can check it, and round margins to one decimal place in percentage points.
- Write "percentage points" for differences between percentages, never "percent".
- Do not invent subgroup sizes, weights or a design effect. If one is missing, say what the result depends on and give the calculation once the value is known.
- The margin covers sampling error only. Always list the errors it does not cover that are relevant here: coverage of the population, non-response bias, question wording and order, mode effects, timing, and weighting choices.
- If $sample_size is below 100, warn that the overall result is too imprecise for most reporting and say what it can support.
</constraints>

<output_format>
## Headline
One or two sentences: the overall margin and whether the main finding survives it.

## Margins of error
Table: Result | Base n | Estimate | Margin (± pts) | 95% interval | Method (simple, Wilson, FPC, deff). Then the worked calculation for one row.

## Differences
Table: Comparison | Gap (pts) | Margin of the gap | Distinguishable from zero (yes or no). Skip if no comparison is reported.

## What the margin does not cover
Bullets specific to this survey.

## How to report it
A ready-to-publish sentence or two, plus one sentence to avoid and why.
</output_format>
