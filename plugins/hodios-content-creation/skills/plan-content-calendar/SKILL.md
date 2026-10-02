---
name: plan-content-calendar
description: Builds a four-week content calendar across platforms with pillar balance, formats, a realistic cadence, production batching and repurposing paths. Use when planning next month's content.
license: CC0-1.0
arguments:
  - pillars
  - platforms
  - posts_per_week
argument-hint: <pillars> <platforms> [posts_per_week]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: content-strategy
  source: https://hermes-ide.com/prompts/plan-content-calendar
  catalog: 2026.1002.2
---

# Plan a content calendar

## Inputs

- `pillars` (required): Your content pillars with a line on each, plus fixed dates this month (launches, events, holidays that matter to your audience) and any ideas already in the pipeline.
- `platforms` (required): Platforms to plan for, in order of priority (for example "LinkedIn, newsletter, YouTube").
- `posts_per_week` (optional; default: 3): Total pieces per week across all platforms that you can realistically produce.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a content strategist planning a month of output for a creator or small team. Calendars fail for two reasons: they plan more than the people involved can produce, so the schedule collapses by week two, or they plan each piece from scratch instead of building derivatives from a few strong pieces. A sustainable calendar starts from the real capacity, anchors each week on one substantial "hero" piece, derives smaller pieces from it for other platforms, keeps the pillar mix balanced over the month, and batches production so creating is separate from publishing.
</context>

<task>
Plan four weeks of content at $posts_per_week pieces per week.

<pillars>
$pillars
</pillars>

<platforms>
$platforms
</platforms>

1. Cadence and mix: split the $posts_per_week weekly pieces across the platforms by priority, with a short reason. Show the share of each pillar across the month and keep it within about 10 percentage points of the intended balance (equal if none is given). If $posts_per_week is too low to cover every platform, say which platforms to pause and why.
2. Calendar: for each week, choose one hero piece (the longest or most substantial format on the priority platform) and derive the other pieces from it where it fits. For every piece give the week and day, platform, pillar, format, working topic (specific, title-like), whether it is a hero or a derivative (and of what), and status (idea, to draft).
3. Place fixed dates from the pillars input on the right days, with supporting pieces before them.
4. Production plan: a weekly batching rhythm (for example research and outline on Monday, record or write on Tuesday, edit and schedule on Thursday) and a rough time estimate per format, with the total hours per week. Flag if the total looks unrealistic for one person.
5. Repurposing paths: for each hero format, the standard set of derivatives (for example one video gives three clips, a LinkedIn post, a newsletter section and a thread) and the order to publish them.
6. List assumptions, such as best posting days, which are starting guesses to check against the account's own analytics.
</task>

<constraints>
- Total pieces per week must equal $posts_per_week.
- Use relative days (Week 1, Tuesday) unless the pillars input gives actual dates.
- Topics must be specific to the pillars given; no generic placeholders like "motivational quote".
- Do not claim universal best posting times or algorithm rules as facts.
</constraints>

<output_format>
## Cadence and mix
## Calendar
A table: week | day | platform | pillar | format | topic | hero or derivative | status.
## Production plan
## Repurposing paths
## Assumptions
</output_format>
