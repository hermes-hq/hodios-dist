---
name: weekly-meal-planning-track
description: Runs a weekly meal planning routine in gated steps, from reviewing the week's calendar to picking meals, building the grocery list, planning prep and reviewing leftovers and waste.
license: CC0-1.0
metadata:
  version: 1.1.0
  kind: workflow
  category: meal-planning
  source: https://hermes-ide.com/prompts/weekly-meal-planning-track
  catalog: 2026.1003.1
---

# Weekly meal planning track

## Inputs

- [HOUSEHOLD] (required): Who eats, ages, diets and allergies, meals you want planned, weeknight cooking time, meals the household already loves, and the shop or delivery you use.
- [BUDGET] (optional): Weekly food budget with currency. Optional.
- [LAST_WEEK] (optional): How last week went if you are coming back, such as meals cooked or skipped and why, what was thrown away and what everyone loved. Optional; step 1 carries the lessons into this week.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Runs the same five-step routine every week, the way an organised household does it: look at the week ahead, choose meals that fit it, write one grocery list, plan the prep, and at the end of the week review what was eaten and wasted so next week's plan is better. Each step produces one short artifact and stops for approval; later steps build on approved versions and do not reopen settled choices without asking. The routine is meant to repeat, so the review feeds the next week's first step.

<household>
[HOUSEHOLD]
</household>
Only if [BUDGET] was provided: Budget: [BUDGET]
Only if [LAST_WEEK] was provided: 
How last week went:
<last_week>
[LAST_WEEK]
</last_week>

Rules for every step:
- Respect every diet and allergy in the household text, including hidden sources, and flag label checks for serious allergies.
- If a dietary need is medical, plan sensibly and say the household's doctor or dietitian sets the targets; do not prescribe calories or nutrient limits.
- Leftovers: cooked food is usually best eaten within about 3–4 days refrigerated, frozen if planned for later, and reheated until steaming hot, once. Guidance varies by country.
- Prices are estimates in the household's currency and are labelled as such.
- If the person asks to skip approvals, confirm once, then run the remaining steps and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. calendar (plan)
2. meals (plan)
3. grocery-list (plan)
4. prep (operate)
5. review (review)

### Step 1: Review the week

Map the week before choosing any food, so the plan fits real life.

1. If the household text does not say who eats, which meals to plan, or the cooking time on weeknights, ask for them in one short message and stop.
2. Ask, in one short batch, about this specific week: late nights and early starts, evenings out or guests, sports and activities, travel, who is home to cook each night, and anything in the fridge or freezer that needs using. If last week's notes are given or last week's review is in the conversation, first summarise in two or three lines what to keep and what to change, carry those lessons into the day types (for example a night that keeps falling apart becomes busy or leftovers), and list last week's leftovers and fridge items that still keep under Use up first.
3. Classify each day: **busy** (15 minutes or a ready meal or leftovers), **normal** (30–40 minutes), **free** (time for a bigger cook that makes leftovers), or **out** (no meal needed).
4. Pick the leftovers and use-up nights: at least one leftover night and one fridge clear-out night near the end of the week.

Write it as Markdown with sections Lessons from last week (only when there are notes), This week, Day types (table: Day | Who's home | Type | Notes), Use up first. Keep it under half a page.

Stop for approval or edits. Do not choose meals yet.

**Gate:** stop here and wait for the user's approval before step 2 (meals).

### Step 2: Pick the meals

Choose meals that fit the approved day types.

1. Match meals to day types: the quickest meals on busy days, one bigger "cook once, eat twice" meal on a free day, and leftovers or the fridge clear-out on the nights chosen in step 1.
2. Build mostly from meals the household already loves; add at most one new meal this week unless they asked for more variety.
3. Share perishables: every fresh ingredient bought for one meal appears in at least one other meal or the clear-out night.
4. Vary proteins and cooking methods across the week, and include vegetables in every dinner.
5. Use up the items listed in step 1 early in the week.
6. If a budget is given, keep the meals within it and note cheaper swaps.

Write it as Markdown with sections The week (table: Day | Meal | Time | Shares ingredients with | Makes leftovers for), New this week, Swaps if plans change. Keep it under one page.

Stop for approval or edits.

**Gate:** stop here and wait for the user's approval before step 3 (grocery-list).

### Step 3: Build the grocery list

Turn the approved meals into one list for one shop.

1. List every ingredient for the approved meals, merged across meals and converted to amounts the shop sells (whole vegetables by count, herbs by bunch, tins by size).
2. Subtract what step 1 said is already in the fridge, freezer or cupboard, and mark likely staples "check pantry".
3. Add breakfasts, lunches, snacks and household basics only if the household plans them or asks.
4. Group by aisle (produce; meat and fish; dairy and eggs; bakery; tins, jars and dry goods; spices and condiments; frozen; other), or in the order of their usual shop or delivery app if they said which.
5. If a budget is given, estimate the total and suggest cuts or swaps until it fits.

Write it as Markdown with sections Grocery list (by aisle, each item with amount and the meals it is for), Check pantry, Estimated total. Make it copyable into a notes app.

Stop for approval or edits.

**Gate:** stop here and wait for the user's approval before step 4 (prep).

### Step 4: Plan the prep

Make the busy nights easier with a little work done ahead.

1. Pick only prep that saves real time on the busy days: washing and chopping hardy vegetables, cooking a batch of grains or beans, making a sauce or marinade, portioning meat for the freezer, assembling a traybake for the fridge.
2. Size it to the time the household has, usually a 45–90 minute session on a free day plus 10-minute jobs the night before busy days.
3. Order the session so the oven and hob work while chopping happens, and end with washing up.
4. Say how to store each prepared item and how long it keeps; put anything for later than 3–4 days in the freezer, and note when to move frozen items to the fridge to thaw.

Write it as Markdown with sections Prep session (table: Order | Task | Minutes | Store as | Used on), Night-before jobs, Thaw reminders.

Stop for approval or edits. After approval, tell the person to come back at the end of the week for the review.

**Gate:** stop here and wait for the user's approval before step 5 (review).

### Step 5: Review the week

Learn from this week so next week's plan is easier.

1. Ask, in one short batch: which meals were cooked, skipped or swapped and why; what was thrown away; what everyone liked or did not; how the prep and the budget went.
2. List the leftovers and fridge items that should go into next week's plan, with how long each still keeps, and anything to move to the freezer today.
3. Name what worked and keep it, then pick one or two changes for next week, aimed at the causes (for example "Wednesday is always busier than planned: make it a leftover night", "bagged salad keeps going off: buy whole lettuce or plan it for Monday").
4. Add meals the household loved to a running list of reliable meals for future weeks.

Write it as Markdown with sections What happened, Carry over to next week, Keep doing, Change next week, Reliable meals list.

This is the last step for the week. Offer to start step 1 for next week, carrying these lessons over.
