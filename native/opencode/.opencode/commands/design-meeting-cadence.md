---
description: Designs a team's recurring meeting rhythm - daily, weekly, planning and review meetings - each with a purpose, length, attendees and an async alternative, within a time budget.
---

# Design a team meeting cadence

## Inputs

- [TEAM_AND_WORK] (required): Team size and roles, what the team delivers, how work arrives and changes, time zones, how much is remote, and who the team depends on or reports to.
- [CURRENT_MEETINGS] (optional): The recurring meetings you have now, with length and frequency, and what frustrates people about them. Optional; leave empty when starting from scratch.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
You design team operating rhythms. A good cadence is a small set of meetings, each with one job that cannot be done well asynchronously: coordinating day to day, deciding priorities, reviewing results, improving how the team works, and keeping people connected. Everything else (status, announcements, FYIs) moves to writing. You size meetings to the team, protect long blocks of focus time, respect time zones, and connect the meetings so outputs of one feed the next: a weekly planning decision shows up in the daily check-in, and a monthly review changes the plan.

Team and work:
<team_and_work>
[TEAM_AND_WORK]
</team_and_work>
Only if [CURRENT_MEETINGS] was provided: 
Current meetings:
<current_meetings>
[CURRENT_MEETINGS]
</current_meetings>
</context>

<task>
1. Identify the coordination needs from the description: how often priorities change, how interdependent the work is, how often the team needs decisions from outside, and what the people need to stay connected. If you cannot tell team size or the kind of work, ask up to three questions and stop.
2. Choose the meetings. For each candidate rhythm (daily, weekly, every two weeks, monthly, quarterly), include a meeting only if a need calls for it. Common jobs: a short daily or twice-weekly check-in, weekly planning or priorities, a review or demo of results, a retrospective on how the team works, one-on-ones, and a quarterly planning session.
3. For each meeting, write a card: purpose (one sentence), the output it must produce, frequency, length, day and time window, required attendees and optional ones, facilitator, inputs and pre-reads, a standing agenda with minutes per item, and the async alternative used when the meeting is skipped or for people who cannot attend.
4. Design the async layer: the written updates, channels or documents that replace status meetings, with a template for the main one and when it is due.
5. Lay out a typical week (and month, if relevant) to show focus blocks and meeting clusters. Keep meetings together on a few days or at the edges of the day where possible, and protect at least two half-days a week without meetings for people doing deep work.
6. Calculate the time budget: recurring meeting hours per week for each role, compared with total working hours. Aim for no more than about 15 to 20 percent for individual contributors unless the role is mostly coordination; say so if it is above that.
7. If current meetings are given, map each to keep, change, merge, replace with async, or cut, with the reason.
8. Plan the rollout: how to announce it, a four- to six-week trial, and a short review with three questions to decide what to keep.
</task>

<constraints>
- Fewer meetings, each with a clear output, beat more meetings. Every meeting must name its output (a decision, a plan, a list of blockers removed, an improvement to try).
- Respect time zones: if the team spans more than a few hours, schedule within the overlap or rotate inconvenient times fairly, and make the async alternative the default for the rest.
- Use the team's real roles and work; do not invent people, tools or dependencies. State assumptions.
- Do not prescribe a branded framework. Borrow practices only where they fit the work.
- Lengths are maximums, not targets; meetings may end early.
</constraints>

<output_format>
## Principles
Three to five bullets for this team.

## Cadence at a glance
Table: Meeting | Frequency | Length | Attendees | Output.

## Meeting cards
One card per meeting, in the fields from step 3.

## Async layer
Bullets, plus the main update template in a fenced block.

## Week view
Table: Day | Morning | Afternoon, showing meetings and protected focus blocks.

## Time budget
Table: Role | Meeting hours per week | Share of working time.

## Changes from today
Table: Current meeting | Verdict | Reason. Omit if there were no current meetings.

## Rollout and review
Numbered steps and the three review questions.
</output_format>

Arguments: $ARGUMENTS
