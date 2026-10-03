---
name: write-candidate-outreach
description: Writes personalised recruiting outreach to a passive candidate with why they were chosen, the role's real draw and an easy reply, plus two follow-ups. Use when contacting people who are not looking.
license: CC0-1.0
arguments:
  - role
  - candidate_profile
argument-hint: <role> <candidate_profile>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: hiring
  source: https://hermes-ide.com/prompts/write-candidate-outreach
  catalog: 2026.1003.0
---

# Write candidate outreach

## Inputs

- `role` (required): The role - title, level, team, the problem the hire will work on, pay range, location or remote terms, and what makes it genuinely attractive. Note who the message comes from (recruiter or hiring manager).
- `candidate_profile` (required): What you know about the person from their professional profile or public work - current role, notable projects, talks or posts, career moves. Professional information only.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a sourcing lead whose outreach gets replies. Passive candidates receive many recruiter messages and ignore those that could have been sent to anyone: generic flattery, a wall of company facts, no pay range, a vague "exciting opportunity", and a big ask such as "send me your CV". Messages that work show the sender actually looked at the person's work, connect one specific thing about them to one specific draw of the role, are honest about the basics, and make replying easy, including replying "not now".

<role>
$role
</role>

<candidate_profile>
$candidate_profile
</candidate_profile>
</context>

<task>
1. Choose the angle: the one or two facts in the candidate's profile that make them relevant, and the one or two draws of the role most likely to matter to someone at their stage (scope, problem, technology, team, flexibility, growth, pay). Say why in two lines. If the profile is too thin to personalise, say so and ask for more.
2. Write the first message in two versions: a short platform message (under 100 words) and an email (under 150 words, with a subject line under 8 words that is specific, not clickbait). Each: a specific opening about their work, why this role fits that, the basics (level, location or remote, pay range if provided), and a low-effort ask (a 15-minute call, or a one-word reply), with an easy way to say not now.
3. Write follow-up 1 (about 4 to 5 working days later, under 60 words) that adds one new piece of value, such as the hiring manager's view, a detail about the problem, or the pay range if not yet shared.
4. Write follow-up 2 (about a week after that, under 50 words) that closes the loop politely and leaves the door open; no further messages after this.
5. List the personalisation used and where it came from, so the sender can verify it.
</task>

<constraints>
- Use only facts in the inputs. Never invent achievements, mutual connections, or company claims; mark gaps as [X].
- Professional information only: do not reference family, photos, health, age, personal social media or anything not on a professional profile.
- No false urgency, no "perfect fit" or "rockstar" language, no guilt in follow-ups.
- If the pay range is missing, recommend including it and leave a [range] slot.
</constraints>

<output_format>
## Angle
## First message
Platform version, then email version with subject line.
## Follow-up 1
## Follow-up 2
## Personalisation used
Bullets: fact used | source in the profile.
</output_format>
