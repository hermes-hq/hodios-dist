---
name: new-manager-track
description: Guides a manager through the first 90 days with a team in gated steps - listening tour, first one-to-ones, team health read, early decisions and a 90-day review.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: people-management
  source: https://hermes-ide.com/prompts/new-manager-track
  catalog: 2026.1003.1
---

# New manager track

## Inputs

- [TEAM] (required): The team you now manage - size, roles and tenure (initials if you prefer), what it owns, who you report to, and the key teams and stakeholders around it.
- [CONTEXT] (required): How you got here (promoted from within, hired externally, merged teams), what happened to the previous manager, what your manager expects of you, known problems and anything urgent.
- [START_DATE] (optional): Your start date in the role, used to put dates on the plan. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Takes a manager through the first 90 days with a team the way an experienced leadership coach would. Listen widely before judging, build a real relationship with each person, form an evidence-based view of how the team is doing, make a few well-chosen early decisions, and review honestly at day 90. Each step writes one artifact and stops for approval. Later steps build on what the manager reports back from the real conversations, not on guesses.

<team>
[TEAM]
</team>

<context>
[CONTEXT]
</context>
Only if [START_DATE] was provided: Start date: [START_DATE]

Rules for every step:
- Use only what the manager tells you, including what they report from conversations. Never invent what people said or how the team feels; mark gaps as [X] and ask.
- Separate observations from interpretations, and note how confident each conclusion is.
- Keep confidences. Do not suggest repeating what one person said to others in a way that identifies them.
- Do not rush to change things in the first 30 days unless something is urgent: safety, legal, a customer crisis, or a person in distress. Say so when something is urgent.
- Refer harassment, discrimination, safety, conduct or health matters to HR rather than handling them as team-health findings.
- End each artifact with open questions and what the manager should bring to the next step.

## Steps

Work through these steps in order. Do not skip a gate.

1. listening-tour (discover)
2. one-to-ones (discover)
3. team-health (discover)
4. early-decisions (plan)
5. ninety-day-review (review)

### Step 1: Plan the listening tour

Plan who to hear from in the first three to four weeks, before forming any view.

1. Your manager first: agree what success at day 90 looks like, the team's known problems and strengths, which decisions are yours, and how to keep them informed.
2. Listening map: every direct report, key peers, partner teams and internal customers, HR, and one or two outside views (a customer-facing colleague, a skip-level). Order them and add dates from the start date if given.
3. Six to eight open questions, adjusted per group: what the team does well, what they need from it, what was tried before, the one thing to change.
4. How to run it: say you are listening before deciding, take notes, promise nothing, ask who else to meet. If promoted from within, how to shift relationships with former peers and how to approach anyone who also wanted the role, early and in private; if replacing a manager, how to acknowledge that.
5. Note quick wins but do not act yet unless urgent.

Sections: Expectations with your manager, Listening map (table: Person or group | Why | When | Focus), Questions, How to run it, Urgent items. The manager runs the conversations and brings back notes.

Save this step's result to `new-manager/01-listening-tour.md`.

**Gate:** stop here and wait for the user's approval before step 2 (one-to-ones).

### Step 2: First one-to-ones

Prepare a first one-to-one with each direct report, using what step 1 surfaced, and set the regular rhythm.

1. Purpose: build trust and learn how each person works; it is not an assessment. Give the opening line.
2. Core questions: their role as they see it, what they are proud of, what gets in the way, what they want to grow into, how they like feedback and recognition, what the previous manager did that they want kept or dropped. Add two or three tailored questions per person, framed as hypotheses to test.
3. A short "how I work" note from the manager, and an invitation to share theirs.
4. Rhythm: frequency, length, and an agenda the report leads.
5. Sensitive cases: a report who wanted the job, a former peer, someone struggling or likely to leave, a serious concern raised.

Sections: Opening, Per-person plan (table: Person | Tailored questions | Listen for), How I work, Rhythm, Sensitive cases. The manager holds the meetings and reports back.

Save this step's result to `new-manager/02-first-one-to-ones.md`.

**Gate:** stop here and wait for the user's approval before step 3 (team-health).

### Step 3: Read the team's health

Turn the notes from steps 1 and 2 into an evidence-based picture.

1. Themes: group what people said, count the sources for each, and mark whether they come from the team, stakeholders or both. Keep sources anonymous.
2. Rate each dimension strong, mixed, weak or unknown, with evidence: purpose and priorities, delivery and quality, workload, skills and capacity, trust within the team, stakeholder relationships, ways of working, growth and recognition, psychological safety.
3. People view: strengths, needs and any risk per person, with confidence. No performance conclusions from hearsay this early.
4. Contradictions between your manager, stakeholders and the team, and what evidence would settle them.
5. A "here is what I heard" summary to share with the team, with nothing that identifies a source.

Sections: Themes, Health read (table: Dimension | Rating | Evidence | Confidence), People view, Contradictions, What I heard. The manager confirms or corrects the read.

Save this step's result to `new-manager/03-team-health.md`.

**Gate:** stop here and wait for the user's approval before step 4 (early-decisions).

### Step 4: Choose early decisions

Choose two or three changes for days 30 to 90 from the approved health read.

1. Candidates: clarifying priorities, fixing a process, rebalancing workload, a team agreement, a hiring need, removing a stakeholder blocker, a performance conversation.
2. Score each on impact, effort, whether the team asked for it, reversibility and credibility. Recommend a set that includes at least one change the team asked for.
3. For each: the change, who to consult, how to communicate it, owner, first step, measure and check date.
4. What to leave alone for now, and why.
5. What to agree with your manager first and what to escalate.
6. A performance concern gets an early, informal, specific conversation, with HR involved when needed.

Sections: Candidates (scored table), Chosen decisions (table: Decision | Consult | Communicate | Owner | First step | Measure | Check date), Leaving alone, Alignment. The manager approves before acting.

Save this step's result to `new-manager/04-early-decisions.md`.

**Gate:** stop here and wait for the user's approval before step 5 (ninety-day-review).

### Step 5: The 90-day review

Review honestly and set the next quarter.

1. Results of each early decision against its measure, from what the manager reports; [X] where unmeasured.
2. Team health now against step 3: what moved, what did not, and the evidence.
3. Relationships: one-to-ones, former peers, stakeholders, your own manager.
4. Three or four questions to ask the team and stakeholders about your first 90 days (keep, start, stop), collected anonymously if needed.
5. Your learning: what was harder than expected, habits to build, where to get support.
6. Two or three priorities for next quarter with measures, and an update to your manager under 200 words.

Sections: Results, Team health now, Relationships, Feedback questions, Your learning, Next quarter, Update to your manager.

Save this step's result to `new-manager/05-ninety-day-review.md`.
