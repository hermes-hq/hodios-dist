---
name: plan-kids-summer
description: Plans a summer holiday for children with a week-by-week overview, a weekly rhythm, camps or childcare to research, an activity bank by age, a budget and screen limits.
license: CC0-1.0
arguments:
  - children_and_ages
  - budget
  - parents_work
argument-hint: <children_and_ages> [budget] [parents_work]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: kids-activities
  source: https://hermes-ide.com/prompts/plan-kids-summer
  catalog: 2026.1004.0
---

# Plan the kids' summer

## Inputs

- `children_and_ages` (required): Each child's age and interests, needs and friends, for example "Maya 9, loves swimming and drawing, anxious about new groups; Tom 5, ADHD, needs lots of outdoor time". Include holiday dates if you know them.
- `budget` (optional): Rough total or weekly budget for childcare and activities, for example "about 1,500 for the summer". Optional.
- `parents_work` (optional): Work patterns and time off for each parent or carer, family trips already booked, and help from relatives. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help parents plan a long school holiday so it covers work, fits the budget and gives children a mix of adventure, friends, rest and a little learning, without over-scheduling. The planning problem is mostly coverage: matching weeks of childcare to the parents' work, then filling the rest with a simple rhythm children can rely on. Popular camps and holiday clubs often fill early, so the plan includes what to book and by when.

<children_and_ages>
$children_and_ages
</children_and_ages>
Only if budget was provided: Budget: $budget
Only if parents_work was provided: 
<parents_work>
$parents_work
</parents_work>
</context>

<task>
1. Summer at a glance: a week-by-week table of the holiday showing for each week who is looking after the children (a parent, a relative, a camp or club, a trip) and gaps where no one is available yet. If dates are unknown, assume a typical length and say so.
2. Weekly rhythm: a simple template for home weeks, with a theme or anchor per day (for example outing day, friends day, library day, home project day, lazy day), consistent wake and bed times, outdoor time every day, and quiet time.
3. Camps and care to research: types that fit each child's age, interests and needs (day camps, sports or arts camps, holiday clubs at schools or community centres, library programmes, swapping days with other families, relatives), with the questions to ask (hours and wraparound care, ratios and staff checks, cost and discounts, how they support children with additional needs, food, refunds) and search terms to find local options. Never invent names, prices or dates.
4. Activity bank: ideas by age and interest, including free and low-cost ones (parks, libraries, museums with free days, nature walks, cooking, backyard projects, a summer reading challenge), a few bigger outings, and rainy-day backups. Include a light learning thread (reading together, a project) without making it school.
5. Budget: a table splitting the budget across childcare, activities, outings and a buffer, with cheaper alternatives if it does not stretch. If no budget is given, give a low, medium and higher option in proportions rather than prices.
6. Screens and downtime: a simple screen plan (for example after outdoor time, a daily limit set by the family, screen-free meals and mornings), boredom as normal and useful, and downtime protected for anxious or easily overwhelmed children.
7. Book by: a dated checklist of what to book first.
</task>

<constraints>
- Plan around each child's needs from the input (age, additional needs, anxiety, friendships); do not diagnose or give medical advice.
- Do not invent specific providers, prices, opening times or eligibility; tell them what to look up.
- Keep it realistic for working parents: do not fill every day with parent-led activities on work days.
- Supervision: say which activities need an adult (water, cooking, tools) and match independence to age. Never fill a coverage gap by leaving a child home alone or in an older sibling's charge for whole working days. If the parents suggest it, say the age at which this is allowed or advised varies by country and region, tell them to check local guidance, and judge readiness by the child's maturity, not age alone; offer a short, staged trial (an hour or two with check-ins) only for children old enough under that guidance, and keep looking for care for the rest.
- If key information is missing (holiday dates, work patterns), state the assumption and list it at the end.
</constraints>

<output_format>
## Summer at a glance
Table: Week | Dates | Who has the kids | Plan | Gap?
## Weekly rhythm
Table: Day | Anchor | Ideas.
## Camps and care to research
Per child: types, questions to ask, search terms.
## Activity bank
Grouped by free, low-cost, big outings and rainy days.
## Budget
Table.
## Screens and downtime
## Book by
Dated checklist, then assumptions.
</output_format>
