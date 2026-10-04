---
name: choose-target-journal
description: Shortlists journals for a manuscript by scope, audience, article type, open-access costs and timelines, ranked in tiers, with facts to verify on each journal's site. For authors before submission.
license: CC0-1.0
arguments:
  - manuscript_summary
  - priorities
argument-hint: <manuscript_summary> [priorities]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: scientific-writing
  source: https://hermes-ide.com/prompts/choose-target-journal
  catalog: 2026.1004.3
---

# Shortlist target journals for a manuscript

## Inputs

- `manuscript_summary` (required): Title, abstract or summary, field and subfield, article type (original research, short report, review, methods), length, and what is new about it.
- `priorities` (optional): What matters to you - speed, open access, budget for fees and any funder mandate, audience, prestige, career deadlines, journals you already considered or were rejected from.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Desk rejection is most often a scope or fit decision, so the best target is a journal whose readers would cite the paper and whose recent issues publish similar work, not simply the highest-ranked one. Authors also weigh article type and length limits, open-access model and article processing charges (and whether a funder or institutional agreement covers them), funder mandates, typical time to first decision and to publication, indexing in the databases their field uses, data and preregistration policies, and their own deadlines. Facts such as fees, impact metrics, timelines and policies change often, so any figure recalled from memory must be checked on the journal's own site. Predatory journals imitate legitimate ones and target early-career authors.
</context>

<task>
Shortlist journals for this manuscript.
<manuscript>
$manuscript_summary
</manuscript>
Only if priorities was provided: 
<priorities>
$priorities
</priorities>

1. Profile the manuscript: field and subfield, likely readers, article type, strength and breadth of the contribution (field-changing, solid advance, incremental, replication or null result, methods or resource), and anything that narrows the options (length, data type, preregistration, open-access mandate).
2. Propose six to nine candidate journals in three tiers: reach (broad or high-profile, lower odds), realistic (strong fit, good odds), and safe (good fit, high odds, often faster). For each, say why it fits, which article type to use, and the open-access model.
3. Mark every fact that changes over time (fees, metrics, timelines, policies) as "verify" rather than stating it as current.
4. Recommend a submission order that respects the user's priorities and deadlines, and say how to adapt the manuscript between rejections (reformatting cost, transfer or cascade options when a publisher offers them).
5. List how to check fit for each journal: read the aims and scope, scan the last year of issues for similar papers, check the editorial board for people in the subfield, confirm article types and limits, fees and waivers, and indexing.
</task>

<constraints>
- Suggest only journals you are confident exist and publish in this area. If you are unsure of a journal in a niche subfield, describe the type of venue and tell the user how to find candidates (for example from where the papers they cite were published, or journal-finder tools offered by publishers and indexing services) instead of naming one.
- Never present fees, impact factors, acceptance rates or review times as verified facts.
- Do not recommend any journal with signs of predatory practice; say what those signs are.
- Respect constraints: if the user has no funds for fees, do not put fee-based gold open-access journals first without naming waiver, transformative-agreement or green open-access routes.
- If the field or article type is unclear, ask, and give a provisional shortlist with assumptions.
</constraints>

<output_format>
## Manuscript profile
Five or six bullets.
## Shortlist
A table: tier | journal | why it fits | article type | OA model and fees (verify) | speed (verify) | risks.
## Submission order
Numbered, with reasoning.
## Verify before submitting
A checklist per journal.
## Red flags
The predatory-journal warning signs to check.
</output_format>
