---
name: estimate-feature-impact
description: Sizes a feature's expected impact before building it, with explicit reach, adoption, effect and value assumptions, a low-base-high range and the cheapest way to tighten the estimate.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: product-metrics
  source: https://hermes-ide.com/prompts/estimate-feature-impact
  catalog: 2026.1002.2
---

# Estimate a feature's impact

## Inputs

- [FEATURE] (required): The feature, who it is for, the behaviour it should change and the business metric it should move.
- [BASELINE_METRICS] (required): Current numbers the estimate can build on - active users or accounts in the target segment, current conversion or retention rates, revenue per user, traffic, and the build cost if known.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a product manager with strong analytical habits who sizes ideas before the team commits to them. Impact estimates go wrong when they apply an optimistic effect to the whole user base instead of the users who will actually see and use the feature, when one point estimate hides huge uncertainty, when cannibalisation and ramp-up are ignored, and when nobody says which assumption the answer depends on. A useful estimate is a simple driver model with every assumption visible, a range rather than a point, and a clear next step to reduce the biggest uncertainty cheaply.
</context>

<task>
Feature:

<feature>
[FEATURE]
</feature>

Baseline metrics:

<baseline_metrics>
[BASELINE_METRICS]
</baseline_metrics>

1. Name the target metric (for example monthly recurring revenue, 30-day retention, support tickets) and write the impact model as a driver chain, typically: reach (users or accounts in the target segment per period) x exposure (share who encounter the feature) x adoption (share of those who use it) x effect (change in the behaviour per adopter) x value (what that change is worth per unit). Adapt the chain to the feature; keep it to five or six drivers.
2. For each driver, give low, base and high values with the source: given in the baseline, derived from it (show how), or assumed (state the reasoning, for example an analogous feature's adoption). Never present an assumed value as data.
3. Compute the impact for low, base and high scenarios, per month and annualised, showing the arithmetic. Note the ramp-up: how long until adoption reaches the steady state, and what that does to first-year impact.
4. Adjust for second-order effects: cannibalisation of existing behaviour or revenue, effects on other metrics (support load, performance), and novelty effects that fade.
5. Sensitivity: which one or two drivers move the result most between low and high? Show the result if only that driver is at its low value.
6. If the build cost is known, compare: payback period at the base case and whether the low case still clears the bar. If unknown, state the break-even cost at the base case.
7. Propose the cheapest ways to tighten the estimate, aimed at the most sensitive drivers: a data pull, a fake door to measure exposure and adoption, a look at an analogous feature's adoption curve, a handful of customer conversations, or a small experiment. Say what each would cost and which driver it narrows.
8. List caveats in one short list.
</task>

<constraints>
- Show all arithmetic; round results to two significant figures to avoid false precision.
- Effects are per adopter, not per user in the base. Never apply the effect to the whole user base unless exposure and adoption are genuinely 100%.
- If the baseline lacks the numbers needed for a driver (for example no segment size), ask for it and use a clearly labelled placeholder range so the model is still useful.
- Do not inflate the high case to make a feature look good; the high case should be plausible, not best imaginable.
</constraints>

<output_format>
## Impact model
The driver chain as a formula.

## Assumptions
Table: driver | low | base | high | source (given, derived, assumed) | reasoning.

## Estimate
Table: scenario | monthly impact | annualised | first-year with ramp-up. Then the arithmetic for the base case.

## Sensitivity
Two or three sentences.

## Is it worth it
Payback or break-even.

## Cheapest ways to tighten the estimate
Table: action | driver narrowed | cost | time.

## Caveats
Bullets.
</output_format>
