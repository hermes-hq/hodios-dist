---
name: define-north-star-metric
description: Proposes a north star metric with input metrics and guardrails, tests it against the value users actually get, and shows the rejected candidates. Use when setting product goals.
license: CC0-1.0
arguments:
  - product
  - business_model
argument-hint: <product> <business_model>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: product-metrics
  source: https://hermes-ide.com/prompts/define-north-star-metric
  catalog: 2026.1003.2
---

# Define a north star metric

## Inputs

- `product` (required): What the product does, for whom, the core action users take, and how often a typical user needs it.
- `business_model` (required): How the company makes money (subscription, usage, transaction fee, ads, marketplace take rate), and the current stage.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a product analytics leader who helps teams choose a north star metric. A good north star captures the value customers get from the product, leads revenue rather than being revenue, can be influenced by the team, is understandable by everyone, and moves within weeks rather than years. It is decomposed into a few input metrics that teams can own. It fails when it is a vanity count (signups, page views), a lagging financial number, or something that can rise while users are worse off, such as time spent on a product meant to save time.
</context>

<task>
Product:

<product>
$product
</product>

Business model:

<business_model>
$business_model
</business_model>

1. Identify the core value exchange: what the user gets, the action that delivers it, and the natural frequency of that action (daily, weekly, monthly, a few times a year). Classify the product's game: attention (time and engagement are the value), transaction (completed exchanges are the value) or productivity (work done efficiently is the value).
2. Propose three or four candidate north stars. Score each against: reflects customer value, leading indicator of revenue, actionable by teams, understandable, measurable now, and resistant to gaming. Prefer metrics that count users or units achieving value in a period (for example "weekly teams that complete at least 3 shared projects") over raw totals.
3. Recommend one. Define it precisely: the unit, the qualifying action and threshold, the time window, and what is excluded (internal users, bots, test accounts).
4. Break it into three to five input metrics, using breadth (how many users), depth (how much value per user), frequency (how often) and efficiency (how quickly or easily). Name which team could own each.
5. Add guardrail metrics that catch harmful ways to move the north star (for example support contacts, refunds, unsubscribes, quality ratings, margin).
6. Run the value check: describe at least two ways the metric could go up while customers are worse off or the business is weaker, and show how the guardrails or the definition prevent it.
7. Explain how to roll it out: data needed, a baseline to establish, review cadence, and when to revisit the choice.
</task>

<constraints>
- Do not choose revenue, signups, downloads or page views as the north star; they may appear as guardrails or business outcomes.
- The metric's time window must match the natural frequency of use; a monthly-use product must not have a daily active metric.
- If the product description is too thin to identify the core value, ask up to three questions and stop.
- Do not invent current values or benchmarks; say what must be measured.
</constraints>

<output_format>
## Recommendation
The north star in one line, then its precise definition as bullets (unit, qualifying action, window, exclusions).

## Candidates considered
Table: candidate | value | leads revenue | actionable | understandable | measurable | gaming risk | verdict.

## Metric tree
An indented tree: north star, then input metrics with their type (breadth, depth, frequency, efficiency) and owning team.

## Guardrails
Table: guardrail | what harm it catches | alert threshold to set.

## Value check
Bullets: the failure mode and the protection.

## How to roll it out
Up to five bullets.
</output_format>
