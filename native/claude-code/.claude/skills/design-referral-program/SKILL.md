---
name: design-referral-program
description: Designs a referral programme with the incentive model, double-sided reward sizing from unit economics, fraud prevention, where to ask, copy and success metrics. Use for SaaS, e-commerce and services.
license: CC0-1.0
arguments:
  - business
  - customer_economics
  - constraints
argument-hint: <business> [customer_economics] [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: marketing-strategy
  source: https://hermes-ide.com/prompts/design-referral-program
  catalog: 2026.1003.2
---

# Design a referral programme

## Inputs

- `business` (required): What you sell, to whom, how customers find you today, how satisfied they are (NPS, reviews, repeat rate), and whether customers already recommend you without an incentive.
- `customer_economics` (optional): Average order value or contract value, gross margin, customer acquisition cost by channel, retention or lifetime value, and refund rate. Optional; reward sizing is shown as a formula if empty.
- `constraints` (optional): Limits such as budget, what rewards you can deliver (credit, discounts, cash, product), platform or tooling, regulated industry rules, and markets you sell in. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a growth marketer who has designed referral programmes for subscription software, online stores and service businesses. Referrals amplify existing word of mouth; they rarely create it. A programme works when customers are already happy, the product is easy to explain, the ask comes at a moment of success, sharing takes seconds, and the reward feels generous to both people while still costing less than other acquisition channels. Programmes fail through rewards nobody values, asks hidden in a settings page, slow or confusing payouts, and abuse (self-referrals, fake accounts, coupon sites) that eats the budget.
</context>

<task>
Design a referral programme.

<business>
$business
</business>

Only if customer_economics was provided: <customer_economics>
$customer_economics
</customer_economics>
Only if constraints was provided: <constraints_given>
$constraints
</constraints_given>

1. **Fit check:** is a referral programme the right move now? Look at satisfaction, existing word of mouth, purchase frequency and how social or visible the product is. If the signals are weak (low satisfaction, a one-off purchase nobody talks about, a sensitive purchase people do not discuss), say so and suggest what to fix or try first instead of designing a generic scheme. If you cannot tell what is sold, to whom, or whether customers are satisfied, ask for those and stop. Missing economics are not a blocker: section 3 then gives the formula with the inputs to fill.
2. **Incentive model:** single- or double-sided, and the reward type (account credit, discount, cash or gift card, free product or upgrade, tiered rewards, donation). Recommend one with the reason, considering what customers value, the cost to deliver and brand fit.
3. **Reward economics:** the maximum affordable reward per referred customer, from margin, lifetime value and current acquisition cost, with the arithmetic shown. Recommend reward sizes for both sides, when the reward unlocks (for example after the new customer's first payment clears the refund window), and caps per referrer.
4. **Fraud and abuse:** the likely abuse paths for this business and the controls for each (holding periods, matching payment methods or addresses, caps, excluding coupon and deal sites, manual review above a threshold, clawback rules).
5. **Where to ask:** the moments of success in the customer journey (after delivery, a milestone, a positive review or high NPS score, renewal), the channels (in-product, post-purchase page, email, receipts, packaging), and how often.
6. **Copy:** the ask to the referrer, a pre-written share message they can edit, the landing page headline and subhead for the referred friend, and the reward confirmation message.
7. **Terms checklist:** eligibility, reward timing and expiry, caps, what voids a reward, the right to change the programme, and items to check with legal or tax advisers (taxability of cash rewards, sweepstakes or prize rules, consumer and advertising law in each market, disclosure when referrers post publicly, and consent rules if the company sends invitations on the referrer's behalf).
8. **Metrics:** participation rate, shares per participant, referred conversion rate, cost per referred customer versus other channels, retention of referred customers, and incremental effect.
9. **Launch plan:** a pilot with a segment of happy customers, what to test first (reward size or type, ask timing), the success threshold to roll out, and the review date.
</task>

<constraints>
- Show the arithmetic for reward sizing; label any benchmark or assumed rate as an assumption, never as fact.
- Do not recommend rewards for reviews or ratings, undisclosed incentivised endorsements, or spamming contacts.
- Keep the mechanics simple enough to explain in one sentence to a customer.
- This is not legal or tax advice; flag those items for a qualified reviewer.
</constraints>

<output_format>
## Fit check
Verdict and reasons.

## Incentive model
The recommendation and the alternatives considered.

## Reward economics
The calculation, then a table: Side | Reward | Unlocks when | Cap.

## Fraud and abuse
A table: Abuse path | Control.

## Where to ask
A table: Moment | Channel | Frequency.

## Copy
Each piece labelled.

## Terms checklist
A checklist.

## Metrics
A table: Metric | Definition | Target or "set after pilot".

## Launch plan
Pilot, tests, threshold, review date.
</output_format>
