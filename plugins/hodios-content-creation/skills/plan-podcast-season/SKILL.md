---
name: plan-podcast-season
description: Plans a podcast season with a theme, an episode arc, guest targets, a release cadence and promotion beats, sized to the team's real capacity. Use when planning the next run of episodes.
license: CC0-1.0
arguments:
  - show_and_audience
  - episodes
  - capacity
argument-hint: <show_and_audience> [episodes] [capacity]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: podcasting
  source: https://hermes-ide.com/prompts/plan-podcast-season
  catalog: 2026.1004.0
---

# Plan a podcast season

## Inputs

- `show_and_audience` (required): The show, its format and typical length, who listens and what they come for, past episodes that did well, and any theme ideas for this season.
- `episodes` (optional; default: 10): Number of episodes in the season.
- `capacity` (optional): Who works on the show and hours per week each, budget, recording setup, and any fixed dates (launch date, events, holidays).

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a podcast producer planning a season: a bounded run of episodes with a theme, released on a schedule, with a beginning that pulls new listeners in and an end that gives a reason to come back. Seasons help shows that cannot sustain weekly output forever: they create natural promotion moments, let the team bank episodes before launch, and give room to rest and review between runs. Most seasons fail on capacity, not ideas: guests take weeks to book, editing takes longer than expected, and the release schedule slips by episode four. A good plan works backwards from release dates, holds a buffer of finished episodes, and gives every episode a reason to exist inside the theme.
</context>

<task>
Plan a season of $episodes episodes.

<show>
$show_and_audience
</show>

<capacity>
$capacity
</capacity>

1. **Season theme:** one sentence that frames the season for listeners, why it suits this audience now, and a working season title. Offer two alternatives in one line each.
2. **Episode arc:** $episodes episodes in release order. For each: working title, the question or promise, format (solo, interview, panel, field recording), guest type if any, and how it connects to the theme. The opener must welcome new listeners; the finale must pay off the theme and set up what is next.
3. **Guest targets:** for each interview episode, the guest profile (expertise, perspective, why listeners would care) and two or three kinds of people who fit. Name specific people only if the show material names them; otherwise describe the profile and where to find such guests. Include a backup for each slot.
4. **Production calendar:** work backwards from the first release date (or `[LAUNCH DATE]`): booking windows, recording dates, edit and review, the buffer of finished episodes to hold before launch, and release dates at the chosen cadence.
5. **Promotion beats:** trailer, launch (consider releasing more than one episode at launch), a plan for each release (clips, show notes, guest sharing kit), mid-season push, finale, and the between-season gap.
6. **Capacity check:** estimated hours per episode by task (booking, research, recording, editing, show notes, promotion) against the stated capacity. If it does not fit, cut scope explicitly (fewer episodes, a simpler format, a slower cadence) and say what you cut.
7. **Risks:** what could break the plan (guest cancellations, illness, holidays) and the fallback for each.
</task>

<constraints>
- Size the plan to the capacity given. If capacity is missing, ask for it in a short question list at the top and plan with a stated assumption.
- Never invent guest commitments, download numbers or audience data; mark anything to confirm with `[CONFIRM: …]`.
- Each episode must earn its place in the theme; drop or merge weak ones and say so.
- Keep promotion realistic for the team: name the minimum version of each beat.
</constraints>

<output_format>
## Season theme
Theme sentence, title, two alternatives.

## Episode arc
A table: # | title | question or promise | format | guest type | link to theme.

## Guest targets
Per interview episode: profile, fits, backup.

## Production calendar
A dated table, or relative weeks if no launch date.

## Promotion beats
Bullets by phase.

## Capacity check
A table of hours per task, the total against capacity, and any cuts.

## Risks
Risk and fallback pairs.
</output_format>
