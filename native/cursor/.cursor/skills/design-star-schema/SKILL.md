---
name: design-star-schema
description: "Designs a dimensional model from the questions analysts need answered: business processes, grain, facts, dimensions, slowly changing dimension types and DDL. Use when building a warehouse layer."
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: data
  source: https://hermes-ide.com/prompts/design-star-schema
  catalog: 2026.1004.3
---

# Design a star schema

## Inputs

- [BUSINESS_QUESTIONS] (required): The questions analysts need answered, verbatim, with the filters and breakdowns they use.
- [SOURCE_TABLES] (required): The operational tables available, with columns, keys and how history is kept (overwritten, audit table, snapshots).

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A dimensional model is judged by whether analysts can answer their questions correctly with simple joins. Models fail when the grain is never stated, so facts at different grains share a table and sums double count; when ratios or balances are stored as if they could be summed; when a dimension attribute that changes over time is overwritten, so last year's revenue moves to this year's region; and when each fact table has its own private version of customer or product, so results cannot be compared. Kimball's sequence still works: pick the business process, declare the grain, choose the dimensions, then the facts.
</context>

<task>
Questions to answer:
[BUSINESS_QUESTIONS]

Source tables:
[SOURCE_TABLES]

1. Identify the business processes behind the questions (ordering, shipping, billing, support, sign-ups…). Each process becomes at least one fact table.
2. For each fact table, declare the grain in one sentence at the most atomic level the sources support, and choose its type: transaction, periodic snapshot (for balances and levels over time), accumulating snapshot (for pipelines with milestones), or factless (for events or coverage with no measure).
3. List each fact's measures and classify them as additive, semi-additive (balances: summable across some dimensions but not across time) or non-additive (ratios and percentages: store the numerator and denominator instead).
4. Design the dimensions: surrogate keys, natural keys, attributes, conformed dimensions shared across facts, a date dimension (and time of day if needed), role-playing dates (order date, ship date), degenerate dimensions such as an order number, junk dimensions for leftover flags, and bridge tables for many-to-many relationships.
5. Choose a slowly changing dimension type for each attribute that can change: type 0 (never changes), type 1 (overwrite, history not needed) or type 2 (new row with valid_from, valid_to and is_current). Justify each choice by a question that needs, or does not need, history.
6. Plan for unknown and late-arriving members: a default "unknown" row in each dimension, and inferred members that are updated when the dimension row arrives.
7. Map every business question to the tables that answer it, with a query sketch. Flag any question the sources cannot answer and what data would be needed.
8. Write the DDL.
</task>

<constraints>
- Do not invent source columns. If a question needs data the sources lack, put it under Source gaps.
- Write portable ANSI-style DDL unless the warehouse is named. Note warehouse-specific choices such as clustering or partitioning separately.
- Prefer one wide dimension to snowflaked sub-dimensions unless the input gives a reason to normalise.
- If the questions are too vague to fix a grain, ask before designing.
</constraints>

<output_format>
## Business processes and grain
One line per fact table: process, grain sentence, fact table type.

## Bus matrix
Table: fact tables as rows, conformed dimensions as columns, marked where used.

## Fact tables
Per table: keys, degenerate dimensions, measures with additivity.

## Dimensions
Per table: keys, attributes with their SCD type, and the unknown member.

## DDL
One fenced SQL block.

## Question coverage
Table: question | tables | query sketch.

## Source gaps
Questions or attributes the sources cannot support, and what would fix it.

## Open questions
Only those that would change the grain or an SCD choice.
</output_format>
