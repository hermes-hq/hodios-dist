---
name: design-microlearning-series
description: Designs a series of five-minute lessons delivered over days, each with one objective, a hook, a practice item with feedback and spaced recall of earlier lessons.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: course-design
  source: https://hermes-ide.com/prompts/design-microlearning-series
  catalog: 2026.1003.1
---

# Design a microlearning series

## Inputs

- [TOPIC] (required): What the series teaches, e.g. "giving feedback with the SBI model", "spotting phishing emails", "basic food hygiene for new kitchen staff".
- [AUDIENCE] (required): Who it is for and what they already know, e.g. "first-time team leads in retail, no management training".
- [LESSON_COUNT] (optional; default: 10): Number of lessons in the series.
- [CHANNEL] (optional; one of: email, chat, app, video; default: email): How lessons are delivered.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Microlearning works when each piece is small because it is focused, not because a long course was chopped into slices. A good five-minute lesson has one objective, starts with a hook that makes the learner care (a scenario, a surprising fact, a mistake they recognise), teaches one idea with one concrete example, and asks the learner to do something with it straight away. Across a series, the strongest lever is retrieval spaced over time: each lesson asks a quick question about an earlier one, at growing intervals, so knowledge is pulled back before it fades. The channel shapes the format: an email can carry a short read, a chat message must be shorter still, a video lesson needs a script.
</context>

<task>
Design a [LESSON_COUNT]-lesson microlearning series on **[TOPIC]** for **[AUDIENCE]**, delivered by **[CHANNEL]**.

1. **Series overview:** the overall performance goal (what learners will do differently at work or in life), why microlearning suits it, the cadence (for example every working day), and the total time per lesson.
2. **Objectives map:** split the goal into [LESSON_COUNT] single objectives, one per lesson, each with an observable verb, sequenced so each builds on the last. Group them into 2 to 4 themes.
3. **Schedule:** the delivery day for each lesson and which earlier lessons each one recalls, using expanding gaps (for example recall lesson 1 in lessons 2, 4 and 8).
4. **Lessons:** for each lesson write:
   - title and objective;
   - the hook (one or two sentences);
   - the core content in the channel's format: email about 150 to 250 words; chat 3 to 5 short messages; app a few screens of text with a prompt; video a 60 to 120 second script with on-screen text cues;
   - one practice item (scenario question, choose the better response, spot the mistake, or a do-it-today task) with feedback for each answer, explaining why;
   - one spaced recall question on an earlier lesson, with the answer (from lesson 2 onwards);
   - a one-line "try this today" action.
5. **Final check:** a 5 to 8 item scenario-based check covering the whole series, with answers, and one reflection question about applying it.
</task>

<constraints>
- One idea per lesson; if the topic needs more than [LESSON_COUNT] lessons to do properly, say what you would cut or add.
- Keep each lesson to about five minutes of the learner's time, including the practice.
- Practice items test application in realistic situations, not recall of the lesson's wording. Distractors reflect real mistakes.
- Plain, friendly language for the audience; no jargon without a definition.
- Use only accurate content. For regulated topics (safety, food hygiene, compliance) state that content must be checked against the organisation's policies and local regulations, and do not invent specific legal requirements or figures.
- If the topic is too broad for a series (for example "management"), narrow it, say how, and design for the narrower topic.
</constraints>

<output_format>
## Series overview
Bullets.
## Objectives map
Table: Lesson | Theme | Objective.
## Schedule
Table: Lesson | Day | Recalls lessons.
## Lessons
One subsection per lesson with the parts in step 4, labelled.
## Final check
Numbered items with answers, then the reflection question.
</output_format>
