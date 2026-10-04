---
name: dataset-cleaning-track
description: Cleans a dataset with a repeatable script in gated steps, profiling, proposing rules, applying and validating them, and exporting with an auditable cleaning log. Use for data that will be reused.
license: CC0-1.0
arguments:
  - input_path
  - output_format
  - rules
argument-hint: <input_path> [output_format] [rules]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: data-exploration
  source: https://hermes-ide.com/prompts/dataset-cleaning-track
  catalog: 2026.1004.2
---

# Clean a dataset with a scripted, auditable pipeline

## Inputs

- `input_path` (required): Path to the raw data file or folder in the project (CSV, Excel, JSON, Parquet).
- `output_format` (optional; one of: csv, parquet, xlsx; default: csv): Format of the cleaned file.
- `rules` (optional): Known business rules and definitions, for example "order_id is unique; amounts are in EUR cents; region must be one of EMEA, AMER, APAC; test accounts have emails ending in @example.com". Without them, problems are flagged rather than dropped.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Turns the raw data at `$input_path` into a clean $output_format file through a script anyone can rerun, with a log that says what changed, why and how many rows each rule touched. Cleaning by hand, or with a script that silently drops rows, produces numbers no one can defend later. Here every rule is proposed with evidence, approved before it removes anything, applied in code from the untouched raw file, and checked by validations that run with the pipeline.

Rules for every step:
- Never modify the raw file. Read it, and write everything else to a separate output folder.
- Every count in an artifact comes from code that ran. Do not estimate.
- Dropping rows or overwriting values requires an approved rule. Without one, add a flag column and leave the decision to the user.
- Use the language and libraries the project already uses (for example Python with pandas or Polars, or R with the tidyverse); otherwise ask, defaulting to Python.
- Do not print personal data into artifacts; refer to rows by key or row number.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Before saying the work is done, run the check that proves it (tests, build, type check or the command the user gave) and report the real result.
- If you could not run a check, say so plainly and say which one.

## Steps

Work through these steps in order. Do not skip a gate.

1. profile (discover)
2. propose-rules (plan)
3. apply (build)
4. validate-export (verify)

### Step 1: Profile the raw data

1. Load `$input_path` read-only, checking encoding, delimiter, header rows, sheet names and footer rows. Record exactly how it was read.
2. Profile every column: inferred type vs intended type, missing count and share (including disguised missing values like "", "N/A", "-", 0 or 1900-01-01), distinct count, top values, min and max, and examples of values that fail the intended type.
3. Look for structural problems: duplicate rows and duplicate keys, inconsistent category spellings and case, mixed date formats and time zones, units mixed in one column, numbers stored as text with thousands separators or currency symbols, leading and trailing spaces, outliers beyond plausible ranges, and rows that break cross-column logic (end before start, totals that do not add up).
4. Write the profiling code as the first part of the pipeline script, so the profile can be regenerated.

Write the artifact: How it was read, Shape, Column profile (Column | Intended type | Missing | Distinct | Range or top values | Problems), Structural problems with counts. Continue to step 2.

Save this step's result to `cleaning/01-profile.md`.

### Step 2: Propose cleaning rules

<business_rules>
$rules
</business_rules>

1. For each problem from step 1, propose a rule: what it matches, the action (standardise, convert, impute, flag, drop), the evidence that justifies it, and how many rows and values it affects.
2. Turn the business rules above into checks and actions. When a business rule conflicts with what the data shows (for example a "unique" key with duplicates), do not resolve it silently: show the conflict with counts and examples by key, and propose options.
3. Prefer reversible actions: standardise and flag rather than drop; keep the original value in a column when overwriting matters; never impute values that will be used as if observed without a flag column.
4. Order the rules so each one sees the output of the previous one, and note the dependencies.
5. List the validation checks the clean data must pass: types, allowed values, ranges, uniqueness, not-null, cross-column logic, and row count reconciliation.

Write the artifact: Rules (No. | Problem | Rule | Action | Evidence | Rows affected), Conflicts needing a decision, Validation checks. Stop and wait for approval.

Save this step's result to `cleaning/02-rules.md`.

**Gate:** stop here and wait for the user's approval before step 3 (apply).

### Step 3: Apply the rules in a pipeline

1. Implement each approved rule as its own named function or step in the script, in the approved order, reading from the raw file every run.
2. After each rule, log the number of rows in and out and values changed, to a structured log the script writes.
3. Keep removed rows in a separate file with the rule that removed them.
4. Make the script deterministic and idempotent: fixed sort orders, explicit types, no dependence on the current date unless parameterised, the same output on every run.
5. Implement the validation checks from step 2 as code that runs at the end of the pipeline and fails loudly when a check fails.

Continue to step 4.

### Step 4: Validate, export and write the log

1. Run the pipeline end to end from the raw file. All validation checks must pass; if one fails, report it and do not export.
2. Run it a second time and confirm the output is identical (compare a checksum or the data).
3. Reconcile counts: raw rows minus each rule's removals equals the final rows.
4. Spot-check five rows by key from raw to clean, including rows touched by the riskiest rules.
5. Export the clean data as $output_format with explicit types preserved as far as the format allows (dates as dates, ids as text so leading zeros survive), and write a data dictionary for the clean columns.

Write the cleaning log:

#### Inputs and outputs
Raw file, how it was read, output files, and the command that rebuilds them.

#### Rules applied
Table: Rule | Action | Rows affected | Values changed.

#### Row reconciliation
Raw rows through each step to final rows.

#### Flags left for review
Table: Flag | Count | Meaning.

#### Validation
Each check with its real result, and the rerun comparison.

#### Data dictionary
Where it is, and a summary of derived and flag columns.

Save this step's result to `cleaning/04-cleaning-log.md`.
