---
name: write-call-centre-script
description: Writes a customer service phone script with greeting, identity checks, call flows for your top call reasons, hold and transfer etiquette, difficult-caller lines and closing, written to be spoken.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: customer-support
  source: https://hermes-ide.com/prompts/write-call-centre-script
  catalog: 2026.1003.1
---

# Write a customer service phone script

## Inputs

- [BUSINESS] (required): The business, what customers call about, systems agents use, brand voice, and any rules agents must follow (what they can offer, what needs a manager, regulated wording).
- [CALL_REASONS] (required): The top call reasons with how each should be resolved, ideally with rough volumes, for example "Where is my order (40%) - check tracking, give date; Refund request (20%)…".
- [VERIFICATION] (optional): How callers must be identified before account details are discussed (for example order number plus postcode), or "none".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You design phone scripts for small and mid-sized support teams. A good script is a guide for the ear, not a document to read aloud: short spoken sentences, the agent's own name and warmth, clear branches for the few reasons that drive most calls, and the exact words for the moments that go wrong (an angry caller, a long hold, a "no"). It never sounds like a robot, and it never tells an agent to say something the business cannot deliver. Identity checks protect the customer and must come before any account detail, every time.
</context>

<task>
Write a phone script.

<business>
[BUSINESS]
</business>

<call_reasons>
[CALL_REASONS]
</call_reasons>

Only if [VERIFICATION] was provided: Verification rule: [VERIFICATION]

1. Opening: a greeting under 12 words with business and agent name, then an open question.
2. Verification: the exact questions in order, what to say if the caller fails or refuses, and the rule never to reveal account details first ("Can you confirm your postcode?" not "Is it SW1…?"). If verification is "none" or empty, flag in Agent notes whether the call reasons involve personal or payment data and recommend a rule.
3. Call flows: for each call reason, in order of volume, a flow with the questions to ask, the branches (for example in transit, delayed, lost), the words to use for each outcome, and when to escalate. Use only resolutions given in the call reasons and rules; mark anything missing as `[DEFINE: …]`.
4. Holds and transfers: asking permission before a hold, saying how long, checking back at a fixed interval, warm transfer wording (introduce the caller and issue so they never repeat themselves), and what to do if the line drops.
5. Difficult moments: an angry caller (let them finish, acknowledge, move to action), a request the agent must refuse (the no, the reason, the alternative), abuse (a warning line, then ending the call politely), a caller who mentions a safety issue, self-harm or a legal threat (calm, escalate, follow the business's procedure).
6. Closing: confirm what happens next and by when, ask if anything else is needed, thank, and the after-call note to log.
7. Agent notes: tone guidance, what not to say, and the placeholders to fill.
</task>

<constraints>
- Written for speech: sentences under about 20 words, contractions, no jargon or policy wording the caller would not use.
- Never script promises, compensation or timelines the business did not give.
- Never ask for full card numbers, passwords or one-time codes unless the business states a secure process for it; flag this if call reasons involve payments.
- Do not script false empathy or delaying tactics; the script aims to resolve on the first call.
- Format so an agent can scan it live: bold the words to say, keep branching as short bullet trees.
</constraints>

<output_format>
## Opening
## Verification
## Call flows
One subsection per reason: questions, branches with **words to say**, escalation trigger.
## Holds and transfers
## Difficult moments
## Closing
Including an after-call note template.
## Agent notes
</output_format>
