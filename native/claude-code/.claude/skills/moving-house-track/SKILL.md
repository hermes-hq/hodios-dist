---
name: moving-house-track
description: Takes a household through a move step by step, from timeline and decluttering to movers, address changes, a packing plan and the first week, pausing for approval between steps.
license: CC0-1.0
arguments:
  - move_details
  - household
argument-hint: <move_details> [household]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: family-logistics
  source: https://hermes-ide.com/prompts/moving-house-track
  catalog: 2026.1002.2
---

# Moving house track

## Inputs

- `move_details` (required): Where from and to (town, country, or "same city"), the move date or window, renting or buying on each side, property sizes and anything fixed such as a key handover time.
- `household` (optional): Who is moving and what they need, for example "two adults, kids aged 3 and 9, a cat, one car, both work from home, budget is tight". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs a household move the way a relocation coordinator would: fix the dates and critical path, shrink what has to move, choose how it moves, redirect the admin, pack in order, and land well. Each step produces one Markdown artifact and stops for approval; later steps build on what was approved.

<move_details>
$move_details
</move_details>
Only if household was provided: 
<household>
$household
</household>

Rules for every step:
- Work backwards from the move date; with no date yet, plan in "weeks before move day" and say so.
- Ask for missing facts that change the plan (date, distance, renting or buying, volume, budget, school dates, pets) in one short batch, and state any assumption.
- Notice periods, costs and who must be told differ by country and change; name your assumption and say to check locally. Never invent prices, company names or legal deadlines.
- Keep the people in view: children need warning and a role, pets need a move-day plan, adults need rest.
- Carry a running list of open questions from step to step.

## Steps

Work through these steps in order. Do not skip a gate.

1. timeline (plan)
2. declutter (plan)
3. movers (plan)
4. admin (build)
5. packing (build)
6. first-week (operate)

### Step 1: Timeline and critical path

1. Confirm the fixed points: move date or window, key handovers, notice periods, school dates and work commitments.
2. Name the critical path: bookings that fill up or take time (movers or van, notice to the landlord, internet installation, school places, move-day parking or lift bookings, time off work).
3. Lay out a week-by-week plan from today to two weeks after the move, with a realistic load per week and the busiest weeks marked.
4. Outline move day hour by hour: who is where, childcare and pets, movers' arrival, meter readings, keys and the "open first" box.
5. Name the risks (a chain falling through, delayed keys, illness) with a fallback for each.

Write sections Fixed dates, Critical path, Week-by-week plan (table: Week | Tasks | Owner), Move day, Risks and fallbacks, Open questions.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 2 (declutter).

### Step 2: Declutter plan

Shrink what has to move; every box not packed saves time and money.

1. Set a target per room and storage area, starting with high-volume, low-emotion areas (kitchen duplicates, books, clothes, toys, garage, paperwork).
2. Give sorting rules (keep, sell, donate, recycle, bin) and a test for borderline items: used in the last year, fits the new home, worth moving.
3. Measure the new home's doorways and rooms and decide now on large furniture.
4. Plan disposal with lead times: selling takes weeks, collections need booking, and paint, batteries and electronics need special disposal (check local services).
5. Let children choose what to keep from their own things within a simple limit, with no surprise disposals.

Write sections Targets (table: Area | Target | Done by), Sorting rules, Large items, Disposal, Kids' part.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 3 (movers).

### Step 3: Movers and quotes

1. Compare the options that fit: do-it-yourself van, a small "man with a van" service, a full removal company, pack-and-move, or freight for long-distance moves, with trade-offs in cost, effort, damage risk and time.
2. Estimate the volume from the rooms, large items and decluttering plan.
3. Write a quote request to send to at least three movers: dates and flexibility, both addresses with access details (stairs, lifts, parking), volume, special items, packing and storage needs, insurance.
4. Give a checklist for comparing quotes: what is included, fixed or hourly price, insurance cover, deposit and cancellation terms, reviews, and red flags such as large cash deposits or no written quote.
5. For do-it-yourself, plan helpers, van size, equipment and safe lifting.

Write sections Options (table), Volume, Quote request, Quote checklist, Decision. Never name companies or state prices as facts.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 4 (admin).

### Step 4: Address changes and admin

1. Build the change-of-address list by group: home (landlord, utilities, internet, insurance, local taxes), money (banks, cards, pensions, tax office), government (electoral register, driving licence, vehicle, benefits, ID), health (doctor, dentist, vet), work and school, and everyday (subscriptions, deliveries, memberships, family and friends).
2. Mark each as before, on or after move day, with the longest lead times first.
3. Recommend mail forwarding for the first months.
4. Write two short templates with [placeholders]: a change-of-address notice and a message to end or transfer a utility.
5. List the moving-out tasks: final readings with photos, cleaning to the required standard, photos of empty rooms, returning keys, and getting the deposit back.

Write sections Checklist (table: Who | When | How | Done), Templates, Moving out. Mark country-specific items with your assumption.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 5 (packing).

### Step 5: Packing plan

1. Estimate supplies: boxes by size per room, tape, paper, markers and bags. If movers pack, list what the household still packs (valuables, documents, medicines).
2. Order packing from least to most used, with a daily box target, so life stays normal until the last days.
3. Set a labelling system: destination room, contents, priority (open first, this week, later), fragile, and a numbered box list.
4. Pack an essentials box and an overnight bag per person: documents, medicines, chargers, toiletries, clothes, bedding, kettle, snacks, comfort items, pet food, basic tools, toilet paper.
5. Cover special cases: valuables and medicines travel with the family; plates, glasses, screens and plants; items movers will not carry; bag and tape furniture screws.
6. Children pack one box of their own to open first; pets stay in a closed room or with a friend on move day.

Write sections Supplies, Packing order (table: Week or day | Items | Boxes), Labels, Essentials, Special items, Kids and pets.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 6 (first-week).

### Step 6: The first week

1. Day one: check the movers' inventory against the box list before signing, take meter readings, check heating, water and electrics, find the stopcock and fuse box, and make the beds first.
2. Days two to seven: unpack kitchen and bathroom, then children's rooms, then the rest, a few hours a day, with the remaining admin slotted in.
3. Safety: change or check locks, test smoke and carbon monoxide alarms, child-proof stairs, windows and cupboards, and secure the garden for pets.
4. Settling in: keep meal and bedtime routines, walk the school route before the first day, explore the area together, and meet the neighbours.
5. Close the move: claim the deposit, report any damage within the movers' deadline, and cancel anything still running at the old address.

Write sections Day one, Days two to seven (table: Day | Tasks), Safety, Settling in, Closing the move, then anything still open.
