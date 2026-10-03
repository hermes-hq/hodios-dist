---
name: request-approval-by-email
description: Writes a bottom-line-first email asking a busy decision-maker to approve a budget, purchase, hire or exception, with options, cost, the risk of waiting and a one-line reply path.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: email
  source: https://hermes-ide.com/prompts/request-approval-by-email
  catalog: 2026.1003.2
---

# Request approval by email

## Inputs

- [REQUEST] (required): What you need approved and why, with the cost, the options you considered, what happens if it is not approved, and anything already checked (budget line, policy, quotes).
- [APPROVER_CONTEXT] (optional): Who approves and what they care about, for example "CFO, cost-focused, reads on phone" or "my director, wants to see we tried cheaper options".
- [DEADLINE] (optional): When you need the answer and why that date matters.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Approvers read approval requests on a phone between meetings. They say yes quickly when the first two lines tell them exactly what they are approving, how much it costs, and by when, and when the email shows the obvious objections have been handled: cheaper options, budget availability, policy, and what happens if they wait. Requests stall when the ask is buried after three paragraphs of background, when the approver has to reply with questions, or when the cost or the option being recommended is unclear. The bottom line up front (BLUF) pattern used in military and consulting writing exists for this reason.
</context>

<task>
Write an approval request email.Only if [APPROVER_CONTEXT] was provided:  Approver: [APPROVER_CONTEXT].Only if [DEADLINE] was provided:  Answer needed by: [DEADLINE].

<request>
[REQUEST]
</request>

1. If you cannot tell what exactly is to be approved or roughly what it costs (money, headcount, time or risk), ask one or two questions and stop.
2. Write the subject line as "Approval needed by [date]: [what], [cost]". Use `[date]` if no deadline was given.
3. First two lines (the BLUF): the request in one sentence, including the amount and what it buys; and the reply you need ("Please reply 'Approved' or tell me which option you prefer by Thursday so we can place the order before the price rise").
4. Then, in short labelled blocks:
   - **Why:** the problem or opportunity in one or two sentences, with the business effect in numbers where the input gives them.
   - **Options:** two or three, including "do nothing" or a cheaper alternative, each with cost and main trade-off, and the recommended option marked. Skip if the input truly has a single option, and say why.
   - **Cost of waiting:** what happens if the decision slips (price, lost revenue, risk, missed deadline), only from the input.
   - **Already checked:** budget line, policy, quotes, who else agrees. Only what the input says.
5. Close with a one-line reply path ("Reply 'Approved' to go ahead with Option B") and an offer of a short call only if the request is complex.
6. Under Before sending, list attachments to include (quotes, the business case) and any `[need: …]` items.
</task>

<constraints>
- Under about 180 words in the body; it must fit on a phone screen with little scrolling.
- Use only facts in the input. Never invent costs, quotes, savings or approvals; use `[need: …]`.
- Confident, not pleading: no "sorry to bother you", no "if possible, at your convenience".
- Tailor the emphasis to the approver context if given (cost for finance, risk for legal, speed for operations), without changing the facts.
- If the request needs an exception to policy, say so plainly in the first lines rather than hoping it goes unnoticed.
</constraints>

<output_format>
## Email
Subject line, then the email body.
## Before sending
Bullets: attachments, `[need: …]` placeholders, and anyone who should be told or copied first. "Ready to send" if nothing.
</output_format>

<examples>
Weak opening: "Hi Anna, as you may know, the team has been discussing the challenges we've been having with the current laptops for some time…"
Strong opening: "Hi Anna, could you approve 9,600 EUR for 8 replacement laptops for the support team? Please reply 'Approved' by Thursday 6 Nov; the supplier's price rises 12% on 10 Nov."
</examples>
