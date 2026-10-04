---
name: moderate-panel
description: Prepares a panel moderator with a timed run of show, opening, speaker introductions, a question flow with follow-ups, tactics for dominant or quiet speakers, audience Q&A and a close.
license: CC0-1.0
arguments:
  - topic
  - panelists
  - duration_minutes
argument-hint: <topic> <panelists> [duration_minutes]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: public-speaking
  source: https://hermes-ide.com/prompts/moderate-panel
  catalog: 2026.1004.1
---

# Prepare to moderate a panel

## Inputs

- `topic` (required): The panel's topic and angle, the event and audience, and what the organiser wants attendees to take away.
- `panelists` (required): Each panellist's name, role, organisation, the perspective or expertise they bring, and anything known about their views or speaking style (for example "talks at length", "new to panels").
- `duration_minutes` (optional; default: 45): Length of the session in minutes, including audience Q&A.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A panel is a conversation the audience overhears, and the moderator is the audience's representative on stage. Panels fail in familiar ways: five-minute self-introductions, questions that every panellist answers in turn until the time is gone, one panellist dominating, polite agreement with no tension, and a rushed audience Q&A where someone gives a speech instead of asking a question. Good moderators keep their own airtime under about 15%, introduce panellists briefly themselves, direct questions to a named person, ask follow-ups that sharpen ("Can you give an example?" "Where do you disagree with that?"), surface real differences, and keep time visibly.
</context>

<task>
Prepare me to moderate this $duration_minutes-minute panel.

<topic>
$topic
</topic>

<panelists>
$panelists
</panelists>

1. If the topic angle or the panellists' perspectives are too thin to write targeted questions, ask up to three short questions and stop.
2. Find the panel's central question and two or three real tensions between panellists' perspectives worth exploring.
3. Build a run of show that fits $duration_minutes minutes: opening (about 2 minutes), introductions (about 30 seconds per person, done by the moderator), discussion in two or three themed blocks, audience Q&A (about a third of the time), and close (about 2 minutes).
4. Write the opening: a hook that makes the topic matter to this audience, the central question, and the format, including when audience Q&A happens.
5. Write a two-sentence introduction for each panellist, done by the moderator, focused on why their perspective matters here, using only facts given.
6. Write the question flow: an opening question that every panellist answers in under a minute; then per block, two or three questions each directed to a named panellist, with the intended follow-up and an invitation for another panellist to respond or disagree. Include one question that surfaces a real tension, and one that asks for a concrete example or a practical takeaway.
7. Give tactics for managing the panel: phrases to interrupt a long answer politely, bring in a quiet panellist, redirect off-topic answers, handle a factual error or a heated moment, and keep time.
8. Plan audience Q&A: how to take questions (microphone runner, app or cards), how to cut a speech short politely, how to repeat questions for the room and the recording, and two backup questions if the room is quiet.
9. Write the close: a lightning round (one sentence each), a thank-you, and the handover to the host.
10. Draft a short prep email to panellists: the format, the themes (not every question), timings and a request to keep answers to about 90 seconds.
</task>

<constraints>
- Use only facts given about panellists; mark missing details `[NEEDED: …]`. Never attribute opinions to panellists that the input does not support; frame tension questions as open invitations.
- Questions are open, specific and short (one sentence). No multi-part questions and no "So, what's the future of X?".
- The moderator does not answer questions or give mini-speeches.
- Treat panellists even-handedly; give each roughly equal airtime in the plan.
</constraints>

<output_format>
## Run of show
Table: Time | Segment | Who | Notes. Total row.
## Opening
The script.
## Introductions
One short paragraph per panellist.
## Question flow
By block: question, to whom, follow-up, invite to respond.
## Managing the panel
Situation | What to say.
## Audience Q&A
Process, handling lines and backup questions.
## Close
The script.
## Prep email to panellists
Subject and email.
</output_format>
