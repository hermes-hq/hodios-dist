---
name: community-event-planning-track
description: Plans a volunteer-run community event such as a street party, school fair or fun run in gated steps - permissions, volunteers, publicity, safety, the day itself and a wrap-up with thanks and accounts.
license: CC0-1.0
arguments:
  - event
  - date
  - volunteers
  - budget
argument-hint: <event> <date> <volunteers> <budget>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: task-management
  source: https://hermes-ide.com/prompts/community-event-planning-track
  catalog: 2026.1004.0
---

# Community event planning track

## Inputs

- `event` (required): What the event is, where, who it is for and roughly how many people, for example "street party on our cul-de-sac for about 120 residents, with a bouncy castle and shared food".
- `date` (required): The planned date, or a target month if not fixed yet.
- `volunteers` (required): How many volunteers you can count on today, including yourself.
- `budget` (required): Money available and where it comes from, for example "300 from the residents' fund, plus whatever we raise on the day", or "none yet".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Plans a community event the way an experienced volunteer organiser would, pausing after each step for approval. Permissions come first because they decide what is possible; the wrap-up makes next year easier.

<event>
$event
</event>
Date: $date
Volunteers: $volunteers
Budget: $budget

Throughout: use the person's facts; never invent approvals, names, prices or dates. Where something is missing, ask, or use a marked placeholder such as [lead - to confirm]. Permits, road closures, insurance, food hygiene, alcohol, background checks for volunteers working with children, and raffle rules differ by country and council: list each as something to check with the named body (council, insurer, venue owner, school) and never state them as settled law. If the event is mainly a fundraiser with income targets and sponsors, say so and suggest a fundraising-event plan alongside this one. Keep documents short enough for volunteers to read.

## Steps

Work through these steps in order. Do not skip a gate.

1. shape-and-permissions (plan)
2. volunteers (plan)
3. publicity (plan)
4. safety (plan)
5. event-day (operate)
6. wrap-up (operate)

### Step 1: Shape the event and check permissions

Agree what the event is and find out what needs permission before anyone books anything.

1. Read the event, date, volunteers and budget. If the location, the expected numbers or who the event is for is unclear, ask up to four questions in one message and wait.
2. Write a one-paragraph event brief: purpose, audience, size, place, time window, the core activities, and what success looks like (for example "neighbours meet; no one hurt; costs covered").
3. Permissions checklist, only for what applies: use of the space, road closure, temporary structures (stages, inflatables, marquees), amplified music, food, alcohol, raffles, and public liability insurance (event cover, or whether a group's existing cover extends to it). For each: who to ask, what to ask, and a lead time to confirm.
4. Timeline: working back from $date, the latest dates to apply for each permission, plus a go or no-go date when the plan is confirmed or scaled down.
5. Budget sketch: likely cost lines (insurance, hire, permits, publicity, first aid, food, waste) against $budget, with a contingency line and ideas for covering any gap.
6. Flag anything that looks tight: a date too close for a road-closure application, a budget that cannot cover insurance, or too few volunteers for the size.

Stop and ask the person to approve the brief and confirm who they will contact for each permission before planning volunteers.

**Gate:** stop here and wait for the user's approval before step 2 (volunteers).

### Step 2: Volunteers and roles

Turn goodwill into a team where everyone knows their job.

1. From the approved brief, list the roles needed before, on and after the day: overall lead, paperwork, money, publicity, set-up, activities, food, first aid, stewards, waste, and a safeguarding lead if children are involved.
2. Match the roles to $volunteers volunteers. If there are too few, show which roles can be combined, which activities to cut, and a short recruitment message to find more (neighbours, school parents, local groups).
3. Write a rota for the day in shifts of two to three hours, with a named lead per area and cover for breaks.
4. Draft a one-page volunteer briefing: timings, where to be, who to report to, what to do if someone is hurt, lost or upset, and who handles money.
5. Note any checks to confirm locally, such as background checks for volunteers working with children, and that volunteers should not work alone with children.

Stop and ask the person to approve the roles and rota and fill in names before publicity.

**Gate:** stop here and wait for the user's approval before step 3 (publicity).

### Step 3: Publicity and neighbours

Let the right people know, early enough and clearly.

1. Choose channels that fit the audience: flyers, posters, local social media and messaging groups, school newsletters, local press for larger events.
2. Write the core message once: what, when, where, cost, who it is for, what to bring, accessibility information and a contact. Then adapt it for a flyer, a social post and a newsletter.
3. For street or neighbourhood events, draft a letter to residents affected (parking, road closure, noise times) with a contact for concerns, sent in good time.
4. Set a publicity timeline: save-the-date, main push, reminder in the final week, and a day-before post with practical details.
5. Ask whether photos will be taken and draft a short notice for the event and sign-up about photography and how to opt out, especially for children.

Stop and ask the person to approve the messages and timeline before the safety plan.

**Gate:** stop here and wait for the user's approval before step 4 (safety).

### Step 4: Safety plan

Plan for the things that go wrong at community events so they stay small.

1. Write a simple risk assessment for this event: hazard, who could be harmed, likelihood and severity (low, medium, high), controls, and who is responsible. Consider crowds, traffic, trip hazards, food allergies, inflatables, weather, lost children, first aid, fire and cash handling; keep only what applies.
2. Emergency plan: how to call emergency services and the exact address or location point to give, an access route kept clear for vehicles, a meeting point, and who is in charge if something serious happens.
3. Lost child procedure in four lines, with a named point and a code phrase for volunteers.
4. First aid: who covers it and with what; for larger or higher-risk events, suggest asking a voluntary first-aid organisation early.
5. Accessibility: step-free routes, seating and shade, toilets, a quiet space, and clear signage.
6. Mark items to check with the insurer, council or venue (for example inflatable operator certificates or food hygiene requirements).

Stop and ask the person to approve the safety plan and confirm owners before planning the day.

**Gate:** stop here and wait for the user's approval before step 5 (event-day).

### Step 5: The day itself

Make the day run from a sheet, not from the organiser's memory.

1. Run sheet from set-up to clear-up: time, what happens, who leads, what they need; include a safety walk before opening and volunteer breaks.
2. Contacts sheet: every lead's phone number placeholder, suppliers, the venue or council contact, and emergency numbers.
3. Kit list: tables, gazebos, signs, bins, first-aid kit, cash float, cable covers, water, rain plan items.
4. Money handling: two people counting, a simple takings sheet, and where cash is kept during the day.
5. Plan B for the likely failures: rain, a no-show supplier, fewer volunteers, a power cut.
6. A five-minute volunteer briefing script for the morning.

Stop and ask the person to approve the run sheet before the wrap-up step.

**Gate:** stop here and wait for the user's approval before step 6 (wrap-up).

### Step 6: Wrap-up, thanks and accounts

Close the event properly so people want to do it again.

1. Clear-up checklist: rubbish, hire items and borrowed kit returned, the space left as found, any damage reported.
2. Thank-you messages: to volunteers (specific to what each did), to suppliers and the venue or council, and a public thank-you post with a highlight or two and any total raised.
3. Simple accounts: income and spending against the budget, receipts kept together, and who signs them off. Say where surplus goes or how a shortfall is covered.
4. Lessons in three lists: keep, change, and stop. Ask volunteers for one line each.
5. A handover file for next year: brief, permissions with dates and contacts, rota, run sheet, risk assessment, accounts and lessons.

This is the last step. Close with the three follow-up actions and their owners.
