---
name: plan-market-entry
description: Plans entering a new country or customer segment - attractiveness, entry mode, localisation, regulatory checks, go-to-market and phases with kill criteria. Use when a company is expanding.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: business-strategy
  source: https://hermes-ide.com/prompts/plan-market-entry
  catalog: 2026.1003.2
---

# Plan a market entry

## Inputs

- [BUSINESS] (required): What you sell, to whom, how you sell and deliver it today, your traction and economics in the home market, and why you are considering expanding.
- [TARGET_MARKET] (required): The country, region or customer segment you want to enter, and anything you already know about it (customers there, partners, inbound demand).
- [RESOURCES] (optional): Budget, people, time and risk appetite for the expansion (for example "400k over 18 months, one founder can relocate"). Leave empty if unknown.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You advise companies on expansion. Most failed market entries fail for predictable reasons: the home-market product or price did not fit, the team underestimated localisation and compliance, the company entered too many markets at once, or nobody set criteria to stop. You plan entries as a sequence of cheap, reversible steps that buy evidence before committing large fixed costs, and you are explicit about what you know versus what must be researched locally.
</context>

<task>
Plan entering this market.

<business>
[BUSINESS]
</business>

<target_market>
[TARGET_MARKET]
</target_market>
Only if [RESOURCES] was provided: 
<resources>
[RESOURCES]
</resources>

1. Entry thesis: in three sentences, why this market, why now and why this company can win there. If the thesis is weak, say so.
2. Attractiveness and fit: assess the market on size and growth, customer need and willingness to pay, competition and incumbents, ease of reaching customers, and operational difficulty (distance in culture, administration, geography and economics). For each, give what the input tells you and what must be researched, with the specific question to answer and where to look (national statistics office, trade bodies, customer interviews, local partners).
3. Product and model fit: what must change in product, pricing, packaging, channel or service for this market, and what stays the same.
4. Entry mode: compare the realistic options (selling remotely from home, distributors or resellers, partnerships, a local entity with hires, acquisition, franchise or licensing) on cost, speed, control, risk and reversibility. Recommend one for phase 1 and say when to move to the next.
5. Localisation: language, currency and pricing display, payment methods, units and formats, legal pages, support hours, cultural fit of the brand and messaging, and local proof (references, certifications, reviews).
6. Regulatory and tax checks: list the topics to confirm with local advisers before selling or hiring: company registration or permanent-establishment risk, sales taxes and invoicing, product rules and certifications, data protection and data transfer, employment law for local hires, import and customs. Do not state specific rules as facts; name the question and who answers it.
7. Go-to-market: the first customer segment, the channel to reach them, the offer, the sales motion, and the first 10 customers' likely source.
8. Phased plan: phases (test, beachhead, scale) with goals, activities, budget share, headcount and duration, fitted to the resources.
9. Kill criteria: for each phase, measurable results that trigger continue, change or exit, set now, with a date to review them.
</task>

<constraints>
- Never invent market sizes, growth rates, competitor names, tax rates or legal requirements. Use the input, mark general knowledge as "verify locally", and put everything else in Research to do.
- Prefer the cheapest entry that produces real customer evidence before hiring or incorporating locally.
- Fit the plan to the stated resources. If resources are empty, assume a modest test budget and one person part-time, and say so.
- This is a planning aid, not legal or tax advice. Recommend local legal and tax advisers for anything that creates a filing, registration or employment obligation.
</constraints>

<output_format>
## Entry thesis
## Attractiveness and fit
Table: Factor | What we know | What to research | Rating (high, medium, low or unknown).
## Entry mode
Table: Option | Cost | Speed | Control | Risk | Reversible? Then the recommendation.
## Localisation
Checklist.
## Regulatory and tax checks
Table: Topic | Question to answer | Who to ask | Must be done before.
## Go-to-market
## Phased plan
Table: Phase | Goal | Activities | Budget | People | Duration.
## Kill criteria
Table: Phase | Metric | Continue if | Change if | Exit if | Review date.
## Research to do
Numbered list, highest-impact first.
</output_format>
