---
name: write-internal-announcement
description: Writes an internal announcement of a reorg, policy change or launch that explains what is changing, why, the impact on each group and where to ask, plus an FAQ and a pre-send check.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: business-writing
  source: https://hermes-ide.com/prompts/write-internal-announcement
  catalog: 2026.1003.0
---

# Write an internal announcement

## Inputs

- [CHANGE] (required): What is changing, when it takes effect, the real reason for it, who is affected and how, and what people need to do. Notes are fine.
- [AUDIENCE] (required): Who receives it, for example "whole company, 300 people" or "the support team and its managers".
- [TONE] (optional): Optional tone guidance such as "upbeat", "sober", "brief and factual". If empty, the tone is matched to the news.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
People read a change announcement asking four questions in order: what is changing, does it affect me, why, and what do I do now. Announcements fail when the change is buried under a preamble about values, when the reason is vague or spun ("to unlock synergies"), when they cheer about news that is bad for some readers, or when nobody knows where to ask. For changes that affect people's jobs, managers, roles or pay, the order of communication matters as much as the words: the people most affected should hear it directly, before a broadcast.
</context>

<task>
Write an announcement for [AUDIENCE] about this change:
<change>
[CHANGE]
</change>
Only if [TONE] was provided: Tone: [TONE].

1. If the input does not say what is changing or when, ask for that and stop.
2. Open with a subject line or headline that states the change itself, and a first paragraph that says what is changing and when it takes effect.
3. Explain why, using the actual reason from the input. If no reason is given, insert `[need: the reason]` rather than writing a generic one.
4. Explain the impact by group: who is affected and how, and say explicitly what is not changing.
5. List what readers need to do, with deadlines. If nothing, say "No action needed".
6. Say where to ask: a named channel, person, session or form from the input, or `[need: where to ask]`.
7. Match the tone to the news. A launch can be upbeat. A reorg, a cut or a policy that removes a benefit is plain and respectful: acknowledge that it is a real change for some people, without corporate euphemism and without over-apologising.
8. Draft an FAQ of five to eight questions readers will actually ask, including the uncomfortable ones (Is this a cost cut? Will there be more changes? What happens to my role?). Answer only from the input; where the answer is unknown, write the honest holding answer ("We don't know yet; we will tell you by [date]").
</task>

<constraints>
- Never invent reasons, numbers, dates, names or commitments.
- No euphemisms that hide what is happening ("rightsizing", "transitioning roles"). Say "roles will be eliminated" if that is the fact.
- Do not mention any individual's performance, health or personal circumstances.
- Keep the announcement under 350 words; detail goes in the FAQ.
- If the change involves job losses, pay or contract changes, or anything with legal implications, add to Before you send that HR or legal should review it, and that affected people must be told directly first.
</constraints>

<output_format>
## Announcement
Subject line, then the message with short sections: What is changing · Why · What it means for you · What you need to do · Questions.
## FAQ
Numbered questions with short answers.
## Before you send
A checklist: who must hear before this goes out, any `[need: …]` placeholders, reviews required, and the best channel and timing.
</output_format>
