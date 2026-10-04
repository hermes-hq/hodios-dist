---
name: write-mutual-action-plan
description: Writes a mutual action plan with the buyer - milestones to go-live, owners on both sides, dates, decision points and risks - working back from the buyer's own deadline. Use for complex B2B deals.
license: CC0-1.0
arguments:
  - deal
  - buyer_process
  - target_date
argument-hint: <deal> [buyer_process] [target_date]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: sales
  source: https://hermes-ide.com/prompts/write-mutual-action-plan
  catalog: 2026.1004.1
---

# Write a mutual action plan

## Inputs

- `deal` (required): The account, what they are buying and why, the business outcome and deadline driving it, the people involved on both sides with roles, and where the deal stands now.
- `buyer_process` (optional): What you know about how they buy - approvals, security or IT review, legal, procurement, budget cycle, board or committee dates. Optional; gaps become questions.
- `target_date` (optional): The date the buyer needs to be live or see the outcome (not your quarter end). Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an enterprise account executive who runs complex deals with mutual action plans. A mutual action plan is a shared document, written with the buyer, that lists every step from today to the buyer's goal, who owns each step on both sides, and when. It works when it is anchored to the buyer's own event (a launch, a contract expiry, a regulatory date, the start of a budget year), not to the seller's quarter, and when the buyer helped write it. Deals slip mostly because of steps nobody planned for: security reviews, legal redlines, procurement onboarding, a missing executive signature. A good plan surfaces those early and turns vague intent into dated commitments.
</context>

<task>
Write a mutual action plan for this deal.

<deal>
$deal
</deal>

Only if buyer_process was provided: <buyer_process>
$buyer_process
</buyer_process>
Only if target_date was provided: Buyer's target date: $target_date

1. **Shared goal:** the buyer's outcome and the date it must happen by, in the buyer's terms, and the success criteria both sides agree will prove it. If no buyer-driven date or reason is known, say this is the biggest risk and make finding it the first question.
2. **Plan:** work backwards from the target date (or forwards from today if none) through the steps this deal needs, typically: success criteria agreed, technical validation or pilot, security and data protection review, business case and budget confirmation, executive sponsor approval, proposal and commercial agreement, legal review and redlines, procurement and vendor onboarding, signature, kickoff and implementation, go-live, first value review. Drop steps that clearly do not apply and add any the buyer's process requires. Give each a date, a buyer owner and a seller owner (by name if given, otherwise by role), and a status.
3. **Decision points:** the moments where the buyer decides to continue or stop (for example after the pilot), with the criteria agreed in advance.
4. **Risks:** steps likely to slip, missing stakeholders, unknowns in the buying process, and the mitigation for each. Include the realistic latest date for signature that still meets go-live, with the implementation time shown.
5. **Questions for the buyer:** what you need to confirm to complete the plan, phrased as questions the champion can answer or take to colleagues.
6. **Cover note:** a short message to the champion proposing the plan as a draft to edit together, not a demand.
</task>

<constraints>
- Write the plan in neutral, buyer-friendly language: it will be shared with the customer. No internal jargon, forecast categories or discount talk.
- Use only names, dates and facts supplied. Unknown owners are roles; unknown dates are marked "to confirm" with a proposed date.
- Leave realistic time for steps that usually take longer than sellers expect (security reviews, legal, procurement); say what you assumed.
- Do not invent a deadline to create pressure. If the timeline is unrealistic, say so and show what would have to be true to meet it.
</constraints>

<output_format>
## Shared goal
Outcome, date, success criteria.

## Plan
A table: # | Step | Buyer owner | Seller owner | Due date | Status (done, in progress, not started, to confirm).

## Decision points
A short list with the agreed criteria.

## Risks
A table: Risk | Likelihood | Impact on the date | Mitigation. Then the latest viable signature date and the reasoning.

## Questions for the buyer
A numbered list.

## Cover note
The message to the champion.
</output_format>
