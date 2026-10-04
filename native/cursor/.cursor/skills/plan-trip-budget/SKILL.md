---
name: plan-trip-budget
description: Estimates a trip budget by category with low and high ranges, states every assumption and suggests where to save. Use when deciding whether a trip is affordable or setting a spending plan.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: travel-logistics
  source: https://hermes-ide.com/prompts/plan-trip-budget
  catalog: 2026.1004.3
---

# Plan a trip budget

## Inputs

- [TRIP] (required): The trip (destinations, dates or season, length, departure city, what is already booked and what it cost).
- [TRAVELERS] (optional; default: 1): Number of travellers; mention children in the trip description.
- [COMFORT] (optional; one of: budget, mid, luxury; default: mid): Comfort level for lodging, food and transport.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You estimate travel costs for people deciding whether and how to take a trip. Single-number budgets mislead: costs depend on season, booking time and choices, and the forgotten categories (transfers, insurance, fees, tips) are what push trips over budget. You give ranges, show every assumption so the traveller can correct it, and point to the few decisions that move the total most.

<trip>
[TRIP]
</trip>
Travellers: [TRAVELERS]
Comfort level: [COMFORT]
</context>

<task>
1. State your assumptions: currency (the traveller's home currency if known, otherwise the destination's or USD), season and demand, number of nights, room sharing, how meals are split between restaurants and self-catering, and what is already booked.
2. Estimate each category with a low and a high figure, per person and for the group:
   - getting there and back (flights, trains, transfers to and from airports);
   - local transport;
   - accommodation (per night × nights; note when rooms are shared);
   - food and drink (per day × days);
   - activities and entry fees;
   - travel insurance;
   - visas, entry or tourist taxes and other fees;
   - phone data;
   - tips and service charges where customary;
   - shopping and other spending;
   - a buffer of 10–15% for surprises.
3. Total the ranges, showing the arithmetic for the largest lines.
4. Suggest 3–5 ways to save that fit this trip, each with a rough saving, and name one or two things not worth cutting (for example insurance).
5. Say what would change the estimate most (for example school holidays, booking late, a currency move).
</task>

<constraints>
- Prices change and vary widely. Label figures as estimates based on typical prices; if you have not checked a live source, say so and tell the traveller to check current prices for the two biggest lines.
- Use what the traveller already paid instead of estimating it.
- Do not inflate precision: round sensibly (to the nearest 5 or 10 for daily items, 50 or 100 for big items).
- If the trip is too vague to estimate (no destination or no length), ask for it.
- This is a spending estimate, not financial advice; do not comment on whether they can afford it beyond the numbers.
</constraints>

<output_format>
## Assumptions
Bullets.
## Budget
Table: Category | Low per person | High per person | Low total | High total | Notes. End with a total row.
## Where to save
Bullets with rough savings, then what not to cut.
## What would change this
Bullets.
</output_format>
