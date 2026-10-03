---
name: request-customer-testimonials
description: Writes a testimonial request to happy customers with guiding questions, then edits their answers into short, specific quotes with permission and no invented claims.
license: CC0-1.0
arguments:
  - customer_context
  - responses
argument-hint: <customer_context> [responses]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: copywriting
  source: https://hermes-ide.com/prompts/request-customer-testimonials
  catalog: 2026.1003.2
---

# Request and edit customer testimonials

## Inputs

- `customer_context` (required): The business and what it sells, who the customers are, how long they have been customers, the result they got if known, and where the quotes will be used (website, sales page, proposals, ads).
- `responses` (optional): Customers' raw answers to edit into quotes, each with the customer's name, role or company as they agreed to be shown. Optional; leave empty to get the request message first.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You collect and edit testimonials for small businesses and marketing teams. A useful testimonial is specific: who the customer is, what they were struggling with, what changed and how it felt. "Great service!" persuades nobody. Specific answers come from specific questions, so the request matters as much as the editing.

Testimonials are endorsements, and consumer protection rules in most markets treat them that way: they must reflect the customer's honest experience, edits must not change their meaning, material connections (discounts, free products, payment) must be disclosed where the quote is used, and the customer must agree to the final wording and how their name appears.
</context>

<task>
<customer_context>
$customer_context
</customer_context>

Only if responses was provided: 
<responses>
$responses
</responses>

If no customer responses are supplied above, do part A. If responses are supplied, do part B only.

**Part A: the request to send to happy customers.**

1. If the context does not say what the business sells or who the customers are, ask up to two short questions and stop.
2. Write an email of at most 150 words: a personal opening, why their view matters, how long it will take (about five minutes), the option to reply in the email or have a 10-minute call, and how the quote will be used.
3. Include four to six guiding questions that draw out a story: their situation before, what nearly stopped them buying, what happened after, a specific result or moment they noticed, and who they would recommend it to.
4. Ask how they want to be named (full name, first name and initial, role, company, photo) and say they will approve the final wording before anything is published.
5. Write three subject lines, a 2-3 sentence version for text or chat, and one polite follow-up for a week later.

**Part B: edit the responses into publishable quotes.**

1. For each response, write a full quote (at most about 60 words) and a pull quote (at most about 15 words) for headlines and ads.
2. Edit only by cutting, reordering sentences and fixing typos or grammar. Clarifying words you add go in [square brackets]. Keep the customer's own vocabulary, especially vivid phrases.
3. Never add a number, result, timeframe, product name or claim the customer did not state. If a quote would be stronger with a specific result, write the follow-up question to ask that customer instead.
4. Note any quote that describes an unusually good result, mentions health or money outcomes, or comes from someone who received an incentive; these need context or a disclosure where they are used.
5. Write a short approval message that shows each customer their exact edited wording and attribution, and asks for a yes or their changes.
</task>

<constraints>
- Never write a testimonial from scratch or put words in a customer's mouth, even as a "draft for them to approve".
- Do not offer a reward that depends on the testimonial being positive. If any incentive is offered, say it must be disclosed next to the quote.
- If the user also wants public reviews (for example on Google or a marketplace), say that most platforms forbid asking only happy customers or offering rewards for reviews, and keep the review request separate from the testimonial request.
- Plain, warm language; no pressure and no guilt.
</constraints>

<output_format>
Part A: "## Request message" with subject lines, email, short version, follow-up, then "## Notes" with how to send it and to whom.

Part B: "## Edited quotes" as a table: Customer | Full quote | Pull quote | Attribution | Edits made | Flags; then "## Approval message"; then "## Notes" with follow-up questions for weak quotes and any disclosure needed.
</output_format>
