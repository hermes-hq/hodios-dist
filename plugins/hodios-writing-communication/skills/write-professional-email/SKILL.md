---
name: write-professional-email
description: Drafts an email from rough intent with a specific subject line, the ask in the first two sentences and the right tone for the relationship, marking any detail it would otherwise have to invent.
license: CC0-1.0
arguments:
  - intent
  - recipient
  - tone
argument-hint: <intent> <recipient> [tone]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: email
  source: https://hermes-ide.com/prompts/write-professional-email
  catalog: 2026.1003.0
---

# Write a professional email

## Inputs

- `intent` (required): What you want the email to achieve, in your own words, with any facts it must include (dates, amounts, attachments, context).
- `recipient` (required): Who it goes to and your relationship, for example "a client I've never met", "my manager", "a professor whose course I want to join".
- `tone` (optional; one of: formal, neutral, friendly; default: neutral): Overall register.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Busy recipients decide from the subject line and the first two sentences whether to act now, later or never. Emails get ignored when the ask is in the last paragraph, when several unrelated requests share one message, when the reader must work out what is wanted or by when, or when the tone is wrong for the relationship (over-familiar with a stranger, stiff with a close colleague). A good work email is short, makes the next step obvious and easy, and gives just enough context to act.
</context>

<task>
Write an email to $recipient in a $tone tone that achieves this:
<intent>
$intent
</intent>

1. If the intent does not make clear what the recipient should do or know, ask one short question and stop.
2. Name the single outcome you want from the recipient (a reply, a decision, a meeting, a document, awareness). If the intent mixes unrelated requests, put the main one in this email and note in Placeholders that the others may deserve their own.
3. Write a subject line that states the topic and the action, with a date if there is a deadline, for example "Approval needed by 12 May: Q3 travel budget".
4. Put the ask, or the key information, in the first two sentences. Then give only the context the recipient needs to act.
5. Make the next step easy: specific options or times, the deadline and why it matters, what is attached, and who else is involved.
6. Fit the relationship: a stranger gets a one-line reason you are writing to them and how you got their name; a senior or formal recipient gets full greetings and no slang; a friendly colleague gets brevity and contractions.
7. Close with a clear line about what happens next, then a sign-off suited to the tone.
</task>

<constraints>
- Under 150 words in the body unless the intent truly needs more; if it does, use short paragraphs or a short list.
- Never invent facts: names, dates, times, numbers, attachments, prior conversations or titles not in the input become `[placeholders]`.
- No filler openings ("I hope this email finds you well") unless the tone is formal and the relationship is new, and never more than one such line.
- No over-apologising, guilt-tripping or false urgency.
</constraints>

<output_format>
## Email
Subject: …
The email body, ready to paste.
## Placeholders
Bullets: each `[placeholder]` with what to put there, plus any split-out requests. "None" if none.
## Alternative subject lines
Two alternatives, one shorter and one more specific.
</output_format>
