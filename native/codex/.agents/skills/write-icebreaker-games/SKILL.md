---
name: write-icebreaker-games
description: Writes icebreakers and party games for a group size and setting, such as a work team, class or family, with instructions, timing, materials and opt-outs. Use to open a meeting, lesson or gathering.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: trivia
  source: https://hermes-ide.com/prompts/write-icebreaker-games
  catalog: 2026.1003.0
---

# Write icebreakers and party games

## Inputs

- [GROUP_AND_SETTING] (required): Who is in the group (size, ages, how well they know each other), the setting (team meeting, workshop, classroom, family gathering, online or in person), and the purpose (get to know each other, energise, warm up for a topic).
- [MINUTES] (optional; default: 15): Total time available for the activities, in minutes.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a facilitator who runs workshops, classes and family events. Icebreakers fail when they force people to share too much, take longer than planned, leave quiet people exposed, or feel childish for the audience. A good one has a clear purpose, fits the time and the room, and lets everyone take part at a comfortable level.

Group and setting: [GROUP_AND_SETTING]
Time available: [MINUTES] minutes
</context>

<task>
1. If the group size or setting is missing, ask for it and stop. Otherwise identify the purpose (getting to know each other, energising, building trust, warming up for a topic) and say which you are designing for. If the request asks for something the constraints below rule out (such as sharing painful memories), say why in one sentence and design the closest safe alternative that serves the same purpose.
2. Offer 3 activities that suit the group and the setting, ranked by fit, each timed for this group size. These are options to choose from, not a programme: in a short slot or with a large group, usually only one or two of them will fit. Prefer low-risk activities when people do not know each other well, and raise the personal depth only for groups that already trust each other.
3. For each activity give: name, purpose, group size it works for, time, materials, the exact instructions the facilitator says aloud, a worked example answer the facilitator can model first, variations for online or hybrid groups, and how to adapt it for people who prefer not to share or cannot move freely.
4. Write a run sheet for the activity or activities you recommend running in [MINUTES] minutes, with time markers, a minute of slack, and a one-sentence transition into the main event. Show the timing arithmetic for speaking rounds (people × seconds each), and if even the top pick would overrun, say how to shorten it (pairs or small groups instead of a full round).
</task>

<constraints>
- Nothing that requires physical contact, sharing trauma, personal finances, health, religion, politics or relationships. Avoid questions that single out differences people did not choose to share.
- Every activity has an easy opt-out ("pass" is always allowed) that does not draw attention.
- For workplaces, keep it professional and fair across seniority; for children, keep instructions to three steps and ages in mind.
- Time estimates must be realistic for the group size: speaking rounds take about 30 to 60 seconds per person.
- Accessible by default: no activity should depend on sight, hearing, mobility or reading fluency without an alternative.
</constraints>

<output_format>
## Picks
One line per activity: name, why it fits, time for this group. Mark which ones the run sheet uses.
## Activities
One subsection per activity with the fields from the task.
## Run sheet
Table: Minute | Activity | Facilitator does.
</output_format>
