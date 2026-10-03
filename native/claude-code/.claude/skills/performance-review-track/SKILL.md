---
name: performance-review-track
description: Guides a manager through review season by gathering evidence, drafting each review, calibrating ratings for bias and preparing each review conversation, with approval between steps.
license: CC0-1.0
arguments:
  - team_and_cycle
  - review_template
argument-hint: <team_and_cycle> [review_template]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: people-management
  source: https://hermes-ide.com/prompts/performance-review-track
  catalog: 2026.1003.0
---

# Performance review track

## Inputs

- `team_and_cycle` (required): Your team (roles, tenure, using initials if you prefer), the review period, deadlines, the rating scale with definitions, any distribution guidance, and what is decided from ratings (pay, promotion).
- `review_template` (optional): Your company's review form or required sections. Optional; without it each review uses summary, results, how the work was done, growth and rating rationale.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs a manager's review season the way a careful HR partner would: collect evidence for the whole period before judging, write each review from that evidence, check ratings across the team for consistency and bias, then prepare conversations that land. Each step writes one artifact and stops for approval.

<team_and_cycle>
$team_and_cycle
</team_and_cycle>
Only if review_template was provided: 
<review_template>
$review_template
</review_template>

Rules for every step:
- Use only evidence the manager supplies. Never invent results, incidents, feedback or ratings; mark gaps as [X] and ask.
- Describe behaviour and outcomes, not personality.
- Never mention or weigh health, disability, pregnancy, leave, age, family or other protected characteristics. If the notes raise them, flag for HR in that step's open questions.
- Ratings and decisions belong to the manager and the company's process; you advise and check.
- End each artifact with open questions.

## Steps

Work through these steps in order. Do not skip a gate.

1. evidence (discover)
2. draft (build)
3. calibrate (review)
4. conversations (ship)

### Step 1: Gather evidence

Build an evidence file per person before drafting anything.

1. List the sources to collect for the whole period: goals set at the start, results and metrics, project outcomes, 1:1 notes, peer and stakeholder feedback, recognition, self-review, and any issues already discussed.
2. Per person, sort what the manager provides into results against goals, how the work was done, and growth, each with dates.
3. Coverage check: mark months or goals with no evidence, and evidence that is only from the last six weeks (recency risk) or from one source.
4. List what to request (for example peer feedback from a named cross-team partner) and by when, given the deadline.

Sections: Evidence by person (table: Theme | Evidence | Date | Source), Gaps, Requests, Open questions.

Save this step's result to `reviews/01-evidence.md`.

**Gate:** stop here and wait for the user's approval before step 2 (draft).

### Step 2: Draft the reviews

Draft one review per person from the approved evidence file, using the review template if given.

1. Summary: two or three sentences that a reader could check against the evidence.
2. Results and how the work was done: each claim backed by a specific example with its date and impact; strengths first, then development areas, with the same level of specificity for both.
3. Proposed rating with a rationale tied to the scale definitions, and the strongest evidence against it.
4. Growth: two or three goals for the next period, each observable.
5. Consistency check: whether anything in the review would surprise the person, given what they heard during the year. Surprises go to open questions.

Sections: one review per person, then Open questions.

Save this step's result to `reviews/02-drafts.md`.

**Gate:** stop here and wait for the user's approval before step 3 (calibrate).

### Step 3: Calibrate

Check the approved drafts across the team before ratings are submitted.

1. Rating table: person, proposed rating, the one-line rationale, and the strongest evidence.
2. Consistency: are similar results rated alike? Is the bar for each rating applied the same way across roles and levels?
3. Bias check: recency, halo or horns, leniency or severity overall, similarity to the manager, visibility (remote or quiet people under-credited), and wording applied unevenly (for example "abrasive" or "emotional" for some people, "direct" or "passionate" for others). Quote the phrase and propose neutral wording.
4. Distribution: compare with any company guidance without forcing it; explain any deviation with evidence.
5. Calibration meeting prep: for each rating likely to be challenged, the two pieces of evidence that defend or change it.

Sections: Rating table, Consistency, Bias findings (table: Person | Issue | Evidence | Change), Calibration prep, Open questions.

Save this step's result to `reviews/03-calibration.md`.

**Gate:** stop here and wait for the user's approval before step 4 (conversations).

### Step 4: Prepare the conversations

Prepare each review conversation from the calibrated review.

1. Logistics: send the written review shortly before or share it in the meeting, per company practice; 45 to 60 minutes; separate pay discussion if the company allows.
2. Opening and the key message in the first five minutes, stated plainly.
3. Talking points: two strengths and one or two development areas, each with its example; one question to invite the person's view on each.
4. Likely reactions (disagreement with the rating, surprise, upset, asking about promotion or pay) and responses that listen first, explain the evidence, and say what can and cannot change.
5. Close: agreed growth goals, support from the manager, and the date of the first follow-up 1:1.

Sections: one conversation plan per person, then Open questions.

Save this step's result to `reviews/04-conversations.md`.
