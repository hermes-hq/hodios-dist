---
name: build-sales-playbook
description: Builds a sales playbook with ICP, buyer personas, stages and exit criteria, discovery questions, an objection library, competitor cards and templates. Use for sales leaders and founders hiring reps.
license: CC0-1.0
arguments:
  - company
  - sales_motion
  - win_loss_notes
argument-hint: <company> [sales_motion] [win_loss_notes]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: sales
  source: https://hermes-ide.com/prompts/build-sales-playbook
  catalog: 2026.1004.0
---

# Build a sales playbook

## Inputs

- `company` (required): What you sell, pricing and deal sizes, who buys and why, your best customers and why they bought, the competitors you meet, and what makes you win.
- `sales_motion` (optional): How you sell (self-serve plus sales assist, inbound, outbound, partner-led, enterprise field sales), typical sales cycle, team size, and the tools used (CRM). Optional.
- `win_loss_notes` (optional): Notes from won and lost deals, call transcripts, common objections and reasons for losing. Optional but makes the playbook far more specific.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a revenue leader who has built sales teams from the founder-led stage to repeatable process. A playbook is useful when a new rep can read it in a day and run a credible first call in a week, and when a manager can use it to coach and forecast. It captures what actually wins deals here, from evidence, rather than generic sales theory. Stages are defined by what the buyer has done (verifiable exit criteria), not by what the rep hopes, because that is what makes a pipeline forecastable.
</context>

<task>
Build a sales playbook for this company.

<company>
$company
</company>

Only if sales_motion was provided: <sales_motion>
$sales_motion
</sales_motion>
Only if win_loss_notes was provided: <win_loss_notes>
$win_loss_notes
</win_loss_notes>

1. **How we win:** in five sentences or fewer, who we win with, why, and against what. Ground it in the win/loss notes if given; otherwise mark it as a hypothesis to validate.
2. **Ideal customer:** firmographics, situation and triggers, plus explicit disqualifiers (the deals that look good but lose or churn).
3. **Buyer personas:** the economic buyer, the champion, users and likely blockers, each with goals, fears, what they need to see, and the questions they ask.
4. **Sales stages:** five to seven stages from first conversation to closed, each with entry criteria, the rep's key activities, and exit criteria stated as buyer actions (for example "buyer has confirmed budget owner and agreed a decision date"), plus a typical duration and a suggested win probability marked as a starting point to calibrate.
5. **Qualification:** a framework sized to the motion (a light one such as BANT for transactional sales, a deeper one such as MEDDICC for complex deals) with the specific questions that answer each element here.
6. **Discovery:** a question bank grouped by situation, problem, impact, decision process and timing, with the answers that signal a strong or weak opportunity.
7. **Objection library:** the ten most likely objections (from the notes first), each with what is really behind it, a response, and proof to use.
8. **Competitor cards:** for each competitor named, where they are strong, where we are strong, landmines to set (questions that expose their weakness fairly) and how to respond to their claims, using only information supplied.
9. **Templates:** first-call recap email, follow-up after a demo, and a proposal cover note, each short.
10. **Metrics and ramp:** the activity, pipeline and outcome metrics to track, and a 30-60-90 day plan for a new rep.
</task>

<constraints>
- Use the company's own evidence first; label anything generic or assumed as "to validate". Do not invent customer names, win rates, deal sizes or competitor facts.
- Competitor cards stay factual and fair: no disparaging claims, no unverified rumours.
- Keep each section skimmable: tables and short bullets, no theory lectures.
- If the company description lacks what is sold, to whom or at what price, ask for those first and stop.
</constraints>

<output_format>
## How we win
Up to five sentences.

## Ideal customer
Bullets, then disqualifiers.

## Buyer personas
A table: Persona | Goals | Fears | Needs to see | Typical questions.

## Sales stages
A table: Stage | Entry criteria | Key activities | Exit criteria (buyer actions) | Typical duration | Starting probability.

## Qualification
The framework with questions per element.

## Discovery
Grouped question lists with strong and weak signals.

## Objection library
A table: Objection | What is behind it | Response | Proof.

## Competitor cards
One short card per competitor.

## Templates
The three templates.

## Metrics and ramp
Metrics table, then the 30-60-90 day plan.

## Gaps
What evidence to gather (call recordings, win/loss interviews) to firm up the parts marked "to validate".
</output_format>
