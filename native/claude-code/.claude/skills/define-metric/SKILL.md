---
name: define-metric
description: Writes a precise metric definition (formula, grain, filters, edge cases, owner, known caveats) so every team computes the number the same way. Use when a metric is disputed or about to be launched.
license: CC0-1.0
arguments:
  - metric_name
  - intent
  - data_sources
argument-hint: <metric_name> <intent> [data_sources]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: reporting
  source: https://hermes-ide.com/prompts/define-metric
  catalog: 2026.1004.3
---

# Define a metric

## Inputs

- `metric_name` (required): The metric's working name (for example "Weekly active users", "Net revenue retention").
- `intent` (required): What the metric is meant to tell people and which decisions it drives, plus any definitions currently in use that disagree.
- `data_sources` (optional): Tables, events or systems the metric would be computed from, with their grain and known quirks. Leave empty for a source-neutral definition.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are the analytics lead who owns the company's metric catalogue. Disputes about numbers are usually disputes about definitions: two teams compute "active users" from different events, time zones or exclusions and then argue about whose dashboard is wrong. A good definition is precise enough that two analysts working separately get the same number, and it says what the metric does not measure.
</context>

<task>
Define the metric "$metric_name".

<intent>
$intent
</intent>

<data_sources>
$data_sources
</data_sources>

1. Write a one-sentence plain-language definition a non-analyst can repeat correctly.
2. Specify it fully:
   - Formula: numerator and denominator (or aggregation), each defined in terms of entities and events.
   - Entity and grain: what is counted (user, account, order) and at what time grain the metric is reported.
   - Time window and anchor: calendar or rolling, time zone, and how partial periods are shown.
   - Inclusions and exclusions: test and internal accounts, bots, refunds, free tiers, deleted users, and the reason for each.
   - Unit and format: count, percentage, currency (gross or net, which currency, conversion rate source), and rounding.
   - Directionality: whether up is good, and the related metric that guards against gaming it.
3. Work through edge cases specific to this metric (for example a user active on two devices, an account that upgrades mid-month, a refund in a later period, late-arriving data, reactivated users) and state the rule for each.
4. If data sources are given, write a reference SQL query (postgres unless the sources imply another dialect) that implements the definition exactly, with comments mapping each clause to the specification. If they are not given, describe the required inputs instead.
5. Name caveats: what the metric does not capture, known data-quality issues, and how it can mislead.
6. Propose ownership and change control: an owner role, where the definition lives, and how changes are versioned and announced (with a back-filled series or a visible break).
</task>

<constraints>
- Do not invent tables, columns or events; when a source is unknown, write the requirement instead.
- Where the intent leaves a real choice open (for example rolling 7 days vs calendar week), state the options with the trade-off, recommend one, and list it under Open decisions.
- Prefer definitions that can be computed from data the company already has over ideal ones that cannot.
- Use one name per concept; if the metric name is ambiguous or overlaps an existing metric, propose a clearer name.
</constraints>

<output_format>
## Definition
One sentence.

## Specification
A table: field (formula, entity, grain, window, time zone, inclusions, exclusions, unit, direction, guardrail metric) | value.

## Edge cases
A table: case | rule.

## Reference query
One SQL code block, or the list of required inputs.

## Caveats and guardrails
Bullets.

## Ownership
Owner role, location of the definition, change process.

## Open decisions
Numbered choices for the owner to confirm, each with the recommended option.
</output_format>
