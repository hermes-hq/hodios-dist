---
name: write-rfc
description: Drafts a technical RFC or design proposal with a clear problem, goals and non-goals, the proposed design, honest alternatives and open questions. Use before building something others must agree on.
license: CC0-1.0
arguments:
  - proposal
  - context
  - template
argument-hint: <proposal> [context] [template]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: writing
  source: https://hermes-ide.com/prompts/write-rfc
  catalog: 2026.1002.1
---

# Write an RFC

## Inputs

- `proposal` (required): What you want to propose, in rough notes. Include the problem, the idea and any constraints you know.
- `context` (optional): Background readers need, such as the current system, data, incidents, or links to earlier discussions.
- `template` (optional): Your organisation's RFC template, if it has one. Its headings replace the default ones.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
An RFC exists to get a decision from people who were not in the author's head: reviewers need to agree that the problem is real, that the proposal solves it, and that the obvious alternatives were weighed fairly. RFCs fail when the problem is assumed rather than shown, when non-goals are missing so scope creeps in review, and when alternatives are straw men. The draft should make disagreement easy to express, through explicit assumptions and open questions.
</context>

<task>
Draft an RFC from these notes:
<notes>
$proposal
</notes>
Only if context was provided: 
Background:
<background>
$context
</background>
Only if template was provided: 
Use this template's headings and fill each one:
$template

1. State the problem with the evidence in the notes (incidents, metrics, user reports, cost). If there is no evidence, write the problem as an assumption and add a question asking for data.
2. Write goals as outcomes that can be checked, and non-goals that name the nearby things this proposal will not do.
3. Describe the proposal in enough detail to review: components, data flow, interfaces or schemas, failure behaviour, security and privacy impact, and cost. Use a short diagram in text or Mermaid only if it clarifies the data flow.
4. Give at least two real alternatives, including "do nothing", each with its strongest honest case and the specific reason it loses.
5. List risks and drawbacks of the proposal itself, with mitigations.
6. Describe rollout: phases, migration, feature flags, how to measure success and how to roll back.
7. Collect open questions, each addressed to the people or team who can answer it, if known.
</task>

<constraints>
- Never invent numbers, incidents, costs, team names or deadlines. Write `[needs data: ...]` where a figure is missing.
- Keep the author's proposal. If you see a serious flaw, say so under Risks or Open questions rather than quietly designing something else.
- Separate facts from the notes and your inferences; mark assumptions as assumptions.
- Aim for something a reviewer can read in 10 minutes. Cut background that does not change the decision.
</constraints>

<output_format>
Markdown with a title line, a status line (`Status: Draft`), then the sections: Summary (three sentences at most), Problem, Goals and non-goals, Proposal, Alternatives considered, Risks and drawbacks, Rollout, Open questions.
After the RFC, a short list "Missing before review" naming the data or decisions the author still has to supply.
</output_format>
