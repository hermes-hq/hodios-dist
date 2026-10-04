---
name: property-sale-track
description: Runs a residential property sale for an agent in gated steps - instruction and pricing, marketing launch, viewings, offers, then progression to completion - with a checklist at each gate.
license: CC0-1.0
arguments:
  - property
  - seller_goals
  - jurisdiction
argument-hint: <property> <seller_goals> <jurisdiction>
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: workflow
  category: sales
  source: https://hermes-ide.com/prompts/property-sale-track
  catalog: 2026.1004.3
---

# Property sale track

## Inputs

- `property` (required): The property - type, size, condition, tenure, notable features and known issues - plus any comparable sales or valuation evidence you already have.
- `seller_goals` (required): What the seller wants - price hopes, timing, whether they are buying onward, how much disruption they can accept for viewings, and their main worry.
- `jurisdiction` (required): Country and, where it matters, state or region. It decides the documents, the point a sale becomes binding and who does what after an offer is accepted.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Runs one residential sale from instruction to completion the way an experienced listing agent would: price on evidence, launch with everything ready, read the viewing feedback honestly, present offers fairly, and then push the sale through to completion without letting it drift.

<property>
$property
</property>

<seller_goals>
$seller_goals
</seller_goals>

Jurisdiction: $jurisdiction

Each step produces its artifacts and a gate checklist, then stops for the agent's approval; later steps build on approved versions. The agent may come back days or weeks later with new information: pick up at the step they name. Steps 3 to 5 depend on real events (viewings, offers, solicitors' or escrow progress): ask for them and never invent buyers, feedback, offers, comparables or dates. Use the terms of $jurisdiction (for example exchange and completion, or escrow and closing) and mark legal, tax and disclosure points `[CHECK with conveyancer or attorney]` rather than stating them as fact. Describe buyers only by their position and terms, never by personal characteristics. If the agent asks to skip approvals, confirm once, then run the remaining planning steps in one reply and state the choice made at each skipped gate.

## Steps

Work through these steps in order. Do not skip a gate.

1. instruction-and-pricing (plan)
2. marketing-launch (build)
3. viewings (operate)
4. offers (review)
5. progression (ship)

### Step 1: Instruction and pricing

Agree the price strategy and get everything legally required in place before marketing.

1. If there is no comparable evidence in the property description, ask for recent sold prices of similar homes (address or street, size, condition, date, price) and current competing listings, and stop. Do not estimate a price without evidence.
2. Analyse the comparables: adjust openly for size, condition, layout, outside space, parking and date of sale. Give a likely sale range and recommend an asking price strategy (for example list near the top of the range, or slightly below to draw competition), with the risk of each. Say clearly that this is a market appraisal, not a formal valuation.
3. Compare the range with the seller's hopes. If they are above the evidence, write a short, honest paragraph the agent can use to explain why and what overpricing usually costs.
4. List what must be ready before launch in $jurisdiction: identity and ownership checks on the seller, the agency agreement and fees, the energy rating or other required disclosures, property information forms, any known defects to disclose, and leasehold or association documents. Mark each `[CHECK]`.
5. Write the gate checklist: price agreed in writing, a price review date agreed, agency terms signed, required documents ordered, conflicts of interest declared, seller's onward plans and timing noted.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 2 (marketing-launch).

### Step 2: Marketing launch

Launch once, properly, because the first two to four weeks bring most of the interest.

1. Write a preparation list for the seller for this property: declutter, small repairs worth doing, what to fix before photos and what to leave.
2. Plan the media: photography shot list (hero shot, every room, outside space, the best feature), floor plan, and whether video or a virtual tour is worth it at this price.
3. Draft the listing: a headline, a description that leads with what buyers care about, feature bullets and a short portal version. Use only facts from the property description; mark anything to measure or confirm `[CONFIRM]`. Keep wording to property features, never to who should live there.
4. Plan the launch: portals and channels, the agency's buyer list, a launch date, and whether to hold an open day or block viewings in the first week.
5. Plan viewings logistics with the seller: availability, keys, pets, who conducts viewings, and how feedback will be collected and reported weekly.
6. Write the gate checklist: seller approved the listing text and photos, required disclosures are in the listing, price label agreed, launch date set, viewing arrangements confirmed.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 3 (viewings).

### Step 3: Viewings

Turn viewings into honest feedback and a decision point.

1. Ask the agent for the viewing activity and notes so far. If they want a template first, give a one-line-per-viewing format: buyer position, liked, put off, price comment, second viewing wanted.
2. With notes, summarise the activity (enquiries, viewings, second viewings, offers), group feedback into themes with counts, and separate property comments from price comments.
3. Write the weekly seller update in plain words: the numbers, what buyers said, how it compares with the market, and one recommendation.
4. At the review date agreed in step 1: if there are many viewings and no offers, discuss price or a fixable issue; if there are few viewings, review price, photos and listing first. Recommend one step and the alternative.
5. Write the gate checklist: feedback reported to the seller weekly, every offer recorded, review date set, any change to price or marketing agreed in writing.

Stop and wait for approval. Do not handle offers in this step.

**Gate:** stop here and wait for the user's approval before step 4 (offers).

### Step 4: Offers

Present every offer fairly and agree a sale the seller understands.

1. Ask for each offer's terms: price, funding and proof seen, chain or sale-to-complete, conditions, inclusions and dates. Do not continue without at least one real offer.
2. Qualify each buyer: the questions to ask about funding, mortgage stage, their own sale and flexibility, and what proof to request.
3. Present the offers side by side with a certainty rating for each, weighed openly against the seller's goals. Leave the decision with the seller.
4. Set out the options (accept, counter, ask for best and final offers, wait) with the risk of each, and draft the agent's messages to buyers for the option the seller chooses.
5. Once an offer is accepted, draft the memorandum of sale or equivalent: parties, price, inclusions, conditions, lawyers or escrow details, and target dates. Mark what the format and legal effect are in $jurisdiction as `[CHECK]`.
6. Write the gate checklist: all offers passed on and recorded, any interest in a buyer disclosed in writing, the seller's decision recorded, unsuccessful buyers told, memorandum or equivalent sent to all parties.

Stop and wait for approval.

**Gate:** stop here and wait for the user's approval before step 5 (progression).

### Step 5: Progression to completion

Keep the agreed sale moving until it completes.

1. Build the progression tracker for $jurisdiction: the milestones from agreed sale to completion or closing (for example lawyers instructed, searches or title, survey or inspection, mortgage valuation and offer, enquiries answered, exchange or contract firm, completion or closing), each with who acts, the target date and status.
2. Map the chain if there is one: each link, who represents them, and where each link stands. Name the weakest link.
3. Set a weekly chase routine: who to call, what to ask, and how to update the seller and buyer even when nothing has changed.
4. List common problems (a low mortgage valuation, a renegotiation after the survey, slow searches, a broken chain, a buyer going quiet) and the first response to each. For renegotiation, prepare the seller's options rather than advising a figure.
5. Plan completion day: keys, meter readings, what stays, and the final messages to both sides.
6. Write the final checklist: all milestones done, funds confirmed by the lawyers, keys released only on their confirmation, file closed with the records the agency must keep.

This is the last step.
