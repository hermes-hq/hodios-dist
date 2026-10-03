---
name: write-research-proposal
description: Writes a research or grant proposal section (aims, significance, approach, timeline) mapped to the funder's criteria, with placeholders instead of invented data. Use for grant or thesis proposals.
license: CC0-1.0
arguments:
  - project
  - funder_criteria
  - section
argument-hint: <project> [funder_criteria] [section]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/write-research-proposal
  catalog: 2026.1003.1
---

# Write a research proposal

## Inputs

- `project` (required): Your project notes: the problem, the question, your approach, preliminary results, team and resources. More detail gives a stronger draft.
- `funder_criteria` (optional): The funder's call text, review criteria, page or word limits and required headings, pasted as given.
- `section` (optional; one of: aims, significance, approach, full; default: full): Which part to write.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Reviewers score proposals against published criteria, often in a few minutes per section. Strong proposals make the problem and its stakes obvious in the first paragraph, state aims that are specific, measurable and independent (one failing aim does not sink the others), show the approach is feasible with preliminary evidence and named alternatives, and use the funder's own language so each criterion is easy to score. Weak ones are vague about aims, hide the hypothesis, promise too much for the timeline and leave reviewers to find the answer to each criterion themselves.
</context>

<task>
Write the "$section" section of a proposal for this project:
<project>
$project
</project>
Only if funder_criteria was provided: 
Funder call and review criteria:
<criteria>
$funder_criteria
</criteria>

1. Extract the review criteria, limits and required headings from the funder text. Without funder text, use the widely shared criteria of significance, innovation, approach, investigators and environment, and say so.
2. Write the requested part:
   - aims: an opening paragraph on the problem and the gap, the long-term goal, the objective of this proposal, the central hypothesis and its rationale, then two to four aims, each with a working hypothesis or objective, a one-line approach and the expected outcome, and a closing paragraph on the payoff.
   - significance: the problem's size and consequences, what is known and the specific gap, and what will change if the aims succeed, for the field and for people.
   - approach: per aim, the rationale, the design and methods, the analysis, expected results, potential problems with alternative strategies, and success benchmarks; then a timeline table by quarter or semester with milestones.
   - full: all of the above in the funder's order, within its limits.
3. Mirror the funder's terms in headings and key sentences so each criterion is visibly addressed.
4. Check feasibility: flag aims that the timeline, team or budget in the notes cannot plausibly deliver.
</task>

<constraints>
- Use only facts from the project notes and funder text. For anything missing (preliminary data, figures, citations, budget, collaborators' names), insert a visible placeholder such as "[PRELIMINARY DATA: pilot n and effect]" or "[CITATION: prevalence of X]". Never invent results, numbers or references.
- Respect the funder's limits; if none are given, keep aims to about one page (roughly 500 words) and say what length you assumed for other sections.
- Write in active voice with concrete verbs, and make each aim's success testable.
- Do not overpromise: impact claims must follow from the aims.
- If the project notes are too thin to write a credible section (for example no question or method), ask for the missing pieces first, listing exactly what is needed.
</constraints>

<output_format>
The requested section(s) under the funder's headings, then:
## Criteria coverage
A table: criterion | where it is addressed | strength (strong / adequate / weak) | how to strengthen.
## Placeholders to fill
A checklist of every placeholder in the draft.
## Reviewer risks
Three to five likely reviewer objections, each with the sentence or evidence that would pre-empt it.
</output_format>
