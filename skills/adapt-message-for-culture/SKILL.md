---
name: adapt-message-for-culture
description: Adapts a message, in the same language, for a reader from a different business culture by adjusting directness, hierarchy, context and politeness, and explains each change.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: interpersonal-communication
  source: https://hermes-ide.com/prompts/adapt-message-for-culture
  catalog: 2026.1003.1
---

# Adapt a message for another business culture

## Inputs

- [MESSAGE] (required): The message as you would send it, plus a line on its purpose (a request, feedback, a refusal, a deadline reminder, an introduction).
- [READER_CULTURE] (required): The reader's business culture, as specific as you can: country or region, and anything you know about their organisation and seniority, for example "senior partner at a Japanese trading company".
- [WRITER_CULTURE] (optional): Optional: your own business culture, so the changes are explained relative to it.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
The same words land differently across business cultures. A Dutch "this won't work" is ordinary candour; to a reader used to indirect disagreement it can read as an attack, while an indirect hint can be missed entirely by a reader used to plain statements. The differences that matter most in writing are well documented in cross-cultural research (for example Erin Meyer's culture map and Hall's high- and low-context communication): how directly disagreement and negative feedback are stated, how much hierarchy and formal address are expected, how much relationship-building comes before the task, how explicit the message is versus implied by context, how firmly deadlines are stated, and the politeness formulas expected at the start and end. These are tendencies, not rules: the individual, their company and their exposure to other cultures often matter more than nationality.
</context>

<task>
Adapt this message for a reader whose business culture is: [READER_CULTURE].
Only if [WRITER_CULTURE] was provided: My own business culture: [WRITER_CULTURE].

<message>
[MESSAGE]
</message>

1. If the reader culture is too broad to adapt for meaningfully (for example "Asian" or "European"), ask which country or organisation, and stop. If the purpose of the message is unclear, ask.
2. Identify the message's purpose and its must-keep content: the facts, the ask, the deadline, any refusal or criticism.
3. Assess the message on the dimensions that matter for this reader: directness of requests and criticism, formality and hierarchy (titles, address, who is copied), relationship before task, explicit versus implicit, how deadlines and commitments are stated, and opening and closing courtesies.
4. Rewrite it in the same language for this reader, changing only what the culture gap requires.
5. Explain each change: what it was, what it is now, and why, relative to the writer's culture if given.
</task>

<constraints>
- Keep the substance. The ask, deadline, refusal or criticism must still be unmistakable to this reader; adapt how it is said, never whether it is said. If softening risks the point being missed, say so and keep it clear.
- Same language as the original. Do not translate.
- Describe cultural patterns as tendencies with the reason behind them; no stereotypes, jokes or claims about what "they" are like as people.
- Do not add flattery, invented personal details or relationship-building lines that claim things that did not happen (for example "It was wonderful meeting you" if no meeting is mentioned). Use a `[slot]` when a personal touch needs a real fact.
- If the original is already well suited to the reader, say so and change little.
- Keep the length appropriate to the reader's culture, and say if it grew and why.
</constraints>

<output_format>
## Adapted message
The full message, ready to send.
## What changed
A table: Original | Adapted | Why (the cultural dimension and the reason).
## Kept as is
One or two lines on what you deliberately did not change.
## Check before sending
Two or three things to verify with someone who knows this reader or organisation, such as the right form of address or whether to copy their manager.
</output_format>
