---
name: check-tone-before-sending
description: Reviews a message someone is about to send for how it may land, such as too blunt, passive-aggressive, unclear or over-apologetic, and suggests minimal edits that keep their intent.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: editing
  source: https://hermes-ide.com/prompts/check-tone-before-sending
  catalog: 2026.1004.3
---

# Check tone before sending

## Inputs

- [MESSAGE] (required): The message exactly as you plan to send it.
- [RECIPIENT_RELATIONSHIP] (required): Who receives it and your relationship, for example "my direct report, new in the job", "a client I've never met", "my sister, we argued last week".
- [INTENT] (required): What you want the message to achieve and how you want to come across, for example "get the numbers by Friday without sounding annoyed".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Written messages lose the voice and face that soften spoken words, and readers fill the gap with their own mood, so neutral text often reads as colder than intended and short replies read as annoyed. The usual culprits are small and fixable: a curt one-liner to someone junior, "per my last email", "as I said", a lone "Noted.", "thanks in advance" as pressure, sarcasm, capitals, a request with no deadline or owner, or the opposite, three apologies and four hedges before the ask. A tone check is a light touch: name the risk, change the fewest words, keep the sender's voice and point.
</context>

<task>
Check how this message will land before I send it.

<message>
[MESSAGE]
</message>
Recipient: [RECIPIENT_RELATIONSHIP]
<intent>
[INTENT]
</intent>

1. If the message is empty, ask for it and stop.
2. Read it as the recipient, given the relationship, the power balance and the likely channel (inferred from the format). Write the most likely reading and the worst plausible reading, one sentence each.
3. Compare those readings with my intent. Name the gap.
4. Check for these risks and flag only the ones present, quoting the exact words:
   - too blunt or curt for this relationship;
   - passive-aggressive markers (pointed reminders of earlier messages, sarcasm, loaded punctuation, quotation marks around their words, "Noted.", "Thanks in advance" used as pressure);
   - blame phrasing ("you didn't", "you always") where a neutral fact would do;
   - an unclear ask: missing what, who, or by when, or a question buried mid-paragraph;
   - over-apologising or over-hedging that undercuts the point;
   - mismatch of length, formality or emoji with the relationship;
   - anything that could be forwarded or screenshotted and look bad out of context.
5. Make the smallest edits that close the gap: change words, not the whole message. Keep my voice, my point and any firm line I intend. If it already works, say "Send as is" and change nothing.
6. If the message is written in anger, or its real intent is to hurt or win, say so kindly and suggest waiting or talking instead.
</task>

<constraints>
- Do not soften a deliberate firm message into a vague one; keep requests, refusals, deadlines and facts at the same strength.
- Do not add apologies, compliments or promises I did not make.
- Keep it about this message; no general lecture on communication.
</constraints>

<output_format>
## Verdict
One of: **Send as is**, **Send with small edits**, **Rethink before sending**, with one line on why.
## How it may land
Most likely reading, then worst plausible reading, one line each.
## Flags
A table: Words | Risk | Suggested change. "None" if there are no flags.
## Edited message
The full message with the minimal edits applied, ready to copy. Omit this section if the verdict is Send as is.
## Before you send
One or two bullets, such as timing, channel or a fact to double-check. "None" if none.
</output_format>
