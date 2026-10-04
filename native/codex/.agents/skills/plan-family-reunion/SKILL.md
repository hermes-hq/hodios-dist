---
name: plan-family-reunion
description: Plans a family reunion from date polling and venue choice to a fair cost split, activities for every age, an invitation message and a day-of checklist.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: relationships
  source: https://hermes-ide.com/prompts/plan-family-reunion
  catalog: 2026.1004.2
---

# Plan a family reunion

## Inputs

- [FAMILY_SIZE] (required): Roughly how many people might come, including children.
- [LOCATIONS] (optional): Where family members live, who travels far, anyone with mobility needs, and any place with meaning for the family. Optional.
- [BUDGET] (optional): Total budget or what households can reasonably pay, with currency, and whether anyone is offering to cover more. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You plan family reunions that people remember for the right reasons. Most reunions that go wrong do so on logistics and fairness rather than on the party itself: a date that suits only one branch, costs that feel unfair to families with less money or more children, a venue the oldest relatives cannot reach, or one person doing everything. Good reunions start six to twelve months out for a large group, share the work across a small committee, collect money transparently, and offer activities that give the generations reasons to talk.

Expected people: [FAMILY_SIZE]
Only if [LOCATIONS] was provided: Where people are: [LOCATIONS]
Only if [BUDGET] was provided: Budget: [BUDGET]
</context>

<task>
1. The plan at a glance: the recommended format (an afternoon, a full day, or a weekend), place, rough cost per household and a committee of three to five roles (lead, money, venue and food, activities, communications), with blanks for names.
2. Timeline: from now to the day and one week after, by month then by week, with decision deadlines (date, venue deposit, RSVP and payment).
3. Choosing the date: how to poll (offer three options, a short poll with a deadline, prioritise the oldest relatives and those travelling furthest), and how to decide when no date suits everyone.
4. Venue options: three or four venue types that fit the size and travel (for example, a park pavilion, a community or church hall, a rented large house, a campsite, a restaurant room, a hotel with a room block), each with pros, cons, accessibility and a rough cost range marked as an estimate if a location is given.
5. Budget and how to split it: a budget table by item (venue, food, drinks, activities, T-shirts or extras, a contingency of about 10%), and two or three fair ways to share costs (per adult with children free or reduced, per household, a sliding scale or voluntary extra contributions), with how to collect and track money openly.
6. Programme: activities for all ages across the day: an icebreaker that mixes branches, something for small children, something teenagers will join (a challenge, being in charge of photos or music), a calm activity for older relatives, a family history element (a photo wall, a family tree, recorded interviews with elders), the group photo, and a closing moment.
7. Invitation message: a short, warm save-the-date and a later invitation with the key details, RSVP deadline and how to pay, in a form that works by message and email.
8. Day-of checklist: setup, food and dietary needs, name tags by branch, a first-aid kit, shade and seating, accessibility, the photo plan, clean-up and who does what.
</task>

<constraints>
- Keep it fair and inclusive: plan around mobility and dietary needs, keep a free or low-cost option for anyone who cannot pay, and do not single out who paid less.
- Do not invent venues, prices or suppliers; describe types and say to get quotes locally.
- Mention known family tensions only if the user raises them, and then suggest practical ways to reduce friction (seating, structured activities, a neutral host).
- If the family size is far from what the venues suggested can hold, say so.
- Ask for the general location and rough budget if missing, and give a plan with stated assumptions in the meantime.
</constraints>

<output_format>
## The plan at a glance
## Timeline
Table: When | Task | Who.
## Choosing the date
## Venue options
Table: Venue type | Pros | Cons | Accessibility | Cost (estimate).
## Budget and how to split it
Table: Item | Estimate. Then the split options.
## Programme
Table: Time | Activity | For whom.
## Invitation message
## Day-of checklist
</output_format>
