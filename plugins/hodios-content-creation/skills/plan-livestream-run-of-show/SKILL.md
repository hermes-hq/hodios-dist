---
name: plan-livestream-run-of-show
description: Plans a livestream or webinar run of show with timed segments, production cues, audience interaction, roles and contingency plans. Use when preparing a live broadcast.
license: CC0-1.0
arguments:
  - event
  - duration_minutes
  - platform
argument-hint: <event> [duration_minutes] [platform]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: video
  source: https://hermes-ide.com/prompts/plan-livestream-run-of-show
  catalog: 2026.1003.2
---

# Plan a livestream run of show

## Inputs

- `event` (required): What the stream or webinar is, its goal, who is presenting, the audience, and any fixed elements (demo, guest, product launch, Q&A, offer).
- `duration_minutes` (optional; default: 60): Scheduled length of the live portion in minutes.
- `platform` (optional): Where it streams (for example YouTube Live, Twitch, LinkedIn Live, Zoom webinar). Leave empty for a platform-neutral plan.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a live producer who has run streams and webinars where things went wrong on air. Live audiences behave predictably: people trickle in for the first five minutes, attention dips after about ten minutes without interaction, the chat wants to be acknowledged, Q&A starts slowly unless someone primes it, and segments run long. A run of show is the document the whole team works from: every segment has a clock time, an owner, the cue that starts it and what the audience is doing. Good plans also say what happens when the stream drops, a guest is late or the demo breaks.
</context>

<task>
Plan a run of show for a $duration_minutes-minute live event.

<platform>
$platform
</platform>

<event>
$event
</event>

1. State the goal (the one thing that makes this stream a success, such as sign-ups, questions answered or a launch moment) and list any assumptions you had to make about presenters, audience size or production setup.
2. Assign roles: host, producer (switching and timing), chat moderator, and guests. If the team is one person, say which duties to drop or automate.
3. Write the pre-show checklist from T-60 to T-0: tech check (audio, camera, scenes, screen share, backup connection), content check (slides, demo environment, links ready to paste), and a soft-open plan.
4. Build the run of show:
   - A soft open in the first three to five minutes that welcomes people as they join, with no essential content.
   - Segments in the order that serves the goal, each with start time (T+mm:ss), length, owner, content or talking points, production cue (scene, slide, lower third, music, screen share), and the audience interaction.
   - An interaction at least every 10 minutes (a poll, a chat prompt, a shout-out, a question).
   - Q&A with three seeded questions in case chat is slow.
   - The call to action, stated live and pinned in chat, placed before the final segment so people who leave early still hear it.
   - About 10% of the time as buffer, and a hard out.
5. Write contingencies: for each likely failure (stream or connection drops, audio fails, guest late or absent, demo breaks, no questions, hostile or spam chat, running over), the trigger, who acts and the exact response.
6. List what happens after the stream: replay edits, follow-up message, clips to cut.
</task>

<constraints>
- Times must add up exactly to $duration_minutes minutes including the buffer.
- Do not invent names, products, offers or links; use role names and `[FILL: …]` placeholders.
- If the platform is not given, keep cues generic and note where platform features (polls, pinned messages, co-hosts) differ.
- If the event lacks a goal or presenters, state your assumption in the first section instead of guessing silently.
</constraints>

<output_format>
## Goal and assumptions
## Roles
## Pre-show checklist
A checklist with T-minus times.
## Run of show
A table: start | length | segment | owner | content | cue | audience interaction.
## Contingencies
A table: failure | trigger | who | response.
## After the stream
Bullets.
</output_format>
