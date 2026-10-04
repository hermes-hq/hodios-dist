---
name: plan-after-school-club
description: Plans a term of an after-school club such as coding, robotics, chess, art or debate, with session plans, a skill progression, mixed-ability options and an end-of-term showcase.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: course-design
  source: https://hermes-ide.com/prompts/plan-after-school-club
  catalog: 2026.1004.3
---

# Plan a term of an after-school club

## Inputs

- [CLUB_TYPE] (required): What the club does, with any equipment you have, e.g. "robotics club with 6 LEGO robotics kits and 8 laptops", "chess club".
- [AGES] (required): Ages or grades of the members and roughly how many, e.g. "ages 9-11, about 15 children".
- [SESSIONS] (optional; default: 10): Number of weekly sessions in the term.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
After-school clubs are voluntary, so children vote with their feet. Clubs that last feel different from lessons: members are doing the thing within five minutes, they make or play something every session, they see themselves getting better, and they work toward something they can show. Leaders face mixed ages and abilities, irregular attendance, tired children at the end of the school day and limited equipment, so each session must stand on its own while still building a progression across the term.
</context>

<task>
Plan [SESSIONS] sessions of a **[CLUB_TYPE]** club for **[AGES]**.

1. If the session length, equipment or number of children is unknown, assume 60 minutes, basic equipment for the activity and about 15 children, and list these assumptions; ask nothing unless the club type itself is unclear.
2. **Club overview:** what members will be able to do by the end of term, in child-friendly words, and the club's rhythm.
3. **Skill progression:** 3 to 4 stages across the term (for example "first moves → tactics → full games → tournament") with what a member can do at each stage.
4. **Session template:** a repeating structure that suits tired children: an arrival activity that anyone can join late (5 to 10 minutes), a short demo or challenge introduction (no more than about 10 minutes of talk), the main hands-on activity, a share or show moment, and tidy-up.
5. **Session plans:** for each of the [SESSIONS] sessions, the goal, the main activity, the equipment, a "level up" challenge for confident members and an easier entry for newcomers or younger members. Make every session work for a child who missed the previous one.
6. **Showcase:** an end-of-term event (exhibition, tournament, demo, debate with an audience) with what each member contributes, how families are invited, and how to make sure every child has something to show.
7. **Logistics and safety:** equipment per session, setup time, supervision and adult-to-child ratios to check against the school's or organisation's policy, collection and sign-out, consent for photos at the showcase, and any activity-specific safety (tools, hot glue, online accounts and data for coding clubs).
</task>

<constraints>
- Match activities to the stated ages: reading load, fine motor skills and attention span.
- Keep demos short and the hands-on time long; every session produces something visible (a build, a game played, a speech given, a piece made).
- Do not assume extra budget or equipment beyond what was stated; suggest optional low-cost extras separately.
- Do not state safeguarding ratios or legal requirements as fact; mark them as items to check with the school or local rules.
- Any online tool for children must be age-appropriate and approved by the school; do not require children to create personal accounts without parental and school consent.
</constraints>

<output_format>
## Club overview
Short paragraph and "By the end of term, you'll be able to…" bullets.
## Skill progression
Table: Stage | Sessions | Members can….
## Session template
Timed list.
## Session plans
Table: # | Goal | Main activity | Equipment | Level up | Easier entry.
## Showcase
Bullets.
## Logistics and safety
Checklist.
## Assumptions
Bullets.
</output_format>
