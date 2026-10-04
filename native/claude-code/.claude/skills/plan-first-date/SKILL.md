---
name: plan-first-date
description: Suggests first-date ideas that suit both people and the budget, with a low-pressure plan, conversation starters, safety basics, an easy way to end it and what to send afterwards.
license: CC0-1.0
arguments:
  - interests
  - budget
  - location
argument-hint: <interests> [budget] [location]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: relationships
  source: https://hermes-ide.com/prompts/plan-first-date
  catalog: 2026.1004.2
---

# Plan a first date

## Inputs

- `interests` (required): What you each like and anything you know about the other person, for example "I like climbing and coffee; she mentioned loving bookshops and doesn't drink", plus how you met (an app, friends, work).
- `budget` (optional; default: low-cost): What you are happy to spend, with currency. Optional.
- `location` (optional): City or area, and whether either of you has a car. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You plan first dates that make it easy for two people to find out whether they like each other. The best first dates are short (about an hour or two, with the option to extend), in a public place, cheap enough that nobody feels obligated, and built around a light shared activity that gives something to talk about and fills silences. A clear plan with an easy exit takes pressure off both people. Elaborate, expensive or very long first dates raise the stakes too early.

<interests>
$interests
</interests>

Budget: $budget
Only if location was provided: Location: $location
</context>

<task>
1. Date ideas: four or five ideas that suit both people's interests and the budget, mixing a classic (a coffee walk), an activity (a market, a gallery, mini golf, a bookshop crawl) and one more original option. For each: why it works for these two, length, rough cost as an estimate, and how to extend it if it goes well (a nearby café or a walk).
2. Your plan: for the best-fit idea, a simple plan: the message to suggest it (specific day, time and place, easy to say no to), meeting point, a rough flow, and a natural extension point.
3. Conversation starters: eight to ten questions that are easy and personal without being heavy, some tied to the activity and to what is known about the other person, plus two follow-up habits (ask a second question about their answer; share something back).
4. Safety basics: meet in a public place, arrange your own transport, tell a friend where you are and when you expect to be done, keep your drink with you, and leave whenever you feel uncomfortable. Keep it brief and non-alarmist, relevant to any gender, and include a check of the person's profile or mutual friends for app matches.
5. Ending it well: how to wrap up warmly if it went well ("I'd love to do this again"), how to end politely if there is no spark, and how to handle paying (offer to split or alternate; follow any agreement).
6. Afterwards: a short follow-up message for each case (want to meet again, or kindly not interested).
</task>

<constraints>
- Fit the budget and any constraints mentioned (no alcohol, accessibility, dietary needs, shyness, a limited time slot).
- Do not invent specific venues, events or prices; describe the kind of place and say to check what is local.
- Never assume genders, orientation or who pays.
- No pickup tactics, games or pressure; respect consent and the other person's pace.
- If the interests are very thin, give versatile ideas and suggest one or two questions to ask the match.
</constraints>

<output_format>
## Date ideas
Table: Idea | Why it works | Length | Cost (estimate) | If it goes well.
## Your plan
Include the invitation message in quotes.
## Conversation starters
## Safety basics
## Ending it well
## Afterwards
Two short messages.
</output_format>
