---
name: ask-for-a-favor
description: Writes a request for a favour, such as an introduction, a review, borrowing something or help moving, that is specific, easy to decline and offers something back.
license: CC0-1.0
arguments:
  - favor
  - person
  - relationship_strength
  - deadline
argument-hint: <favor> <person> [relationship_strength] [deadline]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: interpersonal-communication
  source: https://hermes-ide.com/prompts/ask-for-a-favor
  catalog: 2026.1004.3
---

# Ask for a favour

## Inputs

- `favor` (required): What you need, as specifically as you can: what, how much time or effort, when, and why it matters to you, for example "an intro to the head of design at Lumen, I'm applying for a senior role there".
- `person` (required): Who you are asking and why them, for example "Ana, my former manager, now works at Lumen".
- `relationship_strength` (optional; one of: close, friendly, distant; default: friendly): How close you are.
- `deadline` (optional): Optional, when you need it by, for example "before 15 May" or "no rush".

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
People say yes to favours that are clear, sized honestly, easy to do and easy to refuse. Vague asks ("could you help me with my job search?") put the work on the helper, so they stall. Hidden size ("quick look" at a 40-page document) breeds resentment. Asks with no way out make a "no" feel like a rejection of the relationship. The best requests say exactly what is wanted and by when, explain why this person, do the preparation for them (a forwardable blurb for an introduction, the specific pages to review), give an explicit out, and offer something back that fits the relationship. With distant contacts, the ask should be smaller and the context fuller.
</context>

<task>
Write a request to $person for this favour. We are $relationship_strength.Only if deadline was provided:  Deadline: $deadline.

<favor>
$favor
</favor>

1. Fit check: compare the size of the favour, the deadline and the relationship. If the ask is large for the relationship or the deadline is too tight, say so and propose a smaller first ask (for example 20 minutes of advice instead of a full review, or a name instead of an introduction) and write the message for that smaller ask, with the original as an option.
2. Choose the channel (text, email, LinkedIn message, in person) that suits the relationship and the favour, and say why in one line.
3. Write the ask:
   - context first if we are not close: who I am to them and how we know each other;
   - why I am asking them specifically;
   - exactly what I am asking for, its honest size (time, effort) and the deadline;
   - an explicit, warm out ("Completely fine if the timing doesn't work");
   - an offer back that fits, or a sincere thank-you if we are close and an offer would feel transactional.
4. Make it easy: draft what they would need, for example a short forwardable blurb for an introduction (with a double opt-in suggestion so the third person can agree first), the exact questions for an advice call, or the specific sections for a review.
5. If they say no or do not reply: one gracious reply to a no, and a single follow-up after a sensible interval. Then let it go.
</task>

<constraints>
- No guilt, flattery or pressure. No exaggerating the urgency.
- Keep it short: a text is two to four sentences, an email under 150 words, plus any blurb.
- Do not invent facts about me, them or the third party; use `[placeholders]`.
- Match how I would normally write to this person.
</constraints>

<output_format>
## Fit check
One to three lines, and the channel.
## The ask
The message in a quote block (and the original larger ask as an option, if you proposed a smaller one).
## Make it easy
The blurb, questions or materials, in a quote block, or "Nothing needed."
## Offer back
One or two ideas that fit, or why a thank-you is enough.
## If they say no or do not reply
A reply to a no, and a follow-up message with when to send it.
</output_format>
