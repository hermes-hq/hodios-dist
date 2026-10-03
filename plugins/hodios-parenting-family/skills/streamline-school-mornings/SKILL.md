---
name: streamline-school-mornings
description: Streamlines school-day mornings with a backwards timed schedule, a night-before routine, picture or word checklists per child and specific fixes for the household's bottlenecks.
license: CC0-1.0
arguments:
  - children
  - bottlenecks
  - leave_time
argument-hint: <children> <bottlenecks> <leave_time>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: family-logistics
  source: https://hermes-ide.com/prompts/streamline-school-mornings
  catalog: 2026.1003.2
---

# Streamline school mornings

## Inputs

- `children` (required): Each child's age and anything relevant, for example "6 (can't read yet, slow eater), 11 (wants a shower every morning), baby 1".
- `bottlenecks` (required): Where mornings break down, for example "one bathroom for five people", "can never find shoes", "arguments over the TV", "I'm making lunches at 8am", plus the adults' work start times.
- `leave_time` (required): The time you need to leave the house, for example "8:05".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You fix chaotic school mornings. Most morning stress comes from a few predictable causes: decisions left until the morning (clothes, lunches, lost shoes), a schedule with no buffer, parents acting as the children's memory, screens that are hard to switch off, and one shared bottleneck such as a bathroom. The fixes: move every possible decision to the evening, plan backwards from the leave time with a 10–15 minute buffer, put each child's steps on a visible checklist (pictures for non-readers), make screens and treats conditional on being ready ("when you're ready, then"), and give the parents a head start.

Children: $children
Leave time: $leave_time

<bottlenecks>
$bottlenecks
</bottlenecks>
</context>

<task>
1. Your morning at a glance: a timed schedule built backwards from $leave_time, including a buffer before leaving, the parents' wake-up time, each child's wake-up time (staggered if there is a bathroom queue), and who is where at each point. State any assumptions about how long things take.
2. The night before: a 15-minute evening routine (bags packed and by the door, clothes chosen including shoes and coats, lunches made or prepared, forms signed, the next day's activities checked, breakfast set out), with who does what, adjusted to the children's ages.
3. Checklists for each child: a short, ordered checklist per child that they can follow by themselves, with picture prompts described for children who cannot read, and where to put it (bedroom door, bathroom mirror).
4. Fixes for your bottlenecks: for each bottleneck named, the specific fix and why it works (for example, a bathroom rota; a "launch pad" by the door for shoes, bags and keys; breakfast on the table before the children come down; no screens until ready, then whatever time is left).
5. Your own routine: what the parents do before the children wake or in parallel so they are not rushing, and how to split jobs between adults if there are two.
6. Making it stick: run it for two weeks, start with a "practice morning" at the weekend, praise each child for following their list, adjust timings at the end of week one, and keep the evening routine non-negotiable.
</task>

<constraints>
- Fit every step to the child's age: a 4-year-old needs help with dressing; a 12-year-old can own their own checklist and alarm.
- Keep the morning calm: no punishments, threats or rewards that cost money every day; use simple when-then rules and praise.
- If a child's morning struggles look like more than habit (school refusal, stomach aches every school day, extreme distress), say gently that it may be worth talking to the school or the family doctor.
- Use the times and details given; if a key fact is missing (school start time, travel time), state an assumption.
- Short and scannable; this will be printed and stuck on the fridge.
</constraints>

<output_format>
## Your morning at a glance
Table: Time | Adults | one column per child, headed by age (for example "Age 6"), with a "Bathroom" column if it is shared.
## The night before
## Checklists for each child
One short checklist per child.
## Fixes for your bottlenecks
Table: Bottleneck | Fix | Why it works.
## Your own routine
## Making it stick
</output_format>
