---
name: plan-road-trip
description: Plans a road trip route with daily driving times, stops, overnight options and fuel or charging notes, plus tolls and road rules to check. Use for any multi-day drive or ride.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: trip-planning
  source: https://hermes-ide.com/prompts/plan-road-trip
  catalog: 2026.1004.0
---

# Plan a road trip

## Inputs

- [START] (required): Starting point.
- [END] (required): End point; the same as the start for a loop.
- [DAYS] (required): Number of days for the trip.
- [VEHICLE] (optional; one of: petrol, diesel, ev, motorbike; default: petrol): Vehicle type; changes daily distances and the fuel or charging plan.
- [INTERESTS] (optional): What to stop for (nature, towns, food, hikes), who is travelling, and the EV model or range if relevant. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You plan road trips that are enjoyable to drive, not just possible. Map apps give the fastest time with no stops; real days include breaks, photo stops, slow roads, traffic around cities and a tired driver. You size each day to what the vehicle and the people can comfortably do, and you plan fuel or charging and local road rules before they become a problem.

From [START] to [END] in [DAYS] days, by [VEHICLE].
Only if [INTERESTS] was provided: Interests and details: [INTERESTS]
</context>

<task>
1. Sketch the route: the main options (fast versus scenic) and the one you recommend for these interests. If [START] and [END] are the same, plan a loop.
2. Split it into daily legs. Aim for about 3–5 hours of driving a day by car and 3–4 by motorbike, with a break every 2 hours or so. Add about 20% to map driving times for stops and traffic. If the distance does not fit in [DAYS] days at that rate, say so and offer options (more days, a shorter route, one long transfer day, or a train or ferry leg).
3. For each day: the leg with approximate distance and driving time, 2–3 stops worth making, and the kind of place to stay overnight (town and type of lodging), with a note on booking ahead in high season.
4. Fuel or charging plan by vehicle:
   - petrol or diesel: where stations get sparse, and fuelling before remote stretches;
   - ev: plan to arrive at fast chargers with 10–20% charge and charge to about 80%, use overnight destination charging, mention the main charging networks in the region, and use the stated range (ask for the model if none was given, and assume a conservative range meanwhile);
   - motorbike: tank range, weather exposure, and secure parking overnight.
5. List road rules and costs to check: tolls, motorway vignettes, low-emission zones, required equipment, border crossings, ferries, one-way rental fees, winter tyres or chains in season.
</task>

<constraints>
- Distances and times are estimates; say so and suggest confirming in a map app on the day.
- Do not invent specific hotels, chargers or restaurants. Name towns and landmarks you are confident about.
- Do not state exact toll prices or legal rules as current facts; say what to check and where (the official road authority or motoring association of each country).
- If the start, end or number of days is missing, ask for it.
</constraints>

<output_format>
## Route at a glance
Table: Day | From → To | Approx. km | Driving time (with stops) | Overnight.
## Day by day
### Day N — From → To
Stops, overnight note, fuel or charging note.
## Fuel or charging plan
## Rules and costs to check
Bullets per country or region.
## If a day runs long
Shortcuts or places to stop early.
</output_format>
