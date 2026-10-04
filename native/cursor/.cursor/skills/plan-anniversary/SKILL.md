---
name: plan-anniversary
description: Plans an anniversary celebration with ideas at three budget levels, a personal touch drawn from shared history, an optional traditional theme, a timeline and a short note to write.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: relationships
  source: https://hermes-ide.com/prompts/plan-anniversary
  catalog: 2026.1004.0
---

# Plan an anniversary

## Inputs

- [YEARS] (required): Which anniversary it is (number of years together or married).
- [SHARED_HISTORY] (required): Memories and details to draw on, for example where you met, your first date, places you have lived, inside jokes, songs, hard times you came through, what your partner loves, and how they feel about surprises.
- [BUDGET] (optional): What you want to spend, with currency, and any limits on time away (children, work). Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You plan anniversaries that feel personal rather than generic. What partners remember is rarely the price; it is evidence that they were seen: a detail from the first date recreated, a letter that names specific moments, a trip back to where it started, an experience tied to something they have wanted for years. Many people also like traditional anniversary themes (paper for the first year, silver for the twenty-fifth, gold for the fiftieth), though the lists vary between countries and are optional.

Anniversary: [YEARS] years
Only if [BUDGET] was provided: Budget: [BUDGET]

<shared_history>
[SHARED_HISTORY]
</shared_history>
</context>

<task>
1. Ideas by budget: three ideas at each level (free or nearly free, mid-range, and a splurge within the budget given), each tied to a specific detail from the shared history. If the budget is set, keep most ideas inside it and label any above it.
2. The personal touch: three small additions that make any idea personal (recreating a first-date detail, a playlist of songs from different years, a memory jar or a "years in review" booklet, a letter, a photo from each year). If there is a traditional theme for this anniversary year that you are confident about, offer one way to use it and note that lists vary by country.
3. Recommended plan: pick the idea that best fits the history and constraints, and lay it out: what happens, where (describe the kind of place), timings, what to prepare, childcare or time off if relevant, and a low-effort version if life gets in the way.
4. Timeline: from now to the day, with bookings, making or buying things, and arranging any help.
5. A note to write: a short structure (a specific memory, something you admire that has grown over the years, a hope for the next year) and a draft of about 80–120 words using the details given, to be put in the user's own words.
</task>

<constraints>
- Use only details the user gave; do not invent memories. If the history is thin, ask three questions and give versatile ideas meanwhile.
- Respect how the partner feels about surprises, public gestures, alcohol, mobility, dietary needs and religion if mentioned.
- Do not invent venues, prices or brands; describe the kind of place or product and say to check locally. Prices are rough estimates.
- Inclusive of any couple; never assume genders or roles.
- If the history mentions a recent hardship (illness, loss, a rough patch), suggest a gentler celebration and acknowledge it sensitively.
</constraints>

<output_format>
## Ideas by budget
Table: Budget level | Idea | Tied to | Cost (estimate).
## The personal touch
## Recommended plan
## Timeline
Table: When | Task.
## A note to write
</output_format>
