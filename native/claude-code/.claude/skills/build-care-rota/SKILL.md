---
name: build-care-rota
description: Builds a shared care rota for an ill or ageing relative across family members and helpers, with a task list, weekly schedule, coverage gaps, handover notes and a fair split of the load.
license: CC0-1.0
arguments:
  - care_needs
  - helpers_and_availability
argument-hint: <care_needs> <helpers_and_availability>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: family-logistics
  source: https://hermes-ide.com/prompts/build-care-rota
  catalog: 2026.1004.2
---

# Build a family care rota

## Inputs

- `care_needs` (required): What the person needs and when, for example meals, medicines (as instructed by their care team), personal care, appointments, shopping, company, night checks, pets, bills. Include any tasks that need training and what paid or professional care is already in place.
- `helpers_and_availability` (required): Who can help and when, how far away they live, what they are good at or cannot do, and other commitments, for example "Sam, lives 10 min away, free weekday evenings, can't do lifting; Priya, 3 hours away, can do admin and pay for a cleaner".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help families organise care for a relative the way a care coordinator would: list every task, match tasks to the people best placed to do them, make gaps visible before they become a crisis, and split the load fairly, which is rarely equally. A sibling who lives nearby can do visits; one who lives far away can take admin, phone calls, money or booking paid help. A shared, written rota stops one person quietly doing everything and burning out.

<care_needs>
$care_needs
</care_needs>

<helpers_and_availability>
$helpers_and_availability
</helpers_and_availability>
</context>

<task>
1. Care tasks: list every task with how often, when, roughly how long it takes, whether it needs to be in person, and any skill or training it needs (for example lifting, injections, catheter care). Copy any medical or care instructions exactly as given; do not add or change them.
2. Weekly rota: assign tasks to helpers using only the availability they gave, matching tasks to proximity, skills and limits. Remote helpers get remote tasks (admin, ordering, calls, bookings, money, video company). Add a weekly or fortnightly rhythm for less frequent tasks.
3. Coverage gaps: list every slot or task no one can cover, with options (another relative or friend, neighbours, community or faith groups, paid help, a professional service from the relative's care team) for the family to decide. Flag tasks that need training or a professional and are currently assigned to no one qualified.
4. How the load is split: a table of each helper's hours and type of contribution (time, travel, money, admin, emotional load), and a short, neutral note on fairness: who carries the most, and one suggestion to rebalance. Count the main carer's unseen tasks (planning, being on call, night disturbances).
5. Handover note: a short template for whoever finishes a shift to pass on (how they were, eating and drinking, medicines given as recorded, mood, anything new, tasks done, tasks left, supplies running low), plus where the shared log lives (a notebook in the house, a shared document or group chat).
6. Backup plan: who covers if someone is ill or away, and who to call in an emergency, with a reminder to keep the relative's emergency medical summary and contacts by the door.
7. Message to the family: a short, warm message proposing the rota, with a date to review it in four weeks.
</task>

<constraints>
- Never assign more time than someone said they have, or tasks they said they cannot do. If the needs exceed what the family can cover, say so plainly and put it in the gaps.
- Keep the relative's own wishes and independence in view: include them in the plan and in tasks they can still do.
- Do not give medical or care-technique advice; tasks that need training belong to someone trained or to the relative's care team.
- If the description suggests the relative is unsafe now (left alone when they cannot be, not eating or drinking, a recent fall, sudden confusion), say this needs urgent attention from their doctor or care services before any rota.
- If the main carer sounds overwhelmed, acknowledge it and suggest support for carers in one line.
- Neutral tone about family members; no blame.
</constraints>

<output_format>
## Care tasks
Table: Task | How often and when | Time | In person? | Skills or training needed.
## Weekly rota
Table with days as columns and time slots or tasks as rows, each cell naming the helper.
## Coverage gaps
## How the load is split
Table: Helper | Hours per week | Contribution type. Then the fairness note.
## Handover note
Template in a code block.
## Backup plan
## Message to the family
</output_format>
