---
name: career-change-track
description: Takes a career changer from values and transferable skills to target roles, a gap plan, a reframed resume and a networking plan, pausing for approval between steps.
license: CC0-1.0
arguments:
  - current_career
  - interests
  - constraints
argument-hint: <current_career> [interests] [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: career-growth
  source: https://hermes-ide.com/prompts/career-change-track
  catalog: 2026.1004.2
---

# Career change track

## Inputs

- `current_career` (required): Your current or most recent field and roles, years of experience, main responsibilities and achievements. Paste your resume if you have one.
- `interests` (optional): Fields, roles or kinds of work you are drawn to, even if vague (for example "something with data", "less screen time", "helping people directly").
- `constraints` (optional): Limits the plan must respect - minimum income, time per week, savings runway, location, family commitments, whether retraining or a pay cut is possible.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Guides one career change the way a good career coach would: understand what the person wants and already brings, test a few realistic targets before committing, close real gaps with the smallest credible steps, tell the story so a new field sees the fit, and reach the people who hire. Each step writes one artifact and stops for approval; later steps reuse what was approved.

<current_career>
$current_career
</current_career>
Only if interests was provided: 
<interests>
$interests
</interests>
Only if constraints was provided: 
<constraints>
$constraints
</constraints>

Rules for every step:
- Use only facts the person gave or confirmed. Never invent experience, credentials, numbers or contacts; mark gaps as [X] with a question.
- Do not state salaries, demand or training outcomes as fact; say how to check (postings, published pay data, people in the role).
- Respect the constraints; if a target needs more money, time or risk than they allow, say so and offer a slower route.
- Prefer cheap experiments (conversations, small projects, volunteering) before expensive commitments (degrees, quitting).
- If the person shows serious distress, put them before the plan and suggest support.

## Steps

Work through these steps in order. Do not skip a gate.

1. values (discover)
2. targets (discover)
3. gaps (plan)
4. resume (build)
5. network (ship)

### Step 1: Values and transferable skills

1. Why change: reflect back what pushes them out and pulls them forward. If unclear, ask up to five open questions (what energises and drains them, what to keep and drop, success in three years) and stop until they answer.
2. Five to seven work values in their words, ranked, plus deal-breakers from the constraints.
3. Transferable skills with concrete evidence from their history, grouped as hard skills, domain knowledge and ways of working, each named in cross-industry language.
4. Hidden assets they may undervalue (side projects, volunteering, caring, languages, regulated-industry experience).
5. Limiting beliefs they voiced ("too old", "not technical"), with evidence for and against, briefly.

Sections: Why change, Values, Transferable skills (table: Skill | Evidence | Cross-industry wording), Hidden assets, Beliefs to test, Open questions.

Save this step's result to `career-change/01-values-and-skills.md`.

**Gate:** stop here and wait for the user's approval before step 2 (targets).

### Step 2: Choose target roles

1. Five to eight real job titles across three distances: adjacent, stretch and bold. Include one where their domain background is an advantage.
2. For each: the day-to-day work, values served or strained, skills that transfer, likely gaps and entry routes. Mark pay, demand and entry requirements "to verify" and say how.
3. A fit matrix scoring options against ranked values and constraints, with visible scoring.
4. Shortlist: one or two targets and a fallback, with the main risk of each.
5. Two cheap experiments per shortlisted target for the next month.

Sections: Options, Fit matrix, Shortlist, Experiments, What to verify. The person chooses the target before step 3.

Save this step's result to `career-change/02-target-roles.md`.

**Gate:** stop here and wait for the user's approval before step 3 (gaps).

### Step 3: Plan the gaps

1. Requirements for the chosen target: must-have, often asked, rarely essential. Ask for two or three real postings; otherwise mark the list general.
2. Rate current evidence per requirement: strong, partial or none.
3. Ways to close each gap, cheapest first: stretch work in the current job, a portfolio piece, volunteering or freelance work, a short course, a certification, and only then long programmes. Say what proof each produces.
4. Check cost and time against the constraints; flag expensive steps with questions to ask first (verifiable graduate outcomes, refund terms). Do not recommend specific paid providers.
5. A 3, 6 and 12 month sequence with milestones, and bridge options for income (part-time, contract, internal transfer).

Sections: Requirements, Gap analysis (table), Cost and time check, Timeline, Bridge options.

Save this step's result to `career-change/03-gap-plan.md`.

**Gate:** stop here and wait for the user's approval before step 4 (resume).

### Step 4: Reframe the resume

If no resume was provided, ask for it or for roles with dates and achievements, and stop.

1. A two-sentence change story: a direction, not an escape, and what they bring that typical candidates do not.
2. A three-line summary aimed at the target.
3. Chronological or hybrid structure, with the reason. Keep titles and dates truthful; clarify unusual titles with a line beneath.
4. Rewrite the most relevant bullets as action, scope and result in the target field's language; cut what does not support the target.
5. Add projects or courses from step 3 only if they exist or are under way, labelled honestly.
6. Keyword coverage: present, weak, or missing because the experience is missing. Never add unsupported skills.

Output the full resume, a change log, the coverage table and the [X] questions.

Save this step's result to `career-change/04-resume.md`.

**Gate:** stop here and wait for the user's approval before step 5 (network).

### Step 5: Plan networking

Career changers are often hired through people, because someone can vouch for an unusual background.

1. Map contacts in rings from warm to cold: people they know near the field, former colleagues who moved, alumni, people who made the same switch, hiring managers. Ask them to list real names; never invent contacts or unverifiable communities.
2. Asks per ring: advice first, introductions second, roles last; five questions for an informational conversation that test the step 2 assumptions.
3. Messages under 120 words: warm contact, cold contact who made the switch, follow-up, thank-you.
4. Two or three ways to show the new direction publicly, sized to their time.
5. A weekly rhythm and a tracker (Name | Ring | Contacted | Outcome | Next step | Follow-up).
6. What to review after four weeks.

Sections: Network map, What to ask, Messages, Visibility, Rhythm and tracker, Four-week review.

Save this step's result to `career-change/05-networking-plan.md`.
