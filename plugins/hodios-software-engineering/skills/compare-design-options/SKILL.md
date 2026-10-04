---
name: compare-design-options
description: Compares two to four technical options against the criteria that matter, weighs reversibility and risk, and recommends one. Use when a team is stuck choosing between approaches or tools.
license: CC0-1.0
arguments:
  - problem
  - options
  - criteria
  - constraints
argument-hint: <problem> [options] [criteria] [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: architecture
  source: https://hermes-ide.com/prompts/compare-design-options
  catalog: 2026.1004.2
---

# Compare design options

## Inputs

- `problem` (required): The problem to solve and why a choice is needed now.
- `options` (optional): The options on the table. Leave empty to propose up to three.
- `criteria` (optional): What matters most for this decision, ideally in priority order (for example time to ship, cost, team skills, latency).
- `constraints` (optional): Hard limits any option must meet (budget, deadline, compliance, existing systems).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Teams lose weeks debating options in the abstract. A useful comparison fixes the criteria first, judges every option against the same criteria, separates hard constraints from preferences, and says what evidence would settle the remaining doubt. The result should be ready to turn into an architecture decision record.
</context>

<task>
Problem: $problem
Only if options was provided: 
Options:
$options
Only if criteria was provided: 
Criteria that matter, most important first:
$criteria
Only if constraints was provided: 
Hard constraints:
$constraints

1. If no options were given, propose two or three realistic ones. Always consider keeping the current approach or doing nothing when that is viable.
2. If no criteria were given, derive at most six from the problem and say that you derived them. Put hard constraints first: an option that breaks one is out, with the reason.
3. Judge each option against each criterion as strong, adequate or weak, with a one-line reason specific to this problem.
4. For each option, state how hard it is to reverse later (two-way door or one-way door), the biggest risk, and the cost of being wrong.
5. Recommend one option. If the decision hinges on an unknown, recommend the cheapest experiment that would settle it and the option to pick if the experiment is not possible.
</task>

<constraints>
- Compare at most four options.
- No numeric scores or weighted sums unless the user supplied weights. Qualitative ratings with reasons are more honest than false precision.
- Do not invent benchmarks, prices, product limits or licence terms. When a choice depends on one, say what to check and where.
- Treat every option fairly: each gets its real strengths and real weaknesses, including the recommended one.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Recommendation
Two to four lines: the option, the main reason, and the main cost of choosing it.
## Criteria
Numbered, hard constraints first.
## Comparison
Table: one row per criterion, one column per option, each cell "strong, adequate or weak: reason".
## Options in detail
One short subsection per option: reversibility, biggest risk, cost of being wrong.
## What would change the recommendation
Bullets: the facts or measurements that would flip it.
## Open questions
Bullets, or "None".
</output_format>
