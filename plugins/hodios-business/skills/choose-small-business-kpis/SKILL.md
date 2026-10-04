---
name: choose-small-business-kpis
description: Chooses five to eight KPIs for a small business with exact definitions, data sources, targets, a weekly review routine and the action to take when each one moves.
license: CC0-1.0
arguments:
  - business
  - goals
argument-hint: <business> [goals]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: operations
  source: https://hermes-ide.com/prompts/choose-small-business-kpis
  catalog: 2026.1004.2
---

# Choose KPIs for a small business

## Inputs

- `business` (required): What the business does, how it makes money, team size, the systems that hold data (till or POS, accounting software, booking tool, spreadsheet), and the figures you already look at.
- `goals` (optional): What matters most this year, for example "grow repeat customers", "get margin back above 60%", "stop cash running short at month end".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help small business owners pick the few numbers that tell them whether the business is healthy and what to do next. Owners usually either track nothing or drown in dashboards. A useful scorecard has five to eight KPIs that cover money, customers and operations, mixes lagging results (revenue, margin) with leading signals (enquiries, bookings, repeat visits), can be pulled in under 30 minutes a week from systems the business already has, and has an agreed action for when each number moves. A KPI with no owner and no action is decoration.
</context>

<task>
Choose KPIs for this business.

<business>
$business
</business>
Only if goals was provided: 
<goals>
$goals
</goals>

1. Identify the business model drivers: how revenue is made (customers × frequency × spend, or projects × value, or subscribers × price), where margin is lost, and what limits growth (capacity, demand, cash). If goals are empty, infer the two most likely priorities from the business description and say so.
2. Choose five to eight KPIs covering cash and profit, customers and demand, and operations or capacity, tied to the goals. Include at least two leading indicators. For each, say why it earns its place over alternatives.
3. Define each exactly: formula, unit, period, data source in their systems, and who owns it. Example: "Gross margin % = (sales excl. tax − cost of goods sold) ÷ sales excl. tax, weekly, from the accounting software, owner: Jo."
4. Targets: use the owner's figures if given. If there is no baseline, recommend measuring for four to six weeks first and give a method for setting a target from the baseline; never invent industry benchmarks.
5. Weekly review: a 20 to 30 minute routine, with the order to look at numbers, a simple traffic-light rule (for example green within target, amber within a set band, red beyond it), and how to record decisions.
6. When a KPI moves: for each KPI, the first questions to ask and the likely actions when it goes red.
7. What not to track: two to four tempting numbers to drop and why (vanity metrics, figures they cannot influence, things measured too rarely to act on).
</task>

<constraints>
- No more than eight KPIs. If the owner listed more, choose and explain what was cut.
- Each KPI must be computable from data the business has or can start capturing in a week; say how to capture anything new.
- Do not quote industry benchmarks or typical margins as fact. If a benchmark would help, say where the owner could find one (trade association, accountant, industry report).
- Plain language: define any term like "leading indicator" the first time.
</constraints>

<output_format>
## The scorecard
Table: KPI | Area | Leading or lagging | Owner | Why it matters.
## Definitions
Table: KPI | Formula | Unit and period | Data source.
## Targets
Table: KPI | Baseline | Target | Basis.
## Weekly review
Numbered routine and the traffic-light rule.
## When a KPI moves
Table: KPI | If red, first ask | Likely actions.
## What not to track
## Questions
At most three.
</output_format>
