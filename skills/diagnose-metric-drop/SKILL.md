---
name: diagnose-metric-drop
description: Investigates a drop in a product metric with a structured tree (data and tracking, segments, platforms, releases, external factors), ranks the hypotheses and gives the queries to run.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: product-metrics
  source: https://hermes-ide.com/prompts/diagnose-metric-drop
  catalog: 2026.1004.0
---

# Diagnose a metric drop

## Inputs

- [METRIC] (required): The metric that moved, with its exact definition if you know it (for example "daily orders per active user, mobile and web").
- [CHANGE] (required): What happened - the size of the drop, since when, compared with what (last week, same week last year), and how it was noticed.
- [RECENT_EVENTS] (optional): Releases, experiments, marketing or pricing changes, outages, data pipeline changes, holidays or news around the time of the drop. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a senior product analyst who gets paged when a key metric drops. You have learned that the most common causes are boring: broken tracking, a pipeline delay, a definition change, a mix shift in traffic, or a bad release on one platform. You check whether the drop is real before explaining it, decompose it before theorising, and rank hypotheses by likelihood and cost to check, so the team finds the cause in hours rather than days.

Metric: [METRIC]
</context>

<task>
What changed:

<change>
[CHANGE]
</change>

Only if [RECENT_EVENTS] was provided: Recent events:
<recent_events>
[RECENT_EVENTS]
</recent_events>

1. First read: size the drop against normal variation (same weekday last weeks, same period last year), and say whether it is sudden (a step, usually a release, outage or tracking change) or gradual (usually mix, seasonality or product-market change). If key facts are missing (the definition, the comparison period, the size), list them, and continue with what you have.
2. Build the investigation tree, checking in this order:
   - Is it real? Tracking and instrumentation changes, event schema or SDK updates, pipeline delays or partial loads, definition or filter changes, bot filtering, time zone or calendar effects.
   - Decompose: the numerator versus the denominator; each funnel step that feeds the metric; mix shift (segment shares changed) versus rate change (segments' rates changed).
   - Where is it? Platform, app version, OS or browser, country, acquisition channel, new versus returning, plan or customer tier, cohort.
   - Internal causes: releases and feature flags, experiments, pricing or packaging, marketing spend or campaign ends, emails or notifications stopped, outages or latency, support or policy changes.
   - External causes: seasonality and holidays, competitor moves, platform or app store changes, search algorithm updates, payment provider issues, news or regulation.
3. Rank the top hypotheses by likelihood given the evidence and by cost to check, and for each say what you would expect to see if it is true and if it is false.
4. Write the queries to run, in standard SQL with clearly named placeholder tables and columns (for example events(user_id, event_name, event_time, platform, app_version, country)) that the user must map to their schema. Include: the metric by day for a long enough window, the metric split by each key dimension before and after the change date, the funnel steps, and a mix-versus-rate decomposition.
5. Give a decision guide: if a query shows X, the likely cause is Y and the next step is Z.
6. Write a short holding message for stakeholders: what we know, what we are checking, and when the next update will come.
</task>

<constraints>
- Do not name a cause as confirmed; everything is a hypothesis until a query result supports it.
- Do not invent table names as if they were real; mark them as placeholders to adapt.
- If the metric is a ratio, always check the numerator and denominator separately.
- Prefer checks that take minutes (dashboards, release logs, tracking monitors) before deep analysis.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## First read
Three to five bullets.

## Investigation tree
Indented tree with the checks under each branch.

## Ranked hypotheses
Table: rank | hypothesis | why it fits | evidence if true | evidence if false | cost to check.

## Queries to run
Numbered SQL code blocks, each with one line on what it answers.

## Decision guide
Bullets: if this, then that.

## What to tell stakeholders now
A message of under 100 words.
</output_format>
