---
name: meeting-lifecycle-track
description: Takes a meeting from a purpose check through agenda, pre-read, facilitation plan, minutes and follow-up tracking, pausing for approval between steps.
license: CC0-1.0
arguments:
  - purpose
  - attendees
  - date
argument-hint: <purpose> <attendees> [date]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: meetings
  source: https://hermes-ide.com/prompts/meeting-lifecycle-track
  catalog: 2026.1003.1
---

# Meeting lifecycle track

## Inputs

- `purpose` (required): Why the meeting is happening and what should be different afterwards, plus any material you already have (background, options, data).
- `attendees` (required): Who is invited, with roles, and who makes any decision (for example "Ana - decides; Raj - engineering; Mei - finance").
- `date` (optional): When the meeting is planned, with time zone and length if known (for example "Tuesday 14 Oct, 10:00 CET, 45 min"). Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs one meeting end to end, as an experienced facilitator would: purpose check, agenda, pre-read, facilitation plan, minutes, follow-up.

<purpose>
$purpose
</purpose>

<attendees>
$attendees
</attendees>
Only if date was provided: When: $date

Each step produces one artifact and stops for approval or edits; later steps build on the approved versions. The minutes step needs the meeting to have happened: wait for the organiser's notes, transcript or summary. Use only facts the organiser supplied; mark gaps as `[NEEDED: …]` and never record a decision, attendee or commitment that is not in the notes. If the purpose check says the meeting is not needed, offer the async alternative and end unless the organiser wants to continue. If asked to skip approvals, confirm once, then run the remaining pre-meeting steps in one reply and state each choice made.

## Steps

Work through these steps in order. Do not skip a gate.

1. purpose-check (plan)
2. agenda (design)
3. pre-read (build)
4. facilitation (build)
5. minutes (operate)
6. follow-up (review)

### Step 1: Purpose check

Decide whether this needs to be a meeting, and what it must produce.

1. If the purpose is too vague to name an outcome ("catch up", "sync"), ask what should be different afterwards, who decides, and the date and length; then stop.
2. Classify the purpose: decide, solve a problem, plan, share information, build relationships, or a sensitive conversation.
3. Verdict, with one line of reasoning:
   - **Meet:** a complex or contested decision, a hard problem, a sensitive or relationship conversation.
   - **Go async:** mainly sharing information, collecting input or a simple approval. Sketch the alternative in three to five lines (a written update or decision doc with a deadline, or a short recording).
   - **Smaller or shorter:** who is essential and who can get the notes.
4. Brief: **Purpose** (one sentence); **Outcomes** ("By the end we will have…"); **Decision owner and rule**, flagging it if no attendee can decide; **Essential** and **informed-only** attendees; recommended **length** and whether the date leaves time for a pre-read; **Assumptions to confirm**.

Stop for approval, or for the organiser's choice to go async.

**Gate:** stop here and wait for the user's approval before step 2 (agenda).

### Step 2: Agenda

Turn the approved brief into an agenda where every item produces something.

1. Phrase each item as a question or an output ("Which vendor do we choose?", not "Vendors"). Give each:
   - a type: inform, discuss or decide;
   - an owner who leads it, from the attendees;
   - a timebox in minutes;
   - the expected output.
2. Put decisions early, keep inform items short or move them to the pre-read, and keep three to five minutes at the end to confirm decisions, owners and dates.
3. Timeboxes must add up to no more than the approved length; show the sum. If the outcomes do not fit, say which item to cut, move or handle async rather than squeezing it in.
4. Name the roles: facilitator, note-taker, timekeeper, and the decision owner for each decision.
5. Draft the invitation text: purpose, outcomes, agenda, pre-read with a read-by time, and what to come ready to answer.

Output: the agenda as a table (Time | Item | Type | Owner | Output), the roles, a parking-lot line, and the invitation.

Stop and wait for approval. Do not write the pre-read yet.

**Gate:** stop here and wait for the user's approval before step 3 (pre-read).

### Step 3: Pre-read

Write the document attendees read before the meeting, so the meeting is spent deciding, not explaining.

1. Keep it to what a busy attendee will actually read: one to two pages, readable in under ten minutes.
2. Structure:
   - **Why this matters now:** two or three sentences.
   - **What we need from you:** the decisions or input for each agenda item, and the read-by time.
   - **Background:** only the facts needed to take part, from the organiser's material.
   - **Options** for each decision item, with pros, cons and cost or effort, and the recommendation if the organiser has one, clearly labelled as a recommendation.
   - **Open questions** attendees should come ready to answer.
3. Mark every figure, date or fact the organiser has not supplied as `[NEEDED: …]`. Do not fill gaps with plausible numbers.
4. Draft a two-line cover message to send with it.

Stop and wait for approval. Do not write the facilitation plan yet.

**Gate:** stop here and wait for the user's approval before step 4 (facilitation).

### Step 4: Facilitation plan

Prepare the facilitator to run the meeting to its outcomes.

1. **Opening script** (about a minute): purpose, outcomes, decision owner and rule, roles.
2. **Per item:** the opening question, a technique that fits (silent writing, a round, dot-voting, a fist-to-five check), the closing words ("We've decided… Owner… By…"), and what to do on overrun (park, extend by agreement, or go async).
3. **Risks in the room** (a dominant voice, a missing decider, remote people left out, a known disagreement) with a counter-move each; for a tense meeting, add ground rules and phrases for heated moments.
4. **Notes template:** per item, decision, one-line reasoning, actions with owner and date, open questions.
5. **Closing script:** read back decisions and actions, agree who tells whom, quick check on the meeting.

Stop for approval. Then ask the organiser to come back after the meeting with notes, a transcript or a summary.

**Gate:** stop here and wait for the user's approval before step 5 (minutes).

### Step 5: Minutes

Turn what the organiser supplies about the meeting into minutes people can act on.

1. Work only from the notes, transcript or summary supplied. If none has been supplied, ask for it and stop.
2. Write the minutes:
   - **Header:** title, date, attendees and apologies as recorded; `[NEEDED]` for anything not stated.
   - **Decisions:** each in one sentence, who decided, and the reasoning in one line. Only record a decision that was clearly made; anything discussed but not decided goes under open questions.
   - **Actions:** a table of action, owner, due date and status. Leave the owner or date as `[NEEDED]` if the notes do not give them; never assign them yourself.
   - **Agenda items not reached** and **parking-lot items**, with what happens to each.
   - **Open questions.**
3. Compare the outcomes from the approved brief with what happened, and say in two lines which outcomes were achieved and which were not.
4. Draft the email or message sending the minutes, with the decisions and actions first and a request to correct anything within a set time.

Stop and wait for approval. Do not start follow-up tracking yet.

**Gate:** stop here and wait for the user's approval before step 6 (follow-up).

### Step 6: Follow-up tracking

Make sure the decisions and actions actually happen.

1. **Tracker:** Action | Owner | Due | Status | Next check, sorted by due date; actions missing an owner or date come first.
2. **Reminders:** a friendly note per owner for actions due within a week, and a chaser for overdue ones that asks what is blocking them.
3. **Decisions to communicate:** who outside the meeting needs to hear each one, with a two-sentence note.
4. **Open items:** for each missed outcome or open question, the route to close it (async decision with a deadline, a narrower follow-up meeting, or an owner to investigate).
5. **Next meeting:** needed or not, and its purpose if so; one thing to keep and one to change next time.

When the organiser pastes updates, refresh the tracker and reminders. This is the last step.
