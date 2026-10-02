---
name: analysis-project-track
description: Takes a stakeholder request from question to analysis plan, data checks, analysis and a decision-ready report, pausing for review between steps. Use when an analyst takes on a request.
license: CC0-1.0
arguments:
  - question
  - data_description
  - audience
  - slug
argument-hint: <question> <data_description> [audience] [slug]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: workflow
  category: reporting
  source: https://hermes-ide.com/prompts/analysis-project-track
  catalog: 2026.1002.2
---

# Analysis project track

## Inputs

- `question` (required): The stakeholder's question or request, in their words, plus who asked and what they plan to do with the answer if you know.
- `data_description` (required): The data you have or can get (tables or files, columns, grain, date range, known issues), or the data itself.
- `audience` (optional; default: the stakeholder who asked): Who will read the final report and what they need from it (for example "VP Sales, wants a yes or no on extending the pilot").
- `slug` (optional; default: analysis): Short kebab-case name for the analysis, used for the folder the step artifacts are saved in.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs the analysis behind "$question" the way a senior analyst would: agree what decision the work serves and how it will be answered before touching data, prove the data can be trusted, run the analysis that the plan calls for, and write a report $audience can act on. Each step writes one artifact and stops for review, and later steps build on the approved artifacts instead of re-asking.

Rules for every step: work only from data the user supplies or results of code that was actually run in this session; never invent a number, a table, a column or a finding; when you cannot run code, give the exact query or script, ask the user to run it and paste the output, and continue from that output; label every inference as an inference; and keep a running list of assumptions and decisions so the report can state them honestly. If the user asks to skip the plan or the approvals, keep a compressed plan anyway (the decision, the metric definition and the comparison, in a few lines), because it decides what the answer means; confirm once that later steps will build on unreviewed choices, then continue without stopping and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. plan (plan)
2. data-checks (verify)
3. analysis (build)
4. report (build)

### Step 1: Frame the question and plan the analysis

Turn "$question" into an analysis plan the stakeholder can agree to before any work starts.

<data_description>
$data_description
</data_description>

1. State the decision this analysis informs, who makes it and by when. If the request does not say, propose the most likely decision and mark it as an assumption to confirm.
2. Rewrite the request as one primary question and at most three secondary questions, each answerable with data.
3. Define every metric precisely: formula, unit, grain, filters (for example excluding test accounts and refunds), time window and time zone.
4. Check the data against the questions: which tables or columns answer each one, what is missing, and whether the grain and history are enough.
5. Choose the method for each question (a comparison, a trend, a cohort, a segmentation, a test, a model) and the comparison that gives the number meaning (prior period, control group, target, benchmark).
6. Write the decision rule in advance: "If we find X, the recommendation is A; if Y, B." Name the result that would change the stakeholder's mind.
7. List the pitfalls that apply (seasonality, mix shifts, selection bias, small segments, causal claims from observational data) and how the plan guards against each.
8. List questions for the stakeholder, at most five, ordered by how much they change the plan.

Write the plan as Markdown with sections Decision, Questions, Metrics, Data, Method, Decision rule, Pitfalls, Open questions. Keep it to one page.

Stop and wait for approval.

Save this step's result to `analyses/$slug/01-plan.md`.

**Gate:** stop here and wait for the user's approval before step 2 (data-checks).

### Step 2: Check the data before trusting it

Work from the approved plan from step 1 (saved as `analyses/$slug/01-plan.md` when you can write files). Prove the data can answer the approved questions before running the analysis.

1. Profile each table the plan uses: row count, date range, grain (what one row is), primary key uniqueness, and the share of nulls in each column the plan needs.
2. Run these checks, as code or queries you execute, or that you give to the user to run if you cannot:
   - Completeness: gaps in dates, partial latest period, missing segments.
   - Uniqueness: duplicate keys, and whether each planned join is one-to-one or one-to-many (join fan-out inflates sums).
   - Validity: values out of range, negative amounts, future dates, categories outside the expected list, units and currencies.
   - Consistency: totals that should match a known source (a finance figure, a dashboard, last month's report) within a stated tolerance.
   - Definitions: whether each column means what the metric definition assumes (for example "created_at" in UTC or local time; "status" including cancelled orders).
3. For each issue found, record its size (rows or share affected), its likely effect on the answer (direction and rough size), and the fix: exclude, correct, impute, or caveat.
4. Say whether the data is fit for the plan as written. If not, propose the smallest change to the plan that still answers the decision.

Write the checks as Markdown with sections Tables, Checks run (with the code or query and the actual result), Issues, Fixes applied, Fitness for purpose. Report results only from output you actually saw.

Stop and wait for approval.

Save this step's result to `analyses/$slug/02-data-checks.md`.

**Gate:** stop here and wait for the user's approval before step 3 (analysis).

### Step 3: Run the analysis

Work from the approved plan and data checks from steps 1 and 2 (saved as `analyses/$slug/01-plan.md` and `02-data-checks.md` when you can write files). Run the approved method on the data as cleaned in step 2.

1. For each question in the plan, in order: the code or query, the actual result as a small table, and one sentence saying what it shows.
2. Put every number next to its comparison (prior period, control, target) and its size (absolute and relative change, with counts behind any rate).
3. Quantify uncertainty where it matters: confidence intervals or a test for differences, and minimum segment sizes below which you do not interpret results.
4. Check the obvious alternative explanations the plan listed (mix shift, seasonality, a change in tracking or definitions, one large customer) and record whether each holds.
5. Note anything surprising, and whether it changes the plan. Do not chase new questions without asking; list them instead.
6. Compare the results with the decision rule from step 1 and state which branch the evidence supports, and how strongly.

Write the analysis as Markdown with sections Results by question, Alternative explanations, Uncertainty, Decision rule outcome, New questions. Keep the code reproducible: fixed seeds, explicit filters, and the date the data was pulled.

Stop and wait for approval.

Save this step's result to `analyses/$slug/03-analysis.md`.

**Gate:** stop here and wait for the user's approval before step 4 (report).

### Step 4: Write the decision-ready report

Work from the three approved artifacts (the plan, the data checks and the analysis, saved in `analyses/$slug/` when you can write files). Write the report for $audience.

1. Open with the answer: one headline sentence that states the finding and the recommendation, then two or three supporting points with their numbers.
2. Give the recommendation and the decision it supports, with what would make you change it.
3. Show the evidence in the order the reader needs it: at most three charts or tables, each with a title that states the takeaway and a one-line note on how to read it. Describe each chart's type, data and annotation if you cannot produce the image.
4. State the caveats that a decision-maker must know (data issues from step 2, uncertainty from step 3, causal limits), each in one sentence with its likely effect on the conclusion. Leave the rest to an appendix.
5. List next steps with owners if known, including any follow-up analysis or experiment that would settle open questions.
6. Add an appendix: metric definitions, data sources and date pulled, method, and the assumption log.

Match the length and vocabulary to $audience: an executive gets one page and no jargon; an analytical audience can see the method. Use only numbers that appear in the approved artifacts.

Save this step's result to `analyses/$slug/04-report.md`.
