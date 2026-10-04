---
name: hiring-track
description: Takes a hire from role definition to job description, sourcing plan, interview loop, scorecard debrief and offer, pausing for approval between steps. Use when running a search.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: hiring
  source: https://hermes-ide.com/prompts/hiring-track
  catalog: 2026.1004.2
---

# Hiring track

## Inputs

- [ROLE] (required): The role you are hiring for, its level, and why it exists now (new headcount, backfill, new capability). Rough notes are fine.
- [TEAM_CONTEXT] (required): The team and company - size, what the team does, who the hire reports to, location or remote terms, pay range or budget, and who decides on the hire.
- [TIMELINE] (optional; default: not set): When you need the person to start, or the date you want an accepted offer by (for example "start by March" or "offer within 8 weeks").

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs one hire the way a strong recruiter and hiring manager would together: agree what success looks like, advertise honestly, reach the right people, assess everyone against the same job-related evidence, decide on that evidence, and close fairly. Each step writes one artifact and stops for approval; later steps build on what was approved.

<role>
[ROLE]
</role>

<team_context>
[TEAM_CONTEXT]
</team_context>

Timeline: [TIMELINE]

Rules for every step:
- Use only facts the hiring manager gave or confirmed. Ask for missing essentials (pay range, level, decision maker, location) and mark gaps as [X].
- Keep every requirement and question job-related. Never ask about or screen on age, family plans, health, disability, religion, nationality, sexual orientation or other protected characteristics, or proxies for them.
- Do not state market pay, candidate supply or legal rules as fact; say what to check, and refer contracts, visas and local law to HR or an employment lawyer.
- Give candidates honest information, reasonable time demands and a closed loop.
- End each artifact with open questions.

## Steps

Work through these steps in order. Do not skip a gate.

1. define (discover)
2. describe (build)
3. source (plan)
4. loop (design)
5. debrief (review)
6. offer (ship)

### Step 1: Define the role

Run the intake before any job ad exists.

1. Problem: why this hire, why now, and the cost of the seat staying empty. For a backfill, ask whether the role should change.
2. Outcomes at 90 days, 6 months and 12 months, as observable results.
3. At most five must-haves, each tied to an outcome; a separate trainable list. Replace proxies (years, degrees, specific tools) with the capability they stand for.
4. Level by scope, and the pay range. If none is given, list what to benchmark instead of stating a figure.
5. Trade-offs: tensions between wish list, level, pay, location and timeline.
6. Process: who decides, who interviews, and service levels (for example CV review within 2 working days).
7. Timeline: work back from it (default 6 to 10 weeks to accepted offer, plus notice) and say if it is realistic.

Sections: Problem, Outcomes, Must-haves and trainable, Level and pay, Trade-offs, Process, Timeline, Open questions.

Save this step's result to `hiring/01-role-definition.md`.

**Gate:** stop here and wait for the user's approval before step 2 (describe).

### Step 2: Write the job description

Write the ad from the approved definition: a sales document for the right people and an honest filter for the wrong ones.

1. Opening: the problem this person will solve, in plain words. No "rockstar" or "fast-paced family".
2. Four to six outcome-led responsibilities.
3. Must-haves as capabilities, then nice-to-haves and "you will learn", plus an invitation to apply when meeting most of them.
4. One or two real challenges of the role.
5. Pay range, location and work mode, visa sponsorship, the process stages and total candidate time.
6. Accessibility, adjustments and equal-opportunity lines; neutral wording.

Output the ad ready to post, then an inclusion check (flagged phrases and replacements).

Save this step's result to `hiring/02-job-description.md`.

**Gate:** stop here and wait for the user's approval before step 3 (source).

### Step 3: Plan sourcing

1. Two or three realistic candidate profiles, including one non-obvious pool (adjacent industry, career changer, returner, internal mover).
2. Channels per profile (referrals, internal posting, general or niche boards, communities, schools, direct sourcing, agencies), with effort and why. Do not invent named communities or response rates.
3. Example search strings with title and skill variants.
4. A short outreach message, one follow-up, and a referral request for the team.
5. A weekly funnel plan labelled as assumptions to revisit after two weeks.
6. Evidence a CV screener looks for per must-have, so screening is consistent and not keyword-based; and what not to filter on (school names, unexplained gaps).

Sections: Profiles, Channels, Search strings, Outreach, Weekly plan, Screening criteria.

Save this step's result to `hiring/03-sourcing-plan.md`.

**Gate:** stop here and wait for the user's approval before step 4 (loop).

### Step 4: Design the interview loop

1. Four to six competencies from the must-haves, each with a definition and what meets the bar at this level. Replace "culture fit" with defined behaviours.
2. Three to five stages with length, interviewer and the competencies each owns; state total candidate time. Any take-home is a few hours at most, paid if longer, with an alternative format.
3. Per stage: two to four questions or the exercise brief, probes, and what strong and weak evidence sounds like.
4. Scorecard: 1 to 4 anchors per competency (concern, below, meets, strong) and evidence notes.
5. Rules: independent scoring before discussion, a decision rule agreed now (for example no "concern" score and "meets" or better on every must-have competency), accommodations for all, questions never to ask.

Sections: Competencies, Loop overview (table), Interviewer guides, Scorecard (table), Rules. After approval, the next step waits until interviews are done and scorecards are shared.

Save this step's result to `hiring/04-interview-loop.md`.

**Gate:** stop here and wait for the user's approval before step 5 (debrief).

### Step 5: Run the scorecard debrief

Needs the submitted scorecards and notes. If they are missing, ask for them and stop; never invent scores or evidence.

1. Evidence table: scores per interviewer and competency with one-line evidence; mark gaps.
2. Flag scores without notes, "vibe" comments, and anything touching protected characteristics or undefined "culture fit"; recommend discounting or re-checking them.
3. Disagreements of two points or more: show both sides and the question that would resolve it, rather than averaging.
4. Judge each candidate against the bar with the agreed decision rule before comparing candidates.
5. Gaps of the recommended candidate and how onboarding covers them, plus a short debrief agenda.

Sections: Evidence table, Flags, Disagreements, Recommendation, Risks, Agenda. Draft no offer or rejection until the decision is made.

Save this step's result to `hiring/05-debrief.md`.

**Gate:** stop here and wait for the user's approval before step 6 (offer).

### Step 6: Make the offer and close the loop

1. Package within the approved range, with the reason for the point chosen (evidence, internal equity); unconfirmed figures as [X].
2. What can move and what cannot, the walk-away point, and a reasonable decision window (no exploding deadlines).
3. A short verbal offer script that leads with specific reasons the team chose them.
4. A plain-language written summary; the contract, conditions and local terms go through HR or an employment lawyer.
5. Respectful messages for finalists not chosen (with fair, specific feedback where possible) and for earlier-stage candidates still waiting.
6. Onboarding handover: gaps to support and the 90-day outcomes.

Sections: Offer package, Negotiation room, Verbal script, Written summary, Other candidates, Handover.

Save this step's result to `hiring/06-offer.md`.
