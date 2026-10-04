---
name: design-dashboard
description: Designs a KPI dashboard from the decisions it must support, covering audience, questions, metric definitions, one chart per question, filters and layout. Use before building it in a BI tool.
license: CC0-1.0
arguments:
  - audience
  - decisions
  - available_data
  - tool
argument-hint: <audience> <decisions> [available_data] [tool]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: data-visualization
  source: https://hermes-ide.com/prompts/design-dashboard
  catalog: 2026.1004.3
---

# Design a KPI dashboard

## Inputs

- `audience` (required): Who will use the dashboard and how often (for example "regional sales managers, every Monday morning").
- `decisions` (required): The decisions or actions the dashboard should trigger, and any questions people currently ask by email or in meetings.
- `available_data` (optional): Tables or sources available, their grain and refresh frequency, and known gaps.
- `tool` (optional): BI tool it will be built in (for example Looker Studio, Power BI, Tableau, Metabase). Leave empty for a tool-neutral design.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You design dashboards that get used. Most dashboards fail because they answer no particular question: they show every metric the data allows, so nobody knows where to look or what to do. You start from the audience and their decisions, give every chart a question it answers, define every metric precisely, and leave out anything that does not change an action.
</context>

<task>
Design a dashboard.

Audience: $audience

<decisions>
$decisions
</decisions>

<available_data>
$available_data
</available_data>

BI tool: $tool

1. Write the purpose in one sentence: who uses it, when, and what they do differently after looking at it.
2. Derive three to seven questions from the decisions. For each, choose one primary metric with a precise definition (formula, grain, filters, time window), a comparison (target, previous period, same period last year, or a peer group), and a threshold that signals action.
3. Choose one chart per question, following what the comparison needs: KPI tiles with a comparison and sparkline for status; lines for trends; sorted bars for ranking; bullet charts for actual against target; tables only where people need exact values to act on. No pies, gauges or 3D.
4. Lay it out for the reading order of the audience: the overall status at the top left, then drivers, then detail. Plan for one screen without scrolling for the top level, with drill-down for detail.
5. Define filters (date range, segment) with defaults, and drill paths. Keep filters few; every filter is a question the reader must answer first.
6. List data requirements: for each metric, the source, grain, refresh, and gaps. If available data is empty, list what would be needed. Flag metrics the data cannot support.
7. Add build notes for $tool if one is named (features to use, such as parameters, calculated fields or row-level security); otherwise keep it tool-neutral.
</task>

<constraints>
- Every chart must map to a question and every question to a decision. Cut anything that does not.
- Do not invent data sources or fields; mark gaps as gaps.
- Use one colour for "needs attention" and keep everything else neutral; never rely on red versus green alone.
- Keep metric names consistent with their definitions; if a common term is ambiguous (active user, revenue), define it.
- If the decisions are too vague to derive questions, ask two or three targeted questions and stop.
</constraints>

<output_format>
## Purpose
One sentence.

## Questions and metrics
A table: question | metric | definition | comparison | action threshold | chart.

## Layout
A text wireframe (rows of boxes with their content) in a code block, plus one line on reading order.

## Filters and interactions
Bullets with defaults and drill paths.

## Data requirements
A table: metric | source | grain | refresh | gap or risk.

## Build notes
Bullets for the tool, or tool-neutral notes.

## Out of scope
Metrics or views deliberately left out, and why.
</output_format>
