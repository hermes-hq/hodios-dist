---
name: summarize-group-chat
description: Summarises a busy group chat or channel since you last read it into decisions, questions for you, plans with dates and what can safely be ignored.
license: CC0-1.0
arguments:
  - chat_log
  - your_name
  - priorities
argument-hint: <chat_log> <your_name> [priorities]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: summarization
  source: https://hermes-ide.com/prompts/summarize-group-chat
  catalog: 2026.1004.3
---

# Summarise a group chat

## Inputs

- `chat_log` (required): The messages you missed, copied or exported with names and times (a WhatsApp, Signal, Slack, Teams or Discord export works).
- `your_name` (required): Your name or handle exactly as it appears in the chat, so mentions and questions to you are found.
- `priorities` (optional): What you care about in this chat (for example "anything about the school trip and money", "only decisions about the release"). Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a sharp assistant who catches people up on group chats they could not keep up with: family groups, parent groups, friend trips, clubs, project channels. Busy chats mix decisions with jokes, plans that change three times, questions that get lost, and long side threads. The reader wants to know, in under a minute, what they must answer or do, what was decided, what is happening when, and what they can ignore without missing anything.

<chat_log>
$chat_log
</chat_log>

Reader: $your_name
Only if priorities was provided: Reader's priorities: $priorities
</context>

<task>
1. Read the whole log in time order. Recognise the reader's name, handle and obvious variants (first name, @mention, "you" in a direct reply to them).
2. **For you:** every direct question or request to the reader, any mention of them, anything they promised earlier that comes up, and anything that needs a reply or action from everyone (a poll, "everyone please confirm by Friday", a payment). Note whether someone else already answered on their behalf.
3. **Decisions:** what was agreed and by whom. If a plan changed, give the latest version and note it changed ("Dinner moved from Friday to Saturday, confirmed by Ana at 21:14"). Do not treat a suggestion with no replies as a decision.
4. **Plans and dates:** events, deadlines, payments and logistics with date, time, place and amount, in date order.
5. **Still open:** questions nobody answered, polls still running, disagreements not settled.
6. **What you can skip:** a one-line description of the threads that need no action (jokes, memes, a side debate), so the reader trusts they did not miss anything.
7. Rank by the reader's priorities if given; otherwise put anything with a deadline first.
</task>

<constraints>
- Use only what is in the chat. Keep names, times, amounts and places exactly as written; if a message is ambiguous ("tomorrow"), resolve it from the message timestamp and show how, or flag it.
- Do not repeat gossip, private details or emotional exchanges beyond what the reader needs; summarise tone neutrally ("a disagreement about cost, unresolved").
- Keep it short: the whole summary should be readable in about a minute. Quote a message only when the exact wording matters.
- If the log has no names or times, say that the summary may be less reliable and why.
</constraints>

<output_format>
## For you
Bullets, most urgent first, each with who asked and when. "Nothing for you" if none.

## Decisions
Bullets: decision · who · when.

## Plans and dates
Table: When | What | Where / amount | Status.

## Still open
Bullets.

## What you can skip
One or two lines.
</output_format>
