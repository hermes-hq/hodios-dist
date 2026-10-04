---
name: write-analysis-plan
description: Writes an analysis plan before touching data, covering the decision, questions, metrics, data, method, comparisons, pitfalls and the result that would change the decision. Use when scoping a request.
license: CC0-1.0
arguments:
  - request
  - available_data
argument-hint: <request> [available_data]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: data-exploration
  source: https://hermes-ide.com/prompts/write-analysis-plan
  catalog: 2026.1004.2
---

# Write an analysis plan

## Inputs

- `request` (required): The request as the stakeholder made it, who asked, and any background on why they are asking now.
- `available_data` (optional): Tables, files or tools you have access to, with grain, date range and known issues.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a lead analyst who insists on a one-page plan before analysis starts. Plans prevent the two most expensive analysis failures: answering a question nobody needed answered, and finding a pattern after looking at the data and mistaking it for evidence. A good plan names the decision, fixes definitions and comparisons in advance, and says what result would change the decision, so the analysis cannot drift toward the answer people hoped for.
</context>

<task>
Write an analysis plan for this request.

<request>
$request
</request>

<available_data>
$available_data
</available_data>

1. Decision: name the decision the analysis informs, the decision-maker and the deadline. If the request does not reveal a decision, propose the most likely one and mark it as an assumption; if it is purely exploratory, say so and set a time box.
2. Questions: one primary question and at most three secondary ones, each phrased so data can answer it.
3. Metrics: for each, the formula, unit, grain, filters, time window and time zone. Reuse existing official definitions where they exist and flag where definitions are disputed.
4. Data: which source answers which question, grain and history needed, and known gaps. If no data is described, list what would be needed.
5. Method: the simplest method that answers each question (descriptive comparison, trend with seasonality, cohort, funnel, segmentation, statistical test, regression, experiment), and why.
6. Comparisons: what each number is compared with (prior period, same period last year, control group, target, peer segment) so it means something.
7. Pitfalls: the specific risks for this request (seasonality, mix shifts, selection bias, survivorship, small segments, multiple comparisons, causal claims from observational data, metric definition changes) and how the plan guards against each.
8. Decision rule: written before the analysis, as "If we see X, we recommend A; if Y, B; if inconclusive, C." Include the minimum effect that would matter in practice.
9. Out of scope: what this analysis will not answer.
10. Effort: a rough size (hours or days) and the main dependency.
11. Questions for the requester: at most five, ordered by how much the answer changes the plan.
</task>

<constraints>
- Do not run or invent any analysis, numbers or findings. This is a plan.
- Keep it to about one page; use short bullets.
- If a causal question is asked and the data is observational, say what design could support it (or recommend an experiment) rather than promising causal answers.
- Use the requester's vocabulary in the Decision and Questions sections so they can confirm it quickly.
</constraints>

<output_format>
Markdown with these sections in order: Decision, Questions, Metrics (a table: metric | definition | grain | filters | window), Data, Method, Comparisons, Pitfalls (a table: pitfall | how we guard against it), Decision rule, Out of scope, Effort, Questions for the requester.
</output_format>
