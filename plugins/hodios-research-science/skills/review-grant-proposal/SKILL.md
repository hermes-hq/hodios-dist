---
name: review-grant-proposal
description: Reviews a grant proposal against the funder's criteria as a panel reviewer would, with strengths, weaknesses, a score rationale and ranked fixes. For applicants before submission and for reviewers.
license: CC0-1.0
arguments:
  - proposal
  - criteria
  - purpose
argument-hint: <proposal> [criteria] [purpose]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: peer-review
  source: https://hermes-ide.com/prompts/review-grant-proposal
  catalog: 2026.1004.0
---

# Review a grant proposal as a panel member

## Inputs

- `proposal` (required): The proposal text - summary, aims, research plan, budget justification and any other sections you have.
- `criteria` (optional): The funder's review criteria and scoring scale, pasted from the call or reviewer guidance. If empty, common criteria (significance, innovation, approach, feasibility, team, environment, budget) and a five-point scale are used.
- `purpose` (optional; one of: pre-submission, assigned-review; default: pre-submission): Pre-submission feedback for the applicant, or a draft of a real review you were assigned.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Panels decide quickly. A reviewer reads the summary and aims first and forms a view of significance and fit within minutes, then reads the approach looking for reasons the work might fail. Proposals lose points for an unclear central question, aims that depend on each other, preliminary data that do not support feasibility, vague methods ("appropriate statistical analyses"), unjustified sample sizes, ambition beyond the budget or timeline, missing risk mitigation, and budgets that do not match the work. Good reviews are specific, tie every comment to a criterion, separate major from minor weaknesses, and are written so the applicant can act on them. Scores should follow from the stated strengths and weaknesses, on the funder's own scale.
</context>

<task>
Review this proposal ($purpose).
<proposal>
$proposal
</proposal>
Only if criteria was provided: 
<criteria>
$criteria
</criteria>

1. Summarise the proposal in three or four sentences: question, aims, approach, and the claimed contribution, so the applicant can see whether a reviewer understood it as intended.
2. For each criterion, list strengths and weaknesses, label each weakness as major (would likely lower the score substantially) or minor, and give a score on the funder's scale with a one-line rationale that follows from those points. Keep the scale's direction: on some scales a lower number is better (for example 1 = exceptional, 9 = poor), so state which end is best in the scores table. If no criteria were given, use the common ones and a five-point scale where 5 is best, and say so.
3. Check the things panels check: is the question clear and important; do the aims follow from it and stand independently; do preliminary data support feasibility; are design, sample size, analysis and rigour (controls, blinding, randomisation, reproducibility, or for qualitative work sampling and credibility) adequate; is the timeline realistic; are risks named with alternatives; does the team have the expertise; is the budget aligned with the work; are ethics, data management and impact addressed where required.
4. Give an overall impression: where the proposal would likely land (competitive, borderline, unlikely to be funded in its current form) and the single biggest reason.
5. For pre-submission feedback, rank the fixes by how much they would improve the score per hour of work, with concrete wording or structural suggestions. For an assigned review, phrase the output as a professional review the applicant would receive.
6. List the questions a panel discussion would raise.
</task>

<constraints>
- Base every comment on the proposal text. Quote or point to the passage. Do not assume facts that are not there, and do not invent the funder's criteria or scale.
- Be direct and fair: name real strengths, and do not soften major weaknesses into minor ones.
- Do not speculate about the applicants' identity, institution prestige or demographics; judge the proposal.
- For an assigned review, remind the user that proposals are confidential and that many funders do not allow reviewers to put proposal text into AI tools; tell them to check the funder's policy before using this for a real review.
- A mock score is not a prediction. Say so once.
</constraints>

<output_format>
## Overall impression
Two to four sentences with the likely standing and main reason.
## Scores by criterion
One line naming the scale and which end is best, then a table: criterion | score | rationale.
## Strengths
Bullets by criterion.
## Weaknesses
Bullets by criterion, each tagged (major) or (minor), with the passage it refers to.
## Fixes ranked by impact
Numbered list, highest impact first, each with a concrete suggestion.
## Questions a panel would ask
Bullets.
</output_format>
