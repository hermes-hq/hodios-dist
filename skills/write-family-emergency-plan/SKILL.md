---
name: write-family-emergency-plan
description: Writes a household emergency plan with contacts, meeting points, hazard-specific actions, medical information, a go-bag list and a role for each family member, ready to print.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: family-logistics
  source: https://hermes-ide.com/prompts/write-family-emergency-plan
  catalog: 2026.1004.2
---

# Write a family emergency plan

## Inputs

- [HOUSEHOLD] (required): Who lives there and what they need, for example ages, medical conditions and essential medicines, mobility or communication needs, pets, whether anyone is often away, the type of home (flat, house, floor), cars, and where children are during the day.
- [LOCAL_HAZARDS] (optional): Risks where you live, for example "wildfires and power cuts", "floods", "earthquakes", "winter storms", or your area so the plan can suggest likely ones. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write household emergency plans of the kind civil protection agencies recommend, tailored to a real family. A plan that works fits on a few printed pages, is known by everyone in the house including children, and answers the questions that cause panic: how do we reach each other when phones fail, where do we meet, who collects the children, what do we grab, and what does each of us do. Children, older relatives, people with medical needs or disabilities, and pets need specific planning. Phone networks often fail or jam in large emergencies, so plans use an out-of-area contact and text messages, and keep key information on paper.

<household>
[HOUSEHOLD]
</household>
Only if [LOCAL_HAZARDS] was provided: Local hazards: [LOCAL_HAZARDS]
</context>

<task>
1. Household at a glance: who is in the household and the specific needs the plan must cover (medicines that cannot run out, equipment that needs power, mobility, babies, pets), and the hazards the plan covers. If no hazards are given, plan for house fire, power cut and severe weather, and ask about local risks.
2. Emergency contacts: a table with blanks to fill in: the local emergency number, an out-of-area contact everyone reports to, neighbours, schools and childcare, workplaces, doctors and pharmacy, utilities, insurance, and the vet. Add the rule to text rather than call when networks are busy.
3. Meeting points and routes: a meeting point just outside the home (for a fire), one outside the neighbourhood (if you cannot get home), and an out-of-town place to stay; two ways out of each room or floor where possible; and the plan for picking up children from school (check the school's own emergency plan and who is authorised to collect).
4. What to do by hazard: for each hazard, the actions for "get out" and "stay in" (shelter in place), including which room, when to turn off utilities if you know how and it is safe, and where official alerts come from (local emergency management, weather service, radio).
5. Medical information: a table per person with blanks (conditions, medicines and doses, allergies, devices, doctor, blood type if known), and the advice to keep a paper copy in the go-bag and a week's supply of essential medicines where possible.
6. Go-bag checklist: one per household plus small ones for children, covering water (about 4 litres or 1 gallon per person per day for at least three days is a common guideline), food, medicines and copies of prescriptions, copies of documents, cash, phone chargers and a power bank, torch, battery or wind-up radio, first-aid kit, warm clothes, hygiene items, comfort items for children, and baby and pet supplies as relevant. Mark what to buy and what to grab on the way out.
7. Roles: a role for each person suited to their age (for example, one adult grabs the go-bag and medicines, another the children and pets; a teenager checks on the neighbour; a young child knows their address, a parent's phone number and the meeting point).
8. Practise and update: drills twice a year (fire escape, meeting point, a "no phone" test), dates to check the go-bag and medicines, and when to update the plan.
</task>

<constraints>
- Never invent phone numbers, addresses or local agency names; use blanks such as [out-of-area contact] and say to check the local emergency number and official alert sources.
- Personal data stays in the user's printed copy: use placeholders, not real names or numbers, in your output.
- For anyone dependent on powered medical equipment or with serious needs, add that they should talk to their doctor or equipment supplier and register with the utility or local priority-services list where available.
- Advice must match official guidance in general terms; where it depends on the hazard and place (for example, earthquakes versus floods), say to check the local emergency management guidance.
- If the user describes an emergency happening now, tell them to call their local emergency number and follow official instructions instead of making a plan.
- Calm and practical, readable by older children.
</constraints>

<output_format>
## Household at a glance
## Emergency contacts
Table with blanks: Who | Number | Notes.
## Meeting points and routes
## What to do by hazard
Table: Hazard | Get out when | Stay in when | Key actions.
## Medical information
Table with blanks per person.
## Go-bag checklist
## Roles
Table: Person | Role.
## Practise and update
</output_format>
