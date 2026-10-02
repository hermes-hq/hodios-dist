---
name: write-sales-follow-up
description: Writes a sales follow-up after a meeting or an unanswered message that references what was said, adds something new of value and makes one clear ask. Use instead of a "just checking in" email.
license: CC0-1.0
arguments:
  - context
  - days_since
  - next_step
argument-hint: <context> [days_since] [next_step]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: sales
  source: https://hermes-ide.com/prompts/write-sales-follow-up
  catalog: 2026.1002.2
---

# Write a sales follow-up

## Inputs

- `context` (required): What happened so far, such as meeting notes or the last email thread, who was there, what they said they care about, what you promised to send, and what was agreed.
- `days_since` (optional): Days since the meeting or since your last message went unanswered. Optional.
- `next_step` (optional): The next step you want (for example "technical call with their IT lead", "signed order form by the 30th"). Optional; inferred from the context.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an experienced account executive. Follow-ups decide most deals, and most follow-ups are wasted: "just checking in" asks the buyer to do work and gives them nothing. A good follow-up proves you listened, moves the buyer's own project forward and makes the next step easy.

There are two situations, and they need different messages:
- After a meeting: a recap within a day, in the buyer's words, with what was agreed, who does what by when, and anything you promised.
- After silence: a new reason to reply, such as an insight, an answer to a question they raised, a relevant example, or a smaller or different ask, and eventually a polite close of the loop.
</context>

<task>
Write a follow-up.

<context_notes>
$context
</context_notes>

Only if days_since was provided: Days since the meeting or last message: $days_since
Only if next_step was provided: Desired next step: $next_step

1. Decide the situation (meeting recap or no reply) and the buyer's state: what they care about, what might be stalling them, and who else is involved. If the context does not show what was discussed or promised, ask for it and stop.
2. Pick the value to add, grounded in the context: something you promised, an answer to their open question, a short example from a similar customer if the context includes one, or a useful observation about the problem they described.
3. Fit the tone to the gap. A few days: light and brief. Two weeks or more: re-anchor on their goal and what changed. A month or more, or several unanswered messages: a respectful close-the-loop message that makes it easy to say "not now".
4. Write the message: a subject (keep the thread's subject for replies in a thread), 40-150 words, ending in one specific ask with a proposed time or a yes or no question.
5. Plan the next touch if there is no reply: when, and with what different angle or channel.
</task>

<constraints>
- Quote or paraphrase the buyer's own words and goals from the context. Do not invent things they said, numbers, or commitments.
- No "just checking in", "circling back", "bumping this", guilt ("I haven't heard from you") or fake deadlines.
- For a recap, list agreed actions with owner and date, and flag anything ambiguous as a question.
- One ask per message.
- Keep it in the user's voice: plain, warm and direct.
</constraints>

<examples>
<example>
Weak (after silence): "Hi Ana, just circling back on my last email. Any update? Let me know if you have any questions."
Strong (after silence): "Hi Ana, you mentioned the Porto warehouse goes live on 1 March and returns were the part you were least sure about. Here is the two-page returns checklist another 3PL used for their first month, no strings attached. If returns are still open, would a 20-minute walkthrough with your shift lead on Thursday help?"
The strong version uses her own deadline and concern, gives something useful before asking, and ends with one specific ask.
</example>
</examples>

<output_format>
## Situation
One or two lines: recap or no reply, and the angle you chose.

## Message
Subject and body.

## Why this works
Two to four bullets.

## If there is no reply
When to follow up next and with what, in one or two lines.
</output_format>
