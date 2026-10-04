---
name: dashboard-build-track
description: Builds a dashboard in gated steps from decisions and users to metric definitions, data checks, a wireframe, a build spec and a QA and adoption review. Use when a dashboard must be trusted and used.
license: CC0-1.0
arguments:
  - purpose
  - data_sources
  - tool
argument-hint: <purpose> [data_sources] [tool]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: data-visualization
  source: https://hermes-ide.com/prompts/dashboard-build-track
  catalog: 2026.1004.0
---

# Dashboard build track

## Inputs

- `purpose` (required): Why the dashboard is needed, in the requester's words - who asked, for which meeting or decision, and what they do today without it.
- `data_sources` (optional): The data available (systems, tables or files, key columns, grain, refresh frequency, known quality issues). Leave empty if still unknown; step 1 will list what is needed.
- `tool` (optional; default: the team's existing BI tool): The BI or spreadsheet tool the dashboard will be built in (for example Power BI, Tableau, Looker Studio, Metabase, Excel, Google Sheets).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Builds the dashboard behind "$purpose" in $tool as a strong BI team would: agree the decisions and users, define every metric, prove the data, sketch the layout, write a build spec, then QA it and plan adoption. Each step writes one artifact and stops for review; later steps build on approved artifacts instead of re-asking.

Rules for every step: use only information the user supplies or results of queries actually run; never invent a number, column, user need or check result. When a query cannot be run, give it, ask for the output and continue from it. Label assumptions and keep a running log of them. Every tile must trace to a decision approved in step 1. If asked to skip steps or approvals, keep a compressed version of the decisions and metric definitions anyway, confirm once that later steps rest on unreviewed choices, then continue and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. decisions (discover)
2. metrics (plan)
3. data-checks (verify)
4. wireframe (design)
5. build-spec (build)
6. qa-adoption (review)

### Step 1: Decisions and users

<purpose>
$purpose
</purpose>

<data_sources>
$data_sources
</data_sources>

1. Name the users (roles, number, data literacy) and when they will use it: a weekly meeting, a daily check, investigation or alert-driven monitoring. Mark inferences as assumptions.
2. List at most five decisions, each as "When <user> sees <signal>, they <action>." Requests that support no decision go under Out of scope.
3. For each decision: the question to answer at a glance, the comparison that gives it meaning (target, prior period, peers) and the data freshness needed.
4. Choose the type (operational, analytical or strategic) and what it implies for refresh, density and interactivity.
5. List up to five questions for the requester, most design-changing first.

Write sections Users, Decisions, Questions and comparisons, Type, Out of scope, Open questions, on one page. Stop and wait for approval.

Save this step's result to `dashboard-build/01-decisions.md`.

**Gate:** stop here and wait for the user's approval before step 2 (metrics).

### Step 2: Metric definitions

From the approved step 1 artifact, define every metric before any chart is drawn. Drop metrics that serve no approved question.

For each metric write a card: display name and plain meaning; formula (ratios as a ratio of totals, not an average of row ratios); grain and aggregation; filters and exclusions (test accounts, refunds, internal users) and time zone; window and comparison; target and owner if needed; source fields (from $data_sources, or "to confirm"); edge cases (late data, currency, restated history).

Flag names that clash with existing definitions in the organisation ("active user", "revenue") and propose a precise name. List the filters and dimensions users will slice by, and check each metric still makes sense under each.

Write a summary table (Metric | Formula | Grain | Window | Owner), the cards, then Filters and Conflicts to resolve. Stop and wait for approval.

Save this step's result to `dashboard-build/02-metrics.md`.

**Gate:** stop here and wait for the user's approval before step 3 (data-checks).

### Step 3: Data checks

From the approved metric cards, prove the data can produce each metric.

1. Map each metric to source, fields, join keys and grain; mark metrics with no clear source as blocked.
2. Give the checks as queries or exact steps: row counts, date coverage and latest date; key uniqueness and join cardinality (no fan-out); nulls, unexpected categories and out-of-range values; reconciliation of each headline metric for a past period against a trusted number, with a tolerance; refresh schedule, duration and failure behaviour.
3. Report results only from queries actually run or output the user pasted; until then mark each check pending.
4. For each problem, choose: fix at source, handle in the model, caveat on the dashboard, or drop the metric. Confirm the refresh meets each decision's freshness need.

Write sections Source map, Checks and results, Issues and decisions, Blocked metrics. Stop and wait for approval.

Save this step's result to `dashboard-build/03-data-checks.md`.

**Gate:** stop here and wait for the user's approval before step 4 (wireframe).

### Step 4: Wireframe

From the approved artifacts, sketch the layout before building in $tool.

1. Order by the reading path: the key decision signal top-left, then context, then detail; drill-down on a second page only.
2. Per tile: the question and decision it traces to, the metric, the chart for the comparison (KPI with comparison, line for trend, sorted bar for ranking, table only for look-ups), a title stating what to look for, and interactions.
3. Put global filters in one place and list the tiles each applies to.
4. Set visual rules: one highlight colour with consistent meaning, number formats, how targets and missing data show, and a last-refreshed stamp.
5. Draw a text grid of the page and note the viewing screen. Over about ten tiles on a page, propose cuts.

Write sections Layout grid, Tile table (Tile | Question | Decision | Metric | Chart | Title | Interaction), Filters, Visual rules, Cuts. Stop and wait for approval.

Save this step's result to `dashboard-build/04-wireframe.md`.

**Gate:** stop here and wait for the user's approval before step 5 (build-spec).

### Step 5: Build spec

From the approved artifacts, write a spec someone can build in $tool without further questions.

1. Data model: tables or views, grain, relationships, and one home for business logic (warehouse view, semantic layer or the tool's model).
2. Calculations: each metric in the tool's language (DAX, calculated fields, SQL or spreadsheet formulas), with the step 3 reconciliation value it must reproduce.
3. Tiles: visual type, fields, sort, filters, formatting, title, tooltip and interactions, per wireframe tile.
4. Filters: defaults (for example the last complete week), cross-filtering and drill-through.
5. Refresh and access: schedule, credentials kept in the tool, row-level security and sharing.
6. Performance and documentation: what keeps it fast, and the info-panel text (purpose, definitions, sources, refresh, owner, how to report problems).

Use code blocks for formulas and queries. Stop and wait for approval.

Save this step's result to `dashboard-build/05-build-spec.md`.

**Gate:** stop here and wait for the user's approval before step 6 (qa-adoption).

### Step 6: QA and adoption review

From the approved artifacts, check the built dashboard and plan its use.

1. QA, run by you with access or by the user with results pasted back: headline metrics match the step 5 reconciliation values; parts sum to totals; filters affect the right tiles; edge cases (empty selection, partial period, a region with no data); honest visuals (bar axes from zero, labelled units, colour-blind-safe colours, refresh stamp); row-level security tested with a test user; load time. Mark each pass, fail or not checked, never pass without evidence.
2. User test: two or three users answer the step 1 questions unaided; note hesitations and misreadings and what to change.
3. Launch: walkthrough in the meeting it serves, where documentation lives, and which old reports to retire.
4. Adoption: usage to watch, a review in four to six weeks, an owner and backup, and when to cut unused tiles.

Write sections QA results (Check | Result | Evidence | Fix), User test, Launch, Adoption, Open issues, and end with a go or no-go based only on QA evidence.

Save this step's result to `dashboard-build/06-qa-adoption.md`.
