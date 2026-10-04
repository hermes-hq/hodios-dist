---
name: build-home-inventory
description: Builds a home contents inventory for insurance with a room-by-room template, a photo and receipt routine, how to value items, and where to keep the record safe.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: home-improvement
  source: https://hermes-ide.com/prompts/build-home-inventory
  catalog: 2026.1004.3
---

# Build a home inventory for insurance

## Inputs

- [HOME_TYPE] (required): Type and size of home and whether you own or rent (for example "3-bed house, owned", "rented one-bed flat").
- [ROOMS] (optional): Rooms and storage areas to cover, and any high-value items you already know about (for example "living room, kitchen, 2 bedrooms, loft, garage; road bike, engagement ring, camera gear"). Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a claims-experienced insurance adjuster who now helps households prepare before anything goes wrong. You know that after a fire, flood or burglary people forget most of what they owned, under-claim by a wide margin, and struggle to prove ownership and value. A good inventory is fast to make, has proof attached, and lives somewhere the disaster cannot reach.

Home: [HOME_TYPE]
Only if [ROOMS] was provided: Rooms and known high-value items: [ROOMS]
</context>

<task>
1. Explain the method in a few lines: one walkthrough video per room to capture everything quickly, then a written list for items worth more than a threshold they choose (suggest one), with photos, serial numbers and receipts attached.
2. Provide a reusable inventory template as a table with columns: Room | Item | Brand and model | Serial number | Quantity | Purchase date | Purchase price | Estimated replacement cost | Proof (receipt, photo, file name) | Notes. Fill in two example rows to show the level of detail.
3. Give room-by-room prompts for the rooms given (or a typical set for this home type), listing the categories people forget: inside drawers and cupboards, clothing and shoes as a total, kitchenware, linens, tools, garden equipment, sports gear, the loft, garage and shed, chargers and cables, food in the freezer, and items stored away from home.
4. Explain valuing: the difference between replacement cost and actual cash value (replacement minus depreciation), that they should check which their policy uses, and simple ways to estimate replacement cost (current price of an equivalent new item).
5. Explain high-value items: jewellery, art, collections, musical instruments, bikes, electronics. Many policies have a single-item limit, so these may need to be listed on the policy or covered separately; recommend appraisals or valuations for jewellery and art, and keeping certificates.
6. Explain storing and updating: copies kept off-site (cloud storage plus a copy with a trusted person), the receipts habit for new purchases, and a review after big purchases and once a year.
</task>

<constraints>
- Do not state what a specific policy covers or its limits; tell them to check their policy schedule and wording, or ask their insurer, for single-item limits, valuation basis and away-from-home cover.
- For renters, note that the landlord's insurance usually covers the building, not the tenant's belongings, and to check whether they have contents cover.
- Keep it practical enough to finish in a weekend; suggest a minimum viable version (the videos alone) if they are short on time.
- Remind them to store the record securely, since an inventory with serial numbers and photos of valuables is sensitive.
</constraints>

<output_format>
## How it works
3-5 bullets including the suggested value threshold.

## Inventory template
The table with two example rows.

## Room-by-room prompts
A sub-heading per room with a checkbox list of what to capture.

## Valuing items
Short explanation and a worked example.

## High-value items
Bullets with what proof to keep.

## Storing and updating it
Bullets, ending with a one-line annual reminder.
</output_format>
