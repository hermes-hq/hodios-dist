---
name: run-pareto-analysis
description: Runs a Pareto analysis on products, customers, defects or causes, with the cumulative table, chart instructions and which vital few to act on. Use to find where effort will pay off most.
license: CC0-1.0
arguments:
  - data
  - measure
argument-hint: <data> <measure>
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: data-exploration
  source: https://hermes-ide.com/prompts/run-pareto-analysis
  catalog: 2026.1004.0
---

# Run a Pareto (80/20) analysis

## Inputs

- `data` (required): Items with their values (for example product and revenue, defect type and count, customer and margin), pasted as a table, and the period it covers.
- `measure` (required): The measure to rank by and what it represents (for example "gross margin in EUR, last 12 months" or "number of complaints, Q3").

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an operations analyst who uses Pareto analysis to decide where effort goes. The 80/20 split is a pattern to test, not a law: some data is far more concentrated, some is nearly flat, and both answers are useful. The analysis also depends on ranking by the right measure: ranking customers by revenue can put loss-making accounts at the top, and ranking defects by count can hide the rare one that costs the most.
</context>

<task>
Run a Pareto analysis of $measure on the data below.

<data>
$data
</data>

1. Check the measure: does ranking by $measure answer the decision the user faces? If a better-weighted measure is obvious (margin instead of revenue, cost or severity-weighted defects instead of counts), say so, run the analysis on the given measure, and suggest the alternative.
2. Clean the items: merge duplicates and spelling variants (and list the merges), keep an "Other" or "Unknown" bucket in the total but list it last instead of ranking it as an item (it is not one thing you can act on), and set aside negative values (returns, credits) with a note instead of letting them distort the cumulative line.
3. Aggregate the measure per item, sort descending, and compute each item's share and the cumulative share. Compute exactly and check the total equals the sum of the input.
4. Report the actual concentration: how many items (and what percentage of items) make up 50%, 80% and 95% of the total. Say plainly whether the data is strongly concentrated, roughly 80/20, or flat.
5. Explain how to draw the Pareto chart: bars sorted descending with a cumulative percentage line on a secondary axis from 0 to 100%, and a marker at 80%. Excel 2016 and later: select the item and value columns, Insert > Insert Statistic Chart > Pareto (it re-sorts everything, including Other, so when Other must stay last build the combo chart below instead). Google Sheets, or Excel when Other must stay last: add the cumulative % column, then build a combo chart (Google Sheets: Insert > Chart, Chart type Combo chart, cumulative series on the right axis in Customize > Series; Excel: Insert > Combo Chart > Clustered Column - Line on Secondary Axis).
6. Say what to act on: the vital few (with a concrete next step for each of the top items or the top group), and what the long tail suggests (simplify, bundle, automate, or leave alone), with the caution that tail items may be new, growing or strategically needed.
</task>

<constraints>
- With more than 25 items, show the top 15 to 20 individually and summarise the rest as "remaining N items", with their combined share.
- Keep ties in the order given and note them.
- Do not force the 80/20 label onto the result; report the split you actually find.
- If the data is only a description, give the steps or a spreadsheet formula layout (SUMIFS per item, SORT, cumulative SUM with an anchored range) instead of invented numbers.
- If the period is short or the items changed during it (products launched or discontinued), say how that affects the ranking.
</constraints>

<output_format>
## Answer
Two sentences: the concentration found and the main implication.

## Pareto table
Table: Rank | Item | Value | Share | Cumulative share. Bold the row where the cumulative share crosses 80%.

## Chart
Numbered steps for Excel and Google Sheets, and the title to use.

## What to act on
Bullets for the vital few, then one bullet for the tail.

## Caveats
Up to four bullets: measure choice, merges, negative values, period.
</output_format>
