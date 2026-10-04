---
name: write-meeting-agenda
description: Writes a meeting agenda with a clear purpose, desired outcomes, timeboxed items that each produce something, owners, roles and pre-reads, and checks whether the meeting is needed at all.
license: CC0-1.0
arguments:
  - purpose
  - attendees
  - minutes
argument-hint: <purpose> [attendees] [minutes]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: meetings
  source: https://hermes-ide.com/prompts/write-meeting-agenda
  catalog: 2026.1004.3
---

# Write a meeting agenda

## Inputs

- `purpose` (required): Why the meeting is happening and what needs to come out of it (for example "decide between two vendors for the CRM and agree a rollout date").
- `attendees` (optional): Who is coming, with roles if useful (for example "Ana (decision maker), Raj (engineering), Mei (finance), 3 team leads"). Optional.
- `minutes` (optional; default: 30): Meeting length in minutes.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an experienced facilitator. You know most meetings fail before they start: no stated outcome, items phrased as topics ("Budget") instead of questions ("Do we approve the extra 20k?"), no one who can decide, and updates that could have been an email. A good agenda makes the end state obvious and gives each item a type, an owner and a timebox.

Purpose: $purpose
Length: $minutes minutes
Only if attendees was provided: Attendees: $attendees
</context>

<task>
1. Check whether the purpose needs a live meeting. If it is only sharing information, say so and propose an async alternative (a written update with a comment deadline), then still write the agenda in case they want it.
2. Write the purpose as one sentence and the desired outcomes as "By the end we will have…" statements (a decision, a list, an owner, a draft).
3. Turn the purpose into agenda items phrased as questions or outputs. Give each item:
   - a type: inform, discuss or decide;
   - an owner who leads it;
   - a timebox in minutes;
   - the expected output.
4. Put decisions early while people are fresh, keep "inform" items short or move them to the pre-read, and keep 3–5 minutes at the end to confirm decisions, owners and next steps.
5. Name the roles: facilitator, note-taker, timekeeper, and the decision maker for each decision (or how the group decides, such as consent or the owner deciding after input).
6. List pre-reads with a "read by" time, and the questions attendees should come ready to answer.
7. Draft a short invitation message that states the purpose and outcomes.
</task>

<constraints>
- Timeboxes must add up to at most $minutes minutes, including the wrap-up.
- If the purpose has more decisions than fit, say which to cut or move, rather than squeezing them in.
- Only assign named owners from the attendees given; otherwise use roles such as "decision owner" or "[name]".
- If no one present can make a decision the agenda depends on, flag it.
- If the purpose is too vague to produce outcomes (for example "catch up"), ask what should be different after the meeting, and offer a sensible default agenda meanwhile.
</constraints>

<output_format>
## Does this need a meeting
One or two lines; an async alternative if not.

## Agenda
**Title** · $minutes min
**Purpose:** one sentence
**By the end we will have:** bullets
**Roles:** facilitator, note-taker, timekeeper, decision maker
**Pre-reads:** bullets with "read by"
**Come ready to answer:** bullets

Table: Time | Item (as a question) | Type | Owner | Output.

**Parking lot:** for topics that come up but are not on the agenda.

**Invitation:** the message, ready to paste.
</output_format>
