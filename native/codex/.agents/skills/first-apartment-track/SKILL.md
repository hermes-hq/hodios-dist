---
name: first-apartment-track
description: Walks a first-time renter through gated steps from budget and search to viewings, application, lease read-through, move-in inventory, utilities and furnishing on a budget.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: workflow
  category: home-improvement
  source: https://hermes-ide.com/prompts/first-apartment-track
  catalog: 2026.1004.2
---

# First apartment track

## Inputs

- [CITY] (required): The city or area you want to live in, and the country.
- [BUDGET_PER_MONTH] (required): What you can spend on housing each month, with currency, and your monthly take-home income if you are comfortable sharing it.
- [MOVE_BY] (required): The date you need to move by, and any fixed reason (a job start, a lease ending, term starting).
- [ROOMMATES] (optional; default: 0): How many people you will share with, not counting yourself; 0 means living alone.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

Takes a first-time renter from "I need a place" to a furnished home, one approved step at a time. Each step produces one artifact and stops for approval; later steps build on approved choices and do not reopen them without asking.

City: [CITY]. Budget per month: [BUDGET_PER_MONTH]. Move by: [MOVE_BY]. Roommates: [ROOMMATES].

Rental rules (deposit caps, permitted fees, notice periods, landlord duties) vary by place and change: present them as things to confirm with an official tenant-rights source, never as fact. The lease step is a read-through and question list, not a legal opinion; anything unusual goes to a tenant advice service or lawyer. At every step, watch for rental scams: no money before a viewing (in person or live video) and proof the person can let the property. If the renter asks to skip approvals, confirm once, then run the remaining steps and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. budget (plan)
2. search (discover)
3. viewings (verify)
4. application (build)
5. lease (verify)
6. move-in (build)
7. furnish (build)

### Step 1: Budget

Work out what the renter can really afford.

1. If income, or whether the budget includes bills, is unclear, ask in one message and stop.
2. Monthly table (Item | Estimate | Notes): rent, utilities share, internet, local charges tenants pay, contents insurance, transport, food. Mark figures as estimates.
3. Upfront table: deposit, rent in advance, holding deposit or permitted fees, moving, week-one basics. Deposit caps and fees vary; confirm locally.
4. Affordability: rent against take-home pay (rule of thumb: about a third or less), and whether landlords here ask for an income multiple or guarantor. If it does not fit, say so plainly and offer options (roommates, a cheaper area, a smaller place, a later move) to choose from.
5. With roommates: splitting rent and bills fairly, and joint versus individual tenancies.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 2 (search).

### Step 2: Search plan

1. Rank five or six priorities (commute, quiet, light, laundry, pets, outdoor space, furnished); ask if unknown.
2. Two to four areas of [CITY] by trade-off (cheaper but longer commute, livelier but noisier), commutes to check on a map.
3. Where to search here by type (listing sites, agents, student or employer boards, local groups), without endorsing companies, and a timeline back from [MOVE_BY].
4. A message template for landlords that answers their usual questions upfront.
5. Scam signs: price far below the area, landlord abroad, deposit to "hold" before a viewing, wire transfers, gift cards or crypto, copied listing photos.

Stop for approval of areas and priorities.

**Gate:** stop here and wait for the user's approval before step 3 (viewings).

### Step 3: Viewings

1. A phone-sized checklist: damp and mould, water pressure and hot water, heating, windows and locks, smoke and carbon monoxide alarms, signal, noise, pests, appliances, storage, what is included.
2. Questions: total monthly cost and bills, deposit protection, contract length and break options, repairs, why the last tenants left, rules on guests, pets and decorating.
3. A comparison table: Place | Rent | Bills | Commute | Must-haves | Concerns.
4. Red flags that mean walk away.

If the renter shares viewing notes, fill in the table and say which looks strongest. Stop for their choice.

**Gate:** stop here and wait for the user's approval before step 4 (application).

### Step 4: Application

1. Documents this market usually asks for (confirm with the agent): ID, right-to-rent proof where required, income or job offer, references, credit check, guarantor details.
2. No rental history or thin credit: a guarantor, an employer or university reference, a short cover note; extra deposit or rent in advance only where legal and with care.
3. A short, honest cover note to the landlord.
4. Share documents only through official channels once the property is confirmed real, black out unneeded numbers, and get a written receipt with terms for any holding deposit.

Stop for approval before anything is sent.

**Gate:** stop here and wait for the user's approval before step 5 (lease).

### Step 5: Lease read-through

A checklist and questions, not a legal opinion.

1. If the renter pastes the lease, summarise in plain words: dates, rent, deposit and protection, bills, break clause and notice, renewal and increases, repairs, rules, fees.
2. Flag clauses to ask about: tenant pays all repairs or normal wear, automatic renewals, fees above local limits, entry without notice, joint liability, anything that contradicts the viewing.
3. Turn each flag into a polite question for the landlord and say what to get in writing.
4. Say which points to check with a tenant advice service or lawyer; local law may override a clause.

Stop; the renter decides whether to sign.

**Gate:** stop here and wait for the user's approval before step 6 (move-in).

### Step 6: Move-in and utilities

1. Move-in record before unpacking: timestamped photos and video of every room, inside cupboards and appliances, meter readings; send inventory corrections in writing within the allowed window.
2. Safety: test smoke and carbon monoxide alarms; find the water stop valve, fuse box and gas shut-off; ask for any safety certificates required locally.
3. Admin checklist: energy and water accounts, internet (book early), local registrations or charges, contents insurance, change of address, bill split with roommates.
4. Who to call for repairs, reporting in writing, and keeping copies.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 7 (furnish).

### Step 7: Furnish on a budget

1. First-night list (bedding, towels, toilet paper, a pan, plate and cup, a light, cleaning basics) separate from what can wait.
2. Priority order within the money left: bed and mattress, seating, table, storage, kitchen kit.
3. Secondhand sources and checks: bed bugs on mattresses and upholstery, stability, tested electrical items.
4. Deposit-safe touches: removable hooks, rugs, lamps; ask before painting or drilling; anchor tall furniture if allowed.
5. Save the deposit protection details, inventory, contacts and notice date somewhere safe.
