---
name: plan-first-week-of-school
description: Plans the first week of a school year day by day, with relationship-building, routines to teach and practise, co-created expectations, low-stakes diagnostics and a family welcome message.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/plan-first-week-of-school
  catalog: 2026.1004.1
---

# Plan the first week of school

## Inputs

- [GRADE_LEVEL] (required): Grade, age or course, e.g. "Kindergarten", "Grade 4", "Year 9 English, five classes".
- [CLASS_CONTEXT] (optional): Optional context, e.g. class size, new or returning students, multilingual learners, students with support plans, co-teachers, school values or policies.
- [SCHEDULE] (optional): Optional timetable for the week, e.g. "full days Mon-Fri, 5 hours with me" or "three 50-minute periods with each class this week".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
The first week sets the norms students will test for the rest of the year. Two things matter most: students feel known and safe, and the routines that will run the room (entering, getting attention, transitions, materials, asking for help, finishing early) are taught explicitly, practised and reinforced like content, not announced once. Teachers who spend the week on rules lectures, or who jump straight into heavy content, usually spend October re-teaching routines. A good first week also starts real learning early, at a level where everyone can succeed, and gives the teacher a light read on where students are.
</context>

<task>
Plan the first week for **[GRADE_LEVEL]**.
Only if [CLASS_CONTEXT] was provided: 
<class_context>
[CLASS_CONTEXT]
</class_context>
Only if [SCHEDULE] was provided: 
<schedule>
[SCHEDULE]
</schedule>

1. Set 3 or 4 priorities for the week, in order.
2. List the 6 to 10 routines that matter most for this age and setting. For each, write the steps as students will learn them, how the teacher models it, how students practise it (including practising it wrong and fixing it, for younger classes), and how it will be reinforced in week 2.
3. Plan each day, fitted to the schedule if given (otherwise assume a typical schedule for the age and say so). Each day includes a relationship-building activity, one or two routines introduced or practised, a short piece of real learning in the subject at an accessible level, and a closing reflection.
4. Plan the expectations co-creation: how students help shape 3 to 5 positively stated class expectations, how they are linked to school rules or values if given, and what each looks like and sounds like.
5. Getting to know students: an interest or learning-profile survey (age-appropriate questions), a low-stakes diagnostic of key prior skills that is not graded, and how to learn names quickly and pronounce them correctly.
6. Write a family welcome message: who the teacher is, what the class will learn this year in a few lines, how to get in touch and when to expect replies, one question inviting families to share something about their child.
7. End-of-week check: how the teacher will know the week worked (routines running with fewer reminders, every student known by name, diagnostic results grouped).
</task>

<constraints>
- Activities must be inclusive: no "what I did on my holiday" tasks that expose differences in family income, no activities that require sharing personal or family details students may not want to share, and options for students who are shy, new to the language or new to the school.
- Keep teacher talk short at a time for the age (roughly the age in years plus a few minutes for younger students) and include movement.
- Every routine is described as observable steps, not values ("hands empty, eyes on me, voices off within 5 seconds", not "be respectful").
- Use only materials a typical classroom has.
- For secondary teachers with several classes, plan the routines once and say how to adapt the pacing across classes.
- If the grade or setting is unusual (for example an alternative provision or adult class), say what you assumed.
</constraints>

<output_format>
## Priorities for the week
Numbered.
## Routines to teach
Table: Routine | Steps for students | How it is modelled and practised | Reinforce in week 2.
## Day-by-day plan
One subsection per day: a time-blocked list with activity, purpose and materials.
## Expectations co-creation
Process, then a draft set with "looks like / sounds like".
## Getting to know students
Survey questions, diagnostic outline, name strategy.
## Family welcome message
The message, under about 200 words, with [placeholders].
## End-of-week check
Bullets.
</output_format>
