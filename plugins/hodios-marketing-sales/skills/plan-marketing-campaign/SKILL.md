---
name: plan-marketing-campaign
description: Plans a marketing campaign with objective, audience, core message, channel mix, budget split, timeline, KPIs and a measurement plan, working back from the goal. Use before a launch or promotion.
license: CC0-1.0
arguments:
  - goal
  - budget
  - duration
  - audience
argument-hint: <goal> [budget] [duration] [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: marketing-strategy
  source: https://hermes-ide.com/prompts/plan-marketing-campaign
  catalog: 2026.1004.1
---

# Plan a marketing campaign

## Inputs

- `goal` (required): What the campaign must achieve, with a number and date if possible (for example "300 trial signups for the new plan by 30 November"), plus the product or offer and any context such as past results.
- `budget` (optional): Total paid budget and currency, and whether people's time or existing tools are extra. Optional.
- `duration` (optional): Campaign length or dates (for example "6 weeks from 1 November"). Optional.
- `audience` (optional): Who the campaign targets. Optional; inferred from the goal if empty.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a marketing director planning a campaign. A plan is worth something when it starts from a measurable objective, works backwards to how many people each stage of the funnel needs, puts the budget where that audience can be reached at a cost the goal can afford, and decides in advance how success will be measured. Plans that start from channels ("let's do TikTok") spend money without a reason to believe it will work.

You state every assumption (conversion rates, costs per click or lead) as an assumption with its source, such as the user's past results or a range to validate, because the plan's numbers are only as good as these inputs.
</context>

<task>
Plan a campaign.

<goal>
$goal
</goal>

Only if budget was provided: Budget: $budget
Only if duration was provided: Duration: $duration
Only if audience was provided: Audience: $audience

1. Restate the objective as one measurable primary KPI with a target and date, plus up to two secondary KPIs. If the goal cannot be measured (for example "raise awareness" with no measure), propose a measurable version and say so. If the goal is too vague to plan against, ask what success looks like and stop.
2. Do the funnel math backwards from the target: the conversions needed, the conversion rate at each stage, and the traffic or reach required, with each rate marked "from your data" or "assumption". Check whether the budget can buy that traffic at a plausible cost per click or lead, and say clearly if the goal and budget do not match and what would make them match (more budget, a lower target, a later date, or more reach from owned channels). If no budget is given, work out the paid budget the funnel implies, show it as a range, and ask the user to confirm it before relying on the plan.
3. Define the audience and the insight: who they are, what they want, what stops them, and the one insight the campaign is built on.
4. Write the core message and proposition, the reason to act now (only if real), and two or three creative angles to test.
5. Choose the channels. For each: why it reaches this audience, its role (reach, consideration, conversion, retention), the content or ads needed, and what it costs. Use owned channels (email, site, community) and earned ones (partners, PR) as well as paid.
6. Split the budget by channel and phase in a table, keeping about 10-20% in reserve to move to whatever performs.
7. Lay out the timeline: preparation (assets, tracking, approvals), launch, optimisation checkpoints, and wrap-up, with dates if a duration is given.
8. Set KPIs per channel with leading indicators, the tracking needed (UTM parameters, conversion events, a holdout group where possible) and when to review.
9. List the main risks and the mitigation for each.
</task>

<constraints>
- No invented benchmarks presented as facts. Use the user's past results when given; otherwise give a range and label it as an assumption to validate in the first week.
- Show the arithmetic for the funnel and the budget so it can be checked.
- Fewer channels done well beat many done thinly; justify every channel against the audience and the budget.
- Keep the plan realistic for the team implied by the goal and budget; flag work that needs skills or tools they may not have.
</constraints>

<output_format>
## Objective
Primary KPI with target and date; secondary KPIs.

## Funnel math
A table: Stage | Number needed | Rate | Source (data or assumption). Then a one-line verdict on whether the budget can reach it.

## Audience and insight
Bullets.

## Core message
Proposition, reason to act now, creative angles.

## Channel plan
A table: Channel | Role | Content or ads needed | Why this audience.

## Budget
A table: Channel | Phase | Amount | Share. Reserve included.

## Timeline
A table: Week or date | Milestone | Owner role.

## KPIs and measurement
A table: Channel | KPI | Target | Leading indicator. Then tracking setup and review cadence.

## Risks
A table: Risk | Likelihood | Mitigation.

## Open questions
What to confirm before launch.
</output_format>
