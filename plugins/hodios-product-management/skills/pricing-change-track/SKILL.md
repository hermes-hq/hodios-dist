---
name: pricing-change-track
description: Takes a pricing change through gated steps, from research and options to an impact model, a communication plan and a rollout review, pausing for the owner's approval between steps.
license: CC0-1.0
arguments:
  - current_pricing
  - goals
argument-hint: <current_pricing> <goals>
disable-model-invocation: true
metadata:
  version: 1.0.2
  kind: workflow
  category: product-strategy
  source: https://hermes-ide.com/prompts/pricing-change-track
  catalog: 2026.1003.1
---

# Pricing change track

## Inputs

- `current_pricing` (required): Today's plans, prices, value metric, discounts and contract terms, the customer base by plan and segment (counts and MRR if possible), and recent pricing history.
- `goals` (required): Why pricing should change (revenue, margin, moving upmarket, simpler packaging, monetising a new capability), constraints, the decision owner and any deadline.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Takes a pricing change from evidence to rollout, one approved step at a time.

<current_pricing>
$current_pricing
</current_pricing>

<goals>
$goals
</goals>

Research (what customers value and pay, what the evidence says), two to four options, a revenue and churn impact model for the chosen one, the communication and rollout plan, then a post-launch review. Each step produces one document and stops for the owner's approval or edits; later steps build on approved versions rather than re-asking. Never invent customer data, willingness-to-pay results, competitor prices or elasticity figures: unknowns become labelled assumptions with ranges, or research to run. The owner makes every pricing decision. Pricing is never discussed or coordinated with competitors, and customer-facing terms are checked against existing contracts and consumer rules in the markets served.

## Steps

Work through these steps in order. Do not skip a gate.

1. research (discover)
2. options (plan)
3. impact-model (plan)
4. communication (build)
5. rollout-review (review)

### Step 1: Research

Establish what the evidence says before anyone proposes a price.

1. Ask the owner, in one message, for anything essential that is missing: customers by plan and segment with MRR, discounts actually given, usage of the likely value metric, churn and downgrade reasons, win and loss notes on price, existing willingness-to-pay research, contract terms (annual commitments, price locks), and the decision owner. Skip this if enough is given.
2. When you have the answers, write:
   - **Goal restated:** the business outcome and how success will be measured, in two sentences.
   - **Value metric review:** whether the current metric grows with customer value; alternatives (seats, usage, outcomes, features) with pros and cons.
   - **What customers value:** capabilities that drive retention and upgrades, each claim marked as evidence or assumption.
   - **Price position:** list against realised price after discounts, and where the user's notes place competitors; mark competitor prices "to verify".
   - **Segments:** which customer groups are underpriced, fairly priced or at risk, with the reasoning.
   - **Evidence gaps:** what is missing and the cheapest way to fill it (willingness-to-pay survey, ten interviews, a pricing-page test on new visitors), with how long each takes.
3. Recommend whether there is enough evidence to design options now or whether to run research first.

Stop and wait for approval or edits. Do not propose options yet.

**Gate:** stop here and wait for the user's approval before step 2 (options).

### Step 2: Options

Design two to four distinct pricing options from the approved research.

1. For each option, specify:
   - the plans, what each includes, the value metric and the price points (as proposals or ranges, tied to the research);
   - who it is designed for and which segment's price changes most;
   - how it serves the goal, and what it trades away;
   - treatment of existing customers: grandfather indefinitely, grandfather for a fixed period, migrate at renewal, or migrate with a transition discount;
   - risks: churn in price-sensitive segments, sales confusion, billing work, perceived fairness, contract clauses that limit changes.
2. Include one conservative option (new customers only, or packaging changes without raising list prices) to compare ambition against risk.
3. Compare the options in a table: goal fit, revenue direction, churn risk, complexity to build and explain, reversibility.
4. Recommend one option with the deciding reasons and say what evidence would change the recommendation.

Stop and wait for the owner to choose or adjust an option. Do not build the impact model yet.

**Gate:** stop here and wait for the user's approval before step 3 (impact-model).

### Step 3: Impact model

Model the revenue and churn impact of the chosen option so the owner can change any assumption.

1. A table with one row per segment and plan: customers, current MRR, new MRR, change per customer, assumed churn or downgrade caused by the change, and resulting MRR.
2. Write the formula used: `new MRR = Σ over segments (customers × (1 − added churn) × new price per customer)`, plus expected uplift in new-customer conversion or average deal size if the option affects it.
3. Phase the effect: existing customers move only when the option says (at renewal, after grandfathering or a transition discount), so show MRR month by month for twelve months from the renewal calendar, not as if everyone moved on day one.
4. Run pessimistic, expected and optimistic scenarios by varying added churn and new-customer conversion. Label every assumption's source (step 1 research, the owner's estimate, or a placeholder); none is fact.
5. Calculate the break-even churn: the share of affected customers who could leave before the change loses revenue.
6. Non-revenue effects to watch: support volume, sales cycle length, discount requests, community reaction.
7. Guardrails that would pause or reverse the rollout (for example affected-segment churn above a threshold for two months running).

Stop and wait for approval or changes to the assumptions. Do not write customer communication yet.

**Gate:** stop here and wait for the user's approval before step 4 (communication).

### Step 4: Communication and rollout plan

Plan how the change reaches customers, the team and the systems, based on the approved option and model.

1. **Rollout sequence.** Internal readiness (billing, pricing page, quotes and contracts, analytics), then new customers, then existing ones by segment and renewal date. Set the notice period, longer where prices rise, and check it against contracts and consumer rules in the markets served (flag for legal review; give no legal conclusions).
2. **Customer email** for each affected group: what changes, when, why (in terms of value the customer gets, never only "costs went up"), what it means for their bill in concrete terms, their options (grandfathering, annual lock-in, downgrade), and who to contact. Plain, direct, no burying the price in the fourth paragraph.
3. **Internal enablement.** A one-page brief for support, sales and customer success: the change, the reasoning, a talk track, answers to the ten likely questions, what discounts or exceptions are allowed and who approves them.
4. **Pricing page and in-product changes**, listed for the web and product teams.
5. **Monitoring plan** tied to the step 3 guardrails: what is tracked daily for two weeks and weekly after, who watches, the review date.

Use [DATE], [LINK] and [OWNER] placeholders; never invent them.

Stop and wait for approval before rollout. The next step runs after launch, once results are available.

**Gate:** stop here and wait for the user's approval before step 5 (rollout-review).

### Step 5: Rollout review

Review the results once the owner shares post-launch data (typically after one to three billing cycles).

1. Ask for missing data: MRR by segment before and after, churn and downgrades in affected segments against unaffected ones and last year, new-customer conversion and deal size, discount and exception volume, support themes and notable reactions.
2. Compare actual results with the three scenarios from the impact model, segment by segment. Say which assumptions held and which were wrong.
3. Check the guardrails. If any were crossed, say so first and lay out the options (pause, adjust for a segment, offer a transition discount, reverse).
4. Separate the pricing effect from other causes where the data allows (seasonality, a product launch, a competitor move), and state the confidence of each conclusion.
5. Recommend: keep as is, adjust (say what), or roll back, with the reasoning.
6. List lessons for the next pricing change: what research was missing, which assumptions to measure better, and what to do differently in communication.

Close the track with a short summary the owner can share with leadership.
