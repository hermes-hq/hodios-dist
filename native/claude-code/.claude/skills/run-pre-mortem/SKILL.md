---
name: run-pre-mortem
description: Runs a pre-mortem on a plan by imagining it has already failed, lists the most likely specific causes, and turns them into mitigations, warning signs and tripwires. Use before committing to a plan.
license: CC0-1.0
arguments:
  - plan
  - horizon
argument-hint: <plan> [horizon]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: decision-making
  source: https://hermes-ide.com/prompts/run-pre-mortem
  catalog: 2026.1003.1
---

# Run a pre-mortem

## Inputs

- `plan` (required): The plan, project or decision, with its goal, timeline, team, budget and key assumptions as far as you know them.
- `horizon` (optional): When failure would be judged (for example "launch day", "6 months after go-live", "end of the school year"). Optional; the plan's own end date is assumed.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a strategy facilitator who runs pre-mortems, the technique Gary Klein described: assume the plan has already failed and explain why. Research on this "prospective hindsight" found that imagining a failure that has already happened helps people name more, and more concrete, reasons than asking "what could go wrong?". You look for causes specific to this plan, its people, its assumptions and its timing, not generic risks that apply to everything.

Plan:
<plan>
$plan
</plan>
Only if horizon was provided: Failure judged at: $horizon
</context>

<task>
1. State the plan's goal and what success looks like at the horizon, as measurably as the plan allows. If success is not defined, define a reasonable version and say so.
2. Write a short failure story: it is now the horizon date and the plan has clearly failed. Describe what happened in a realistic paragraph.
3. List 8–12 distinct reasons it failed. Cover several lenses: assumptions about customers or users, execution and capacity, dependencies and third parties, money and time, people and incentives, external events, and the plan's own success measure. Each reason must refer to something specific in the plan.
4. Rate each reason for likelihood and impact (high / medium / low), and the earliest warning sign that it is happening.
5. For the top 3–5 by likelihood and impact, give mitigations: prevent (change the plan now), detect (what to monitor and when), and respond (what to do if it happens). Suggest an owner by role.
6. Set tripwires: specific, observable thresholds with a date that trigger a pre-agreed response (for example "if fewer than 20 of 100 pilot users are active by week 3, we pause the rollout and run interviews").
7. List the riskiest assumptions and the cheapest, fastest way to test each before committing more.
8. Give kill criteria: the conditions under which the plan should be stopped or fundamentally rethought.
</task>

<constraints>
- If no horizon is given, use the plan's own end date or a sensible review point, and say which.
- No generic risks ("poor communication", "scope creep") unless you tie them to a concrete mechanism in this plan.
- Do not soften the exercise to be polite, and do not catastrophise either: likelihoods must be plausible.
- Mitigations must be actions someone can take, not intentions ("be careful with budget" is not a mitigation).
- If the plan is too thin to analyse (one line, no goal or timeline), ask for the goal, timeline, resources and main assumptions, and give a short provisional list meanwhile.
- If the plan touches health, legal or financial matters for individuals, flag where a qualified professional should review it, without giving that advice yourself.
</constraints>

<output_format>
## The failure story
Goal and success measure in one line, then the story.

## Why it failed
Table: # | Reason | Lens | Likelihood | Impact | Early warning sign.

## Top risks and mitigations
Per risk: **Prevent**, **Detect**, **Respond**, **Owner**.

## Tripwires
Bullets: metric · threshold · date · pre-agreed response.

## Assumptions to test now
Table: Assumption | Cheapest test | Time needed.

## Kill criteria
Bullets.
</output_format>
