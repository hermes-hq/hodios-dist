---
name: trip-planning-track
description: Takes a trip from goals and budget to a chosen destination, an itinerary, a bookings checklist, and documents and packing, pausing for approval between steps. Use to plan a whole trip end to end.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: trip-planning
  source: https://hermes-ide.com/prompts/trip-planning-track
  catalog: 2026.1004.2
---

# Trip planning track

## Inputs

- [TRAVELLERS] (required): Who is going (ages, mobility, any children), where you are travelling from, and what a great trip means to you.
- [DATES_OR_LENGTH] (required): Fixed dates or a travel window and the trip length (for example "10 to 14 days, any time in spring").
- [BUDGET] (optional): Total budget with currency and what it must cover (flights, accommodation, food, activities). Optional.
- [INTERESTS] (optional): What you love doing, must-sees, places already visited, deal-breakers, pace, and any destination already in mind. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Plans a trip for [TRAVELLERS] ([DATES_OR_LENGTH]) one approved step at a time: a trip brief, then the destination, then a day-by-day itinerary, then a bookings plan and budget, then documents, packing and a pre-departure timeline. Each step produces one artifact and stops for the traveller's approval or edits; later steps build on the approved versions and do not reopen settled choices without asking. Prices, schedules, opening times and entry rules are never stated as fact: they are typical estimates or items to verify, with where to check. If the traveller asks to skip the approvals, confirm once that later steps will build on unreviewed choices; if they agree, run the remaining steps in one reply and state the choice made at each skipped gate.

- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.

## Steps

Work through these steps in order. Do not skip a gate.

1. brief (discover)
2. destination (plan)
3. itinerary (plan)
4. bookings (build)
5. prepare (verify)

### Step 1: Trip brief

Agree what this trip is for, before choosing anything.

Travellers: [TRAVELLERS]
Dates or length: [DATES_OR_LENGTH]
Only if [BUDGET] was provided: Budget: [BUDGET]
Only if [INTERESTS] was provided: Interests: [INTERESTS]

1. Ask, in one message, only for what is missing and matters: the departure city, exact or flexible dates, the total budget and what it covers, the purpose of the trip (rest, adventure, culture, celebration), pace, accommodation style, accessibility, dietary or health needs, passports held, and deal-breakers.
2. When you have the answers, write the brief:
   - **Purpose:** one sentence on what a great trip means for these travellers.
   - **Must-haves** and **deal-breakers:** short lists.
   - **Constraints:** dates, maximum travel time, budget split (a rough share for transport, accommodation, food and activities, marked as a starting assumption), and pace (for example "one main thing a day").
   - **Open questions** that later steps will need answered.

Stop and wait for the traveller to approve or edit the brief. Do not suggest destinations yet.

**Gate:** stop here and wait for the user's approval before step 2 (destination).

### Step 2: Destination

Choose where to go for the trip ([DATES_OR_LENGTH]) from the approved brief.

1. If the traveller already named a destination, confirm it fits the brief and check the season for their dates (weather, rainy or storm seasons, holidays and festivals that raise prices or close things), then skip to step 4 below.
2. Otherwise shortlist 3 to 5 varied destinations that fit the brief. For each give: why it fits, typical weather and crowds for the dates, rough travel time from the departure city, relative cost on the ground (budget, moderate, expensive), and the main drawback, all marked as typical patterns, not current facts.
3. Lay out the key trade-offs between the top two in plain language and recommend one.
4. For the chosen or recommended destination, note what to check before committing: the traveller's government travel advice, entry requirements for their passport (to verify, never stated as fact), and anything in the season that could change the plan.

Stop and wait for the traveller to choose or approve the destination. Do not build an itinerary yet.

**Gate:** stop here and wait for the user's approval before step 3 (itinerary).

### Step 3: Itinerary

Build the day-by-day plan for the approved destination and dates ([DATES_OR_LENGTH]).

1. Decide the bases and nights in each. Avoid one-night stops (unless the traveller wants a moving trip) and backtracking.
2. Plan each day:
   - arrival and departure days kept light;
   - activities grouped by area so the traveller is not crossing the city twice;
   - the pace from the brief (for example one main thing a day plus something optional);
   - realistic travel times between places, marked as estimates;
   - a rest or flexible day about every 3 to 4 days on longer trips;
   - a bad-weather alternative for outdoor days.
3. Mark what must be booked ahead (timed tickets, popular restaurants, tours, trains) and what can be decided on the day.
4. Check the plan against the brief's must-haves and deal-breakers, and list any must-have that did not fit with the reason.

Output a table: Day | Base | Morning | Afternoon | Evening | Book ahead? | Bad-weather option.

Stop and wait for approval or edits. Do not make the bookings plan yet.

**Gate:** stop here and wait for the user's approval before step 4 (bookings).

### Step 4: Bookings and budget

Turn the approved itinerary into a bookings plan and a budget check.

1. List every booking the trip needs (flights or long-distance transport, accommodation per base, local transport passes, timed tickets, tours, restaurants, car hire, travel insurance), in order of urgency: what sells out or rises in price first.
2. For each booking note what to compare (for example flexible versus non-refundable rates, location of accommodation versus price, baggage in the flight price) and the cancellation terms to check before paying.
3. Estimate the budget by category with a low and a high figure, clearly labelled as rough estimates to verify, and compare it with the budgetOnly if [BUDGET] was provided:  ([BUDGET]). If it is over, show where to save without breaking a must-have.
4. Suggest booking timing as rules of thumb (for example flights and peak-season accommodation first; keep some evenings unbooked).

Output a checklist: Booking | Book by | What to compare | Cancellation terms to check | Est. cost (low to high). Then the budget table.

Stop and wait for approval or edits. Do not prepare documents and packing yet.

**Gate:** stop here and wait for the user's approval before step 5 (prepare).

### Step 5: Documents, packing and departure

Get the travellers ready to leave.

1. **Documents to verify:** passport validity beyond the return date and blank pages, visas or electronic travel authorisations for each country entered or transited, documents for children travelling with one parent, driving permits if hiring a car, travel insurance, and health entry requirements. Mark each as "to verify" with where to check (the destination government's official site, the traveller's own government travel advice, the airline). Do not state any rule as fact. For complex cases (previous refusals, long stays, work or study), say to consult the consulate or an immigration professional.
2. **Health and money:** a travel health clinic or doctor 4 to 8 weeks ahead for vaccines and medicines, prescriptions in original packaging, a backup card and some local currency.
3. **Packing:** a packing list sized to the itinerary's climate, activities and luggage limits, grouped by category, with what is easy to buy there instead.
4. **Pre-departure timeline:** what to do 8 weeks, 4 weeks, 1 week and the day before (check-in, offline maps and tickets, sharing the itinerary with someone at home, a last check of travel advice).
5. **One-page trip summary:** bases with dates, key bookings, and emergency contacts to fill in (the local emergency number, the nearest embassy or consulate of their country, the insurer's helpline).
