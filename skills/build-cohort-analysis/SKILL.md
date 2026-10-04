---
name: build-cohort-analysis
description: Builds a cohort retention analysis from event data (cohort definition, query or code, the retention triangle) and explains how to read it. Use to see whether newer customers stick around better.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: data-exploration
  source: https://hermes-ide.com/prompts/build-cohort-analysis
  catalog: 2026.1004.1
---

# Build a cohort retention analysis

## Inputs

- [EVENT_DATA] (required): The table or file with user activity (columns, types, sample rows) and where it lives (a SQL warehouse and its dialect, or a CSV for pandas).
- [COHORT_BY] (optional; default: signup month): What groups users into cohorts.
- [ACTIVITY_DEFINITION] (required): What counts as retained in a period (for example "placed at least one paid order", "opened the app at least 3 days that week").

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a product analyst building a cohort retention analysis. A retention triangle answers one question well: are later cohorts behaving better or worse than earlier ones at the same age? It is easy to get wrong in ways that look plausible: counting calendar periods instead of periods since joining, letting the youngest cohorts' incomplete periods look like drops, or mixing a cohort definition with an activity definition that the cohort event itself satisfies.
</context>

<task>
Build a cohort retention analysis.

<event_data>
[EVENT_DATA]
</event_data>

Cohort by: [COHORT_BY]

<activity_definition>
[ACTIVITY_DEFINITION]
</activity_definition>

1. Define precisely: the cohort event and date for each user (for example first signup), the period length (month or week, matching the cohort grain unless the activity definition says otherwise), period 0, and the retention measure. Decide whether the cohort event itself counts as period-0 activity and say which.
2. Decide the retention type and state it: classic or bounded (active in exactly period N) by default; mention unbounded or rolling retention (active in N or later) only if the use case calls for it.
3. Write the code. If the data lives in a SQL warehouse, write SQL for the dialect named or implied in the event data (default postgres) using CTEs: cohorts, activity by period, cohort sizes, then the triangle. If it is a file, write pandas. Compute period number as whole periods since the cohort date, not calendar month minus calendar month on raw timestamps without truncation.
4. Output the triangle as cohorts in rows, period numbers in columns, values as percentages of cohort size, with the cohort size as its own column.
5. Mark cells that are incomplete because the period has not fully elapsed, and exclude them from averages.
6. If the event data includes a sample, compute the triangle on the sample to show the shape, labelled as illustrative.
</task>

<constraints>
- If the event data lacks a user identifier, a timestamp, or anything that can satisfy the activity definition, say what is missing and stop.
- Never fill missing cohort-period cells with zeros; an unobserved period is not zero retention.
- Users with activity before their cohort date (data errors, imports) are reported as a count, not silently dropped or kept.
- Do not draw conclusions from cohorts smaller than about 30 users without saying the numbers are noisy.
- Keep time zones consistent between the cohort date and activity timestamps; state the assumption.
</constraints>

<output_format>
## Definitions
Bullets: cohort, period, period 0, retained, retention type, time zone.

## Code
One code block.

## Retention triangle
A Markdown table if computed from a sample (labelled illustrative); otherwise the column layout the code produces.

## How to read it
Four to six sentences: reading down a column (cohort quality over time), across a row (decay curve), where the curve flattens, and what change would count as meaningful.

## Caveats
Bullets specific to this data: incomplete periods, small cohorts, seasonality, definition changes.
</output_format>
