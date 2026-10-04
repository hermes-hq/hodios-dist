---
name: convert-course-to-online
description: Redesigns an in-person course for online or hybrid delivery, deciding what becomes live or self-paced and how activities, assessment and community change. Use before moving a course online.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: course-design
  source: https://hermes-ide.com/prompts/convert-course-to-online
  catalog: 2026.1004.0
---

# Convert an in-person course to online

## Inputs

- [COURSE_OUTLINE] (required): The current in-person course - weekly topics, session types (lecture, seminar, lab), activities, assessments and class size.
- [PLATFORM] (optional): Optional learning platform and video tool available, e.g. "Moodle and Zoom", "Canvas and Teams". Leave empty for a platform-neutral plan.
- [DELIVERY] (optional; one of: fully-online, hybrid; default: fully-online): fully-online means every student is remote; hybrid means some sessions or some students are in the room and others online.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Moving a course online by streaming the same lectures on a video call ("emergency remote teaching") produces exhausted students and low engagement. A real conversion asks of each activity what it is for, then picks the mode that does that job best online: self-paced (asynchronous) for explanation, reading and reflection people can do at their own pace; live (synchronous) time for discussion, practice with feedback and connection. Online courses need more explicit structure than in-person ones: a predictable weekly rhythm, clear instructions, visible instructor presence and deliberate community building. Assessment usually needs redesign because invigilated exams do not transfer cleanly.
</context>

<task>
Redesign this course for **[DELIVERY]** delivery.

<course_outline>
[COURSE_OUTLINE]
</course_outline>

Only if [PLATFORM] was provided: Available tools: [PLATFORM].

1. If the outline gives no activities or no assessments (for example only a course title), ask for the topics, weekly session types and lengths, assessments and class size in one short list and stop. If only class size or session lengths are missing, assume typical values, state them under Assumptions and continue.
2. **Conversion principles:** 4 to 6 rules you applied, specific to this course.
3. **Activity conversion:** for every current activity, the new mode (live, self-paced, or dropped/merged), the online format (for example a 3 x 8-minute video set with a check question after each; a breakout case discussion; a collaborative document; a virtual or take-home lab) and why.
4. **Weekly rhythm:** a repeating week template with what opens when, live session times and length (no more than about 90 minutes live without a break), and deadlines that do not all fall on the same day. For hybrid, say how in-room and online students take part equally (roles, a room microphone, a co-host who watches the chat).
5. **Assessment changes:** for each assessment, keep, adapt or replace, focusing on what it must evidence. Prefer authentic and open-book tasks, staged submissions and short oral checks over remote proctoring; note the integrity and equity trade-offs.
6. **Community and presence:** week-1 onboarding activities, discussion structures that need real responses (not "post once, reply twice"), small stable groups, and how the instructor shows up each week (announcements, short videos, feedback).
7. **Accessibility and technology:** captions and transcripts, accessible documents, low-bandwidth options, time-zone fairness for live sessions (recordings plus an alternative participation task), and a minimum tech requirements statement.
8. **Instructor workload:** a realistic estimate of build time and weekly running time, and where to save effort (reuse, a teaching assistant, peer feedback).
9. **Pilot checklist:** what to test before launch.
</task>

<constraints>
- Do not simply move every lecture into a live video session; justify each live minute.
- Keep student workload equivalent to the in-person course; list the weekly hours.
- If a platform is named, describe features in general terms and say to check what the institution's version supports; do not invent menu paths.
- Labs, placements or practical skills that cannot be done remotely must be flagged with options (on-campus intensive, kits, simulations) rather than quietly dropped.
</constraints>

<output_format>
## Conversion principles
Numbered.
## Activity conversion
Table: Current activity | Purpose | New mode | Online format | Reason.
## Weekly rhythm
A day-by-day template table, then hybrid notes if relevant.
## Assessment changes
Table: Assessment | Keep / adapt / replace | New design | Integrity and equity notes.
## Community and presence
Bullets.
## Accessibility and technology
Bullets.
## Instructor workload
Build hours and weekly hours with savings.
## Pilot checklist
Checkbox list.
## Assumptions
Bullets: every value you assumed and what the instructor should confirm.
</output_format>
