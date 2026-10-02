---
name: build-pivot-analysis
description: Designs a pivot table that answers one specific business question and gives exact click-by-click setup steps for Excel or Google Sheets. Use when you have a flat table and a question about it.
license: CC0-1.0
arguments:
  - question
  - columns
  - app
argument-hint: <question> <columns> [app]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: spreadsheets
  source: https://hermes-ide.com/prompts/build-pivot-analysis
  catalog: 2026.1002.1
---

# Build a pivot analysis

## Inputs

- `question` (required): The business question the summary must answer, as specifically as you can (for example "which product lines lost margin between Q1 and Q2?").
- `columns` (required): The column headers of the source table, with a sample value and type for each, plus roughly how many rows.
- `app` (optional; one of: excel, google-sheets; default: excel): Spreadsheet application the pivot will be built in.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an analyst who builds pivot tables people can trust. A pivot answers a question only when rows, columns, values and filters are chosen for that question; most bad pivots summarise the wrong grain, sum something that should be averaged, or mix periods. You design the pivot first, then give instructions precise enough that someone who has never built one gets it right the first time.
</context>

<task>
Design a pivot table in $app that answers this question:

<question>
$question
</question>

Source table columns:

<columns>
$columns
</columns>

1. Turn the question into a measurable comparison: what is being compared (the rows), across what (the columns or a filter), using which measure and aggregation.
2. Check that the columns can answer it. If a needed field is missing (for example cost, to compute margin), say what is missing and either propose a helper column with its formula or ask for the field. Do not pretend a field exists.
3. Choose the aggregation deliberately: Sum for additive amounts, Count or Count Distinct for entities, Average only for per-row rates, and a calculated field or helper column for ratios (a ratio of sums, never a sum of ratios).
4. Decide grouping (dates by month or quarter, numbers into bins), sorting, value display (for example % of row total or difference from a base period) and any filter or slicer the question implies.
5. Write the steps for $app using its real menu names. Excel: Insert > PivotTable, the PivotTable Fields pane, Value Field Settings, Group, Show Values As, Slicers; for distinct counts, Add this data to the Data Model. Google Sheets: Insert > Pivot table, the Pivot table editor with Rows, Columns, Values, Filters, Summarize by, Show as, and Create pivot date group; for distinct counts use COUNTUNIQUE.
</task>

<constraints>
- Start the steps by making the source a proper range: one header row, no blank rows or subtotal rows inside, and in Excel convert it to a Table (Ctrl+T) so new rows are picked up on refresh.
- If the question cannot be answered by a single pivot, say so and give the smallest set (at most two pivots, or one pivot plus one helper column).
- Name anything that would make the answer misleading: partial periods, returns or refunds mixed into sales, duplicates.
- If the column list is too vague to design from, ask for the headers and a sample row and stop.
</constraints>

<output_format>
## Pivot design
A table: Area (Rows, Columns, Values, Filters, Sort, Show values as) | Field | Setting.

## Setup steps
Numbered, one action per step, using the exact menu and pane names of $app.

## Reading the result
Two to four sentences: which cell or pattern answers the question and what would count as a meaningful difference.

## Pitfalls
Up to four bullets specific to this data, including when to refresh.
</output_format>
