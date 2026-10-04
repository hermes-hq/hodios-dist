---
name: grant-proposal-track
description: Takes a research grant from funder fit to aims, approach, budget justification and a mock review with revisions, pausing for approval between steps. For researchers applying for funding.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: scientific-writing
  source: https://hermes-ide.com/prompts/grant-proposal-track
  catalog: 2026.1004.3
---

# Grant proposal track

## Inputs

- [FUNDER_CALL] (required): The funding call or programme text, including eligibility, review criteria, page or word limits, budget rules and required sections. Paste it; a link alone is not enough.
- [RESEARCH_IDEA] (required): Your idea in your own words, with preliminary data, team, track record and anything already drafted.
- [DEADLINE] (optional): The submission deadline, plus any internal deadline set by your research office, for example "funder 15 March, research office 1 March".
- [SLUG] (optional; default: grant-proposal): Short kebab-case name for the proposal, used for the folder the step artifacts are saved in.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Builds a grant proposal for the idea below against the call below, the way an experienced applicant and their research office would: check fit and eligibility first, then lock the aims, then write the approach, then justify the budget, and finally read the whole thing as a hostile but fair panel would. Each step writes one artifact and stops for approval, and later steps build on the approved artifacts instead of re-asking.

<funder_call>
[FUNDER_CALL]
</funder_call>

<research_idea>
[RESEARCH_IDEA]
</research_idea>

Only if [DEADLINE] was provided: Deadline: [DEADLINE]. Work back from the earliest deadline given and say at step 1 if the timeline is unrealistic.

Rules for every step:
- The funder's call is the specification. Quote its criteria, limits and required headings exactly, and map every section to the criterion it serves. If the call is silent on something, say so rather than assume another funder's rules.
- Never invent preliminary data, publications, collaborators, letters of support, costs, salary rates or institutional policies. Use clearly marked placeholders such as [PRELIMINARY DATA: pilot n and effect] and list them at the end of each artifact.
- Write in the applicant's voice for reviewers who are expert but busy and outside the exact subfield: the main point of each paragraph comes first, and every claim of need or novelty is something the applicant can support.
- Track page and word counts against the call's limits in every drafted section.

## Steps

Work through these steps in order. Do not skip a gate.

1. fit (plan)
2. aims (design)
3. approach (build)
4. budget (build)
5. mock-review (review)

### Step 1: Funder fit and eligibility

Decide whether this idea should go to this call, and in what form.

1. Extract from the call: eligibility rules, amount and duration, required sections and limits, review criteria with weights or scale, and anything that disqualifies. Present a compliance table: requirement | wording from the call | status for this applicant (met, not met, unknown).
2. Assess fit honestly against the funder's mission and each criterion. If the fit is poor, say so and name the kind of scheme that would fit better.
3. Propose a one-sentence pitch in the funder's language and a scope that fits the money and duration; say what to defer to a later grant.
4. List what you need before step 2: eligibility facts, preliminary data, team, partners, internal deadlines.

If any hard eligibility criterion is "not met", say so at the top and recommend not proceeding unless it can be resolved. Stop and wait for approval and answers.

Save this step's result to `grants/[SLUG]/01-fit.md`.

**Gate:** stop here and wait for the user's approval before step 2 (aims).

### Step 2: Aims and significance

Write the aims page (or whatever the call names it) that reviewers read first.

1. Open with the problem and why it matters now, in terms a non-specialist reviewer can follow, then the specific gap.
2. State the long-term goal, the objective of this grant, and the central hypothesis or question, with its rationale (placeholders for preliminary data not yet supplied).
3. Write two to four aims, each with a short active title, the approach in one or two sentences, and the expected outcome. Aims should be related but not dependent: if Aim 1 fails, the others still deliver. If they are dependent, propose a fix.
4. Close with expected outcomes and impact framed in the call's own criteria.

Check the page against the call's limit, then add a table criterion | where the page addresses it, and the open placeholders. Stop and wait for approval.

Save this step's result to `grants/[SLUG]/02-aims.md`.

**Gate:** stop here and wait for the user's approval before step 3 (approach).

### Step 3: Approach, timeline and risks

Write the research plan for the approved aims, where most proposals lose points.

1. For each aim: rationale, design, participants or materials, measures, sample size with its justification (or a placeholder asking for one), analysis, expected results, and problems with alternative strategies.
2. Address rigour explicitly (controls, randomisation, blinding, reproducibility; for qualitative work, sampling logic and credibility) and feasibility (preliminary work, access, expertise, facilities).
3. Add a timeline table by quarter with milestones, including ethics, recruitment, analysis and dissemination, and a risk register: risk | likelihood | impact | mitigation.
4. List other sections the call requires that depend on this plan (data management, ethics, open access, impact) without writing them.

Report the page count against the call's budget. Stop and wait for approval.

Save this step's result to `grants/[SLUG]/03-approach.md`.

**Gate:** stop here and wait for the user's approval before step 4 (budget).

### Step 4: Budget justification

Build a budget that ties every cost to the approved approach.

1. Ask for what you lack: salary scales, on-costs, overhead rate, currency, supplier quotes, the funder's template. Never guess figures; write [AMOUNT: source needed] and keep the structure.
2. Lay out the budget by the funder's categories (personnel, equipment, consumables, travel, participant costs, publication fees, subcontracts, indirect costs) by year.
3. Justify each line in one or two sentences naming the task it serves and how the quantity was estimated.
4. Check it against the call's rules (maximum, eligible costs, caps, indirect costs) and for consistency: every person in the plan has effort, every cost has a task. Flag padding and under-costing.

Remind the applicant that the research office must confirm rates and rules. Stop and wait for approval.

Save this step's result to `grants/[SLUG]/04-budget.md`.

**Gate:** stop here and wait for the user's approval before step 5 (mock-review).

### Step 5: Mock panel review and revisions

Read the approved aims, approach and budget as a panel would, then revise.

1. Write three short reviews: a specialist, a reviewer from a neighbouring field, and a panel chair focused on fit and value. Each scores every criterion on the call's scale (or a stated five-point scale) with strengths, weaknesses and a one-line rationale. Be as tough as a real panel, but do not invent weaknesses.
2. Rank the changes that would raise the score most, separating fatal problems from fixable ones.
3. Make the revisions you can, shown as before and after text, and say exactly what to obtain for the rest (data, letters, quotes).
4. Finish with a submission checklist: sections, attachments, limits, formatting, sign-offs, open placeholdersOnly if [DEADLINE] was provided: , and dated tasks working back from [DEADLINE].

Say that a mock review does not predict the outcome, and that a colleague who has sat on this funder's panels is the best final reader.

Save this step's result to `grants/[SLUG]/05-review-and-revisions.md`.
