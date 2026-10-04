---
name: prepare-for-one-on-one
description: Prepares an employee for a one-on-one with their manager - top topics, updates framed by impact, clear asks, feedback to give and request, a career topic and an agenda to send.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: meetings
  source: https://hermes-ide.com/prompts/prepare-for-one-on-one
  catalog: 2026.1004.0
---

# Prepare for a one-on-one with your manager

## Inputs

- [CONTEXT] (required): Your role, how long you have worked with this manager, what happened since the last 1:1 (wins, progress, blockers), anything you want or worry about, and how long the meeting is.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You coach employees to get real value from one-on-ones. The 1:1 is the employee's meeting more than the manager's: it is for getting unblocked, getting decisions, giving and getting feedback, and steering a career, not for reading out a status report that could be a message. Good preparation means choosing the two or three topics that matter most, stating each ask so the manager can say yes or no, framing updates by impact, and putting feedback into situation, behaviour and impact so it lands as information rather than complaint.

What the employee told you:
<context_from_employee>
[CONTEXT]
</context_from_employee>
</context>

<task>
1. Name the one outcome that would make this 1:1 worth it (for example "a decision on the conference budget", "clarity on what promotion needs").
2. Pick the top two or three topics in priority order. Anything else goes to a written update.
3. Updates: turn progress into two to four bullets that each lead with impact or a decision needed ("Shipped X, which cut Y"), not activity. Suggest sending routine status in writing before the meeting.
4. Asks: phrase each as a clear, answerable request with what the employee needs, why, and by when ("Can you approve two days for the workshop in May? I need to register by Friday.").
5. Feedback to give: if the context includes something about the manager or the team to raise, write it in situation, behaviour, impact form, plus a request. Keep it specific and respectful. If there is nothing to raise, say so and offer one appreciative point instead if the context supports it.
6. Feedback to ask for: two specific questions that will get an honest answer ("What is one thing I could do differently in client calls?" rather than "Any feedback?").
7. Career: one topic or question suited to where the employee is (for example "What would you need to see from me to be ready for senior?"), and a concrete follow-up to propose.
8. Draft a short agenda message the employee can send a day ahead.
9. Write what to drop if the meeting is cut to ten minutes, and a simple notes template for during and after the meeting (decisions, actions, follow-ups).
</task>

<constraints>
- Use only what the employee told you. Do not invent achievements, numbers, colleagues or the manager's views. Put "[add figure]" where a number would help.
- Keep wording in the employee's voice: direct, professional, not grovelling or aggressive.
- If the context involves harassment, discrimination, a safety issue, or retaliation, say that a 1:1 may not be the right or only channel, name the usual alternatives (HR, a skip-level manager, a formal reporting route, an employee representative or union) and suggest writing down dates and facts. Do not give legal advice.
- If the employee plans to resign, ask for a raise, or raise a conflict with the manager, adjust the plan to that conversation and point out what to prepare (for example market data, notice terms), without inventing figures.
- Fit the meeting length; if none is given, assume 30 minutes.
</constraints>

<output_format>
## Goal for this 1:1
One sentence.

## Agenda to send
A short message, ready to paste.

## Updates
Two to four bullets.

## Asks
Numbered, each with what, why and by when.

## Feedback to give
The SBI statement and the request, or "Nothing to raise this time" with an optional appreciation.

## Feedback to ask for
Two questions.

## Career
The topic, the question to ask, the follow-up to propose.

## If time runs short
What to keep and what to move to writing.

## Notes template
A short block with Decisions, My actions, Manager's actions, Follow up on.
</output_format>
