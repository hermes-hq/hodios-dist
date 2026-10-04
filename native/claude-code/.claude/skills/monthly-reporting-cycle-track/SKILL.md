---
name: monthly-reporting-cycle-track
description: Runs a monthly reporting cycle in gated steps from data pull and quality checks to metric calculation, variance commentary, review with metric owners and distribution.
license: CC0-1.0
arguments:
  - report
  - sources
  - deadline_day
argument-hint: <report> <sources> [deadline_day]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: reporting
  source: https://hermes-ide.com/prompts/monthly-reporting-cycle-track
  catalog: 2026.1004.1
---

# Monthly reporting cycle track

## Inputs

- `report` (required): What is reported, to whom and in what form, for example "operations KPI pack for the leadership team - 12 metrics, slides plus a spreadsheet".
- `sources` (required): The systems or files each metric comes from, their owners, and when the month's data are complete.
- `deadline_day` (optional; default: 5): The working day of the new month by which the report must be distributed.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs one month's cycle for this report, due by working day $deadline_day:

<report>
$report
</report>

Each step produces one artifact and stops for approval; later steps build on the approved artifacts. Start by laying out the working-day schedule back from day $deadline_day, with the owner of each step.

Rules for every step: use only data, query results and notes the user supplies, and never invent a number, a driver or an owner's explanation; when you cannot run a query, give it and continue from the pasted output. Keep a cycle log of issues, fixes and decisions, and carry unresolved items forward to next month's cycle. If a gate is skipped, note it in the log and continue.

## Steps

Work through these steps in order. Do not skip a gate.

1. pull (operate)
2. quality (verify)
3. metrics (build)
4. commentary (build)
5. owner-review (review)
6. distribute (ship)

### Step 1: Data pull

<sources>
$sources
</sources>

1. For each metric, list the source, the query or export, the owner and the time the month's data are complete (late-arriving data, month-end close).
2. Pull or ask the user to pull a snapshot after that time, and record the extraction timestamp and row counts for each source.
3. Note any source not yet complete and the risk to the day $deadline_day deadline.

Write sections: Source register (table: Metric | Source | Owner | Complete when | Extracted at | Rows), Late or missing data. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 2 (quality).

### Step 2: Quality checks

Before calculating anything, check the snapshot:

1. Completeness: every day and segment present; row counts against last month and the same month last year, flagging changes beyond a stated tolerance.
2. Reconciliation: totals against an independent figure (finance ledger, source system screen, last report's restated value).
3. Validity: nulls in key fields, duplicates, out-of-range or negative values, unexpected new categories.
4. Definitions: any change in source logic, product codes, regions or tracking since last month.

For each issue: its size, its likely effect on the metrics, and the fix (correct, exclude, footnote, or escalate to the owner). Write sections: Checks run (with real results), Issues, Fitness for reporting. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 3 (metrics).

### Step 3: Metric calculation

1. Calculate each metric with its documented definition, from the checked data.
2. Show each against last month, the same month last year and the target or budget, with absolute and percentage change.
3. Apply the agreed thresholds (or propose them) to mark metrics as on track, watch or off track, and flag any movement larger than usual variation.
4. Recalculate any restated prior month and say why it changed.

Write sections: Metrics table (Metric | This month | Last month | Same month last year | Target | Status), Restatements, Flags for commentary. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 4 (commentary).

### Step 4: Variance commentary

For each flagged metric:

1. Decompose the change into its drivers where the data allow (volume, rate, mix, price, one-offs, calendar effects such as working days).
2. Write commentary in the form: what happened, by how much, why (labelled as confirmed by data or awaiting the owner), and what happens next.
3. Draft a question for the metric owner wherever the cause is not visible in the data.

Write sections: Commentary by metric, Questions for owners. Do not state a cause as confirmed unless the data show it. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 5 (owner-review).

### Step 5: Review with metric owners

1. Prepare a short review pack per owner: their metrics, the draft commentary and the questions.
2. When the user pastes owners' replies, update the commentary, marking each explanation with its source, and log disagreements about the numbers with how they were resolved.
3. Record each owner's sign-off, or the open item blocking it, and the consequence for the deadline.

Write sections: Owner packs, Changes after review, Sign-off status. Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 6 (distribute).

### Step 6: Distribution

1. Final checks: numbers in the narrative match the table, dates and period labels are right, charts use the agreed scales, and the methodology note and known caveats are attached.
2. Write the distribution message: headline points, where the report lives, the version, and who to contact.
3. Archive the snapshot, queries, the cycle log and the final report with a version label.
4. Write a short retrospective: what slowed the cycle, issues to fix before next month, and items carried forward.
