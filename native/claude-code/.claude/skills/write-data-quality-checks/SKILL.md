---
name: write-data-quality-checks
description: Writes data-quality checks for a table (freshness, volume, schema, validity, uniqueness, referential integrity, distribution) with severities, thresholds and owners. Use when a table feeds decisions.
license: CC0-1.0
arguments:
  - table
  - sample_rows
  - tool
argument-hint: <table> [sample_rows] [tool]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data
  source: https://hermes-ide.com/prompts/write-data-quality-checks
  catalog: 2026.1002.0
---

# Write data-quality checks for a table

## Inputs

- `table` (required): The table name, its DDL or column list, what one row means, how and when it is loaded, and who uses it.
- `sample_rows` (optional): A few dozen representative rows, or summary statistics such as daily row counts and null rates.
- `tool` (optional; one of: sql, dbt, great-expectations, soda; default: sql): Where the checks will run.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most bad data is not a failed job. It is a job that succeeded with half the rows, a column that turned null after an upstream release, a duplicated load, or an enum value nobody had seen before. Useful checks cover the dimensions that catch these (freshness, volume, schema, validity, uniqueness, referential integrity, distribution and business rules), distinguish failures that must block publishing from ones that only warn, and route every alert to a named owner with a first action. A check nobody owns, or one that fires every day, gets muted and then protects nothing.
</context>

<task>
Write data-quality checks in $tool for this table:
$table
Only if sample_rows was provided: 

Sample or statistics:
$sample_rows

1. State the grain ("one row per …"), the key, the load cadence and the consumers. If the grain or cadence is unclear, ask, or state the assumption.
2. Write checks across these dimensions, skipping any that do not apply and saying why:
   - freshness: the newest load or event timestamp against the expected cadence;
   - volume: today's row count against the same weekday over recent weeks, as a ratio or z-score;
   - schema: expected columns and types;
   - validity: nulls in required columns, accepted values for categorical columns, numeric ranges, formats;
   - uniqueness of the key;
   - referential integrity: orphaned foreign keys;
   - distribution: drift in null rate, mean or percentiles, and category shares;
   - business rules across columns, such as end after start, or a total equal to the sum of its lines.
3. Give each check a severity: block (stop downstream publishing) or warn. Give a threshold derived from the sample where possible, or an explicit starting value marked to be tuned. Name an owner role or a placeholder, and give the first action on failure.
4. Implement the checks in $tool:
   - sql: one query per check that returns failing rows or a single failing metric, so zero rows means pass;
   - dbt: generic tests in properties YAML plus singular tests, naming any package a test needs;
   - great-expectations: an expectation suite using the GX Core 1.x API (say which version you assumed);
   - soda: SodaCL checks in YAML.
5. Explain how to tune thresholds after two to four weeks of history, and when to retire a check that never fires.
</task>

<constraints>
- Do not invent columns. Checks must reference only columns in the table definition.
- Avoid checks that will alert on normal variation. Weekly seasonality and month-end peaks belong in the threshold.
- Keep each check independent, so one failure does not hide another.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Table grain and assumptions
Grain, key, cadence, consumers, and assumptions.

## Checks
Table: check | dimension | severity | threshold | owner | first action on failure.

## Implementation
The code for $tool in fenced blocks, one per file.

## Tuning plan
How and when to adjust thresholds.

## Gaps
What these checks cannot catch, and what would.
</output_format>
