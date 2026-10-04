---
name: ux-research-study-track
description: Runs a UX research study in gated steps - research questions, method choice, screener, session guide, notes template, synthesis and a decision-focused readout - pausing for approval.
license: CC0-1.0
arguments:
  - research_question
  - product
  - timeline
argument-hint: <research_question> [product] [timeline]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: ux-research
  source: https://hermes-ide.com/prompts/ux-research-study-track
  catalog: 2026.1004.2
---

# UX research study track

## Inputs

- `research_question` (required): What the team needs to learn and why now - the decision it will inform, who makes it, and what is already known (analytics, past research, support themes).
- `product` (optional): The product or prototype, its users and the area in scope. Optional.
- `timeline` (optional): When the decision is due and how much time and budget the study has, for example "3 weeks, 1,000 USD for incentives, one researcher". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs one UX research study from question to decision.

<research_question>
$research_question
</research_question>
Only if product was provided: 

Product: $product
Only if timeline was provided: 

Timeline and resources: $timeline

Seven steps: sharpen the research questions, choose the method, write the screener, write the session guide, prepare the notes template while sessions run, synthesise the notes, and write a readout aimed at the decision. Each step produces one document and stops for the team's edits or approval; later steps build on the approved versions.

Rules for every step: the study exists to inform a decision, so every question, task and finding traces back to it. Keep what people did apart from what they said and from what we interpret. Protect participants: informed consent, the right to stop, fair incentives, minimal personal data and anonymised quotes. Never invent participants, quotes, counts or results; steps that need real-world work wait for the team to paste notes. The team owns every decision.

## Steps

Work through these steps in order. Do not skip a gate.

1. questions (discover)
2. method (plan)
3. screener (plan)
4. guide (plan)
5. notes-template (verify)
6. synthesis (review)
7. readout (review)

### Step 1: Research questions and the decision

If the decision this study informs, or who makes it, is missing, ask for both and stop. Other gaps become marked assumptions.

Write:
- **Decision:** what will be decided, by whom, by when, and the options.
- **Research questions:** three to five, specific and answerable with evidence, each labelled behaviour (what people do), attitude (why, what matters) or prevalence (how many).
- **Known so far:** from the input, with sources, and what it does not tell us.
- **Out of scope.**
- **What would change our mind:** for each option, the evidence that would favour it, set before any data.

Flag questions this study cannot answer in time, and propose a narrower one or a better source (analytics, a survey).

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 2 (method).

### Step 2: Choose the method

1. Match each approved question to a method: behaviour and usability → usability tests, contextual inquiry or diary studies; attitude → interviews; prevalence → surveys or analytics; navigation and labels → tree tests or card sorts. Say plainly when a requested method cannot answer a question (a usability test cannot show whether people would buy).
2. Recommend one primary method, and a second only if a question needs it and time allows.
3. Specify participants (behaviour-based, by segment), sample size with reasoning (about five to eight per segment for qualitative work; far more for surveys), session length and format, stimulus, incentive, roles, and a schedule with recruiting lead time, a pilot, sessions, synthesis and readout.
4. Note consent, data storage and deletion, and any ethics review (children, patients, vulnerable groups).

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 3 (screener).

### Step 3: Screener and invitation

1. **Recruit spec:** must-have behaviours with recency and frequency; exclusions (research, UX, marketing or press jobs; employees of the company or competitors; a similar study in the last six months; study-specific ones).
2. **Screener:** 8 to 12 questions, knock-outs first, multiple choice with distractors and "None of these", the target hidden among other options, never a yes/no that reveals the answer. Give the logic per answer (accept, reject, quota), one articulation question with accept criteria, logistics and consent questions.
3. **Quota grid** with about 20% over-recruit.
4. **Invitation** (under 120 words, criteria not revealed) and **confirmation message**, with placeholders for incentive, time and links.

Ask only what decides eligibility; sensitive data only if needed, optional, with a reason.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 4 (guide).

### Step 4: Session guide

Write the guide for the approved method, timed to the session length.

- **Opening:** neutral purpose, consent and recording, the right to stop, "we are testing the product, not you", and a think-aloud practice for usability tests.
- **Interviews:** context warm-up, then the last specific time the behaviour happened, probing trigger, steps, people, tools, workarounds and cost. Open, neutral questions about the past; no "would you use" or "how much would you pay".
- **Usability tests:** five to eight scenario tasks that avoid interface labels, each with start point, success criteria and time limit; neutral probes. Unmoderated: self-contained instructions and an attention check.
- **Other methods:** the equivalent instrument.
- Label every block or task with the research question it serves, and add moderator notes (do not help or defend the design) and a pilot checklist.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 5 (notes-template).

### Step 5: Notes template and sessions

1. A notes template per session: session id, date, segment, device (no names); for each block or task, what the participant did, verbatim quotes with timestamps, and the note-taker's interpretation in a separate labelled field; task outcome, time and problem severity; evidence per research question; surprises.
2. A five-minute debrief routine after each session.
3. A session tracker: id, segment, date, status, notes link placeholder.

Stop for approval. Then run the sessions. The team pastes all notes or transcripts to start step 6; do not continue without them.

**Gate:** stop here and wait for the user's approval before step 6 (synthesis).

### Step 6: Synthesis

If no notes or transcripts were pasted, ask for them and stop.

1. List sessions analysed (N) and any excluded, with the reason.
2. Break notes into observations tagged with session id and type: behaviour, opinion or hypothetical.
3. Cluster by underlying cause; name each finding as a statement, not a topic.
4. Per finding: n of N with ids, one to three verbatim quotes, confidence, and for usability problems a severity (critical, serious, minor) separate from frequency.
5. Answer each research question, or say "not answered by this study".
6. Note contradictions, segment differences, surprises and what worked.

Use "n of N", not percentages; mask personal details.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 7 (readout).

### Step 7: Decision-focused readout

One to two pages for the decision-maker, from the approved synthesis only:

1. **Recommendation:** the option the evidence favours, confidence, and the findings that drive it, checked against the step 1 "what would change our mind" criteria. Say plainly when evidence is mixed.
2. **Answers to the research questions.**
3. **Top findings,** ranked by impact on the decision, with n of N, a quote and severity.
4. **Next actions** with owner placeholders.
5. **Limits and still unknown,** each gap with its cheapest next step.
6. **Appendix:** method, segments, dates, link placeholders.

Put uncomfortable findings first. The decision-maker owns the decision.
