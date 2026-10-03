---
name: write-follow-up-email
description: Writes a polite follow-up to an unanswered email that adds new context, makes the ask easier to answer and sets a gentle deadline, in three escalation levels from nudge to final note.
license: CC0-1.0
arguments:
  - original_email
  - days_since
  - relationship
argument-hint: <original_email> [days_since] [relationship]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: email
  source: https://hermes-ide.com/prompts/write-follow-up-email
  catalog: 2026.1003.2
---

# Write a follow-up to an unanswered email

## Inputs

- `original_email` (required): The email you sent that has not been answered, including its subject line and any deadline it mentioned.
- `days_since` (optional; default: 5): How many days ago you sent it.
- `relationship` (optional): Who the recipient is to you, for example "hiring manager I interviewed with", "client's finance team", "a senior colleague in another department", "a stranger I cold-emailed".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Most unanswered emails are not refusals. The recipient was busy, the ask was unclear or too big to answer quickly, or it sank under newer mail. A follow-up that just says "Just checking in!" or "Bumping this to the top of your inbox" adds nothing and can read as passive-aggressive. Follow-ups that work restate the ask in one line, make it easier to say yes (a yes or no question, a choice of two options, a default the sender will act on), add something new (a fact, a deadline, a smaller version of the request), and get shorter and clearer with each round, while staying courteous.
</context>

<task>
Write follow-ups to this email, sent $days_since days ago with no reply.
Only if relationship was provided: The recipient is: $relationship.

<original_email>
$original_email
</original_email>

1. If the original email is missing or has no identifiable ask, say what is unclear and ask what the sender needs from the recipient, then stop.
2. Diagnose why it may have gone unanswered: was the ask buried, vague, too big, or missing a deadline? Name the one change that will help most.
3. Write three escalating follow-ups, each designed to be sent as a reply in the same thread so the original stays below:
   - **Follow-up 1 (gentle nudge):** two to four sentences. Restate the ask in one clear line, add one helpful element (new context, a link, a smaller ask or a yes-or-no version), and propose a soft date.
   - **Follow-up 2 (make it easy):** shorter. Offer a choice or a default ("If I don't hear by Thursday, I'll go ahead with option A"), or offer another route (a 10-minute call, the right person to ask instead).
   - **Follow-up 3 (close the loop):** a courteous final note that releases the recipient or states what the sender will do next, leaving the door open. Only include a default action the sender can genuinely take.
4. Keep the subject line of the thread; suggest a clearer subject only if the original was vague, as "Re: [original]" plus the ask.
5. Recommend when to send each one, adjusted for the relationship, any deadline in the original, and the $days_since days already passed.
</task>

<constraints>
- Polite, warm and direct. No guilt ("I know you're busy, but…" repeated), no sarcasm, no "per my last email", no fake urgency or invented deadlines. A deadline must come from the original or be clearly the sender's own preference.
- Do not assume the recipient is ignoring the sender, and never threaten.
- Match the formality of the original email and the relationship. For a hiring manager or a senior person, keep it brief and deferential; for a supplier who owes a deliverable, it can be firmer.
- Do not invent facts, attachments or prior conversations.
- If more than one follow-up would be inappropriate (for example a job application after a final round, or a personal message), say so and recommend only what fits.
</constraints>

<output_format>
## Diagnosis
One or two sentences.
## Follow-up 1
Subject line, then the email.
## Follow-up 2
Subject line, then the email, or "Not recommended" and the reason when a second follow-up would not fit the situation.
## Follow-up 3
Subject line, then the email, or "Not recommended" and the reason.
## Timing
When to send each, and when to switch channel (call, chat, someone else) instead.
</output_format>
