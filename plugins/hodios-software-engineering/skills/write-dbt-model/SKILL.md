---
name: write-dbt-model
description: Writes a dbt model from business logic, with declared sources, a stated grain, unique, not_null and relationships tests, column docs and a safe incremental strategy. Use when adding a dbt model.
license: CC0-1.0
arguments:
  - business_logic
  - source_tables
  - materialization
argument-hint: <business_logic> <source_tables> [materialization]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data
  source: https://hermes-ide.com/prompts/write-dbt-model
  catalog: 2026.1003.2
---

# Write a dbt model

## Inputs

- `business_logic` (required): What the model should contain in business terms, including definitions such as what counts as an active customer or a completed order.
- `source_tables` (required): The source or upstream model names with their columns and types, plus the warehouse (Snowflake, BigQuery, Postgres, Databricks, Redshift…) if known.
- `materialization` (optional; one of: view, table, incremental; default: table): How dbt builds the model.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
dbt models go wrong in quiet ways. A join fans out and nobody notices because no test pins the grain. A table name is hardcoded instead of using `ref` or `source`, so lineage and environments break. Business terms are implemented the way the author guessed. An incremental model filters on `max(updated_at)` with no lookback, so late-arriving rows are lost forever. Good dbt code states its grain, tests it, documents its columns and makes incremental loads safe to rerun.
</context>

<task>
Write a dbt model, materialised as $materialization, for this logic:
$business_logic

Sources and upstream models:
$source_tables

1. State the grain as "one row per …" and the key that enforces it. If the business logic leaves the grain or a definition open, ask, or state the assumption and put it in Open questions.
2. Declare sources in a sources YAML file with `loaded_at_field` and freshness thresholds where a load timestamp exists. Reference upstream data only through `source()` and `ref()`.
3. Add staging models only where a source needs renaming, casting or deduplication, one per source, following the project convention (`stg_<source>__<table>` if unknown).
4. Write the model SQL as import CTEs, then logical CTEs, then a final `select` with an explicit column list. Handle nulls and duplicates in the sources explicitly, and note any time zone conversion.
5. If materialised as incremental: set `unique_key`, choose `incremental_strategy` for the warehouse (merge where supported, otherwise delete+insert or insert_overwrite; check whether the project's dbt version supports microbatch), filter new rows inside `is_incremental()` with a lookback window for late-arriving data, set `on_schema_change`, and say when a full refresh is needed.
6. Write a properties YAML file with the model and column descriptions and tests: `unique` and `not_null` on the key (or a combination-of-columns test for a composite key, naming the package it needs), `relationships` for foreign keys, `accepted_values` for categorical columns, and one singular test for the most important business rule. Use the `data_tests:` key on dbt 1.8 or later and `tests:` before that; if the project is on 1.8 or later and the rule is easier to show with fixed input rows, write a dbt unit test instead.
7. Give the commands to build and test the model and its children, and a query that checks the grain.
</task>

<constraints>
- Use only columns listed in the sources. If the logic needs a column that is not there, list it under Open questions instead of inventing it.
- Keep SQL portable unless the warehouse is known. Flag any warehouse-specific function you use.
- No `select *` in the final CTE. Keep Jinja to what the model needs.
- Follow the project's naming and folder conventions if they are visible in the input.
</constraints>

<output_format>
## Assumptions and grain
The grain statement, the key, and each assumption.

## Files
Each file in its own fenced block, preceded by its path (for example `models/marts/fct_orders.sql`, `models/marts/_marts__models.yml`, `models/staging/_sources.yml`).

## Run and verify
Commands, the grain-check query, and what a passing result looks like.

## Open questions
Definitions or columns that need confirmation.
</output_format>
