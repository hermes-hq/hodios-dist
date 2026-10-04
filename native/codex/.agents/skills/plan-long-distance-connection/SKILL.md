---
name: plan-long-distance-connection
description: Plans ways to stay close at a distance with a partner, family or grandchildren, with a call rhythm across time zones, rituals, shared activities, small surprises and a visit plan.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: relationships
  source: https://hermes-ide.com/prompts/plan-long-distance-connection
  catalog: 2026.1004.0
---

# Plan a long-distance connection

## Inputs

- [RELATIONSHIP] (required): Who you want to stay close to and why you are apart, for example "my partner, abroad for a 2-year job" or "grandparents and our kids aged 3 and 7". Add how you keep in touch now, what is not working, visit budget and any limits (shifts, hearing, tech skills).
- [TIME_ZONES] (optional): Where each person is, for example "London and Sydney" or "UTC-5 and UTC+1", plus usual waking and working hours if known. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You help people keep relationships strong across distance. What keeps people close is less the length of calls than their predictability and shared experience: a reliable rhythm, small everyday glimpses of each other's lives, doing things together rather than only reporting news, and something to look forward to. The right plan depends on who it is for. Partners need intimacy and a shared future; grandparents and young children need short, playful, routine contact with a parent's help; adult children need low-pressure contact that respects their independence.

<relationship>
[RELATIONSHIP]
</relationship>
Only if [TIME_ZONES] was provided: Time zones: [TIME_ZONES]
</context>

<task>
1. Your overlap: if time zones are given, work out the hours difference and the windows when both are awake and free, in both local times, noting that daylight saving changes can shift the difference by an hour at certain times of year. If not given, ask and explain how to find the overlap.
2. Call rhythm: a weekly table of contact (longer calls, short check-ins, asynchronous messages) that fits the overlap and everyone's routines, kept realistic and light enough to sustain.
3. Rituals: two to four recurring rituals suited to the relationship (for example a Sunday breakfast call, a goodnight voice note, reading the same bedtime story over video, a weekly photo of the same thing, a shared countdown).
4. Between calls: asynchronous ways to share daily life (voice and video notes, a shared photo album, letters and parcels, a shared list or journal), and small surprises.
5. Doing things together: activities to do at the same time remotely (watching a film in sync, cooking the same recipe, online games, a shared book, a walk while on the phone, a craft for grandparent and grandchild), with tips for young children's attention spans (short calls, a puppet, a game, show-and-tell, a parent on hand) and for anyone less confident with technology.
6. Visits: how often is realistic for the budget, how to plan them (alternating who travels, booking early, a mix of everyday time and special plans), and how to handle goodbyes and the post-visit dip, especially for children.
7. Check in on the plan: a short monthly question to ask each other ("What's working? What should we change?") and how to adjust when life gets busy or a time zone changes.
</task>

<constraints>
- Fit the plan to the relationship type and ages; do not apply partner advice to grandparents or vice versa.
- Do not name specific apps or products; describe the kind of tool (a video calling app, a shared photo album, a multiplayer word game).
- Be careful with time-zone maths: state the offsets you used and say to double-check around daylight-saving changes.
- Keep it light and kind; no guilt about missed calls. Contact is chosen by both people, never required or monitored. If the description suggests control or fear (constant location tracking, demands to prove where they are or who they are with, accusations over missed calls, being scared of the other person's reaction), lead with a short, gentle note that this is not a normal part of staying close and that confidential support such as a domestic-abuse or relationship helpline is available, without assuming; do not build the rhythm around those demands, and keep the rest of the plan brief.
- If key details are missing, give a plan with assumptions and list them.
</constraints>

<output_format>
## Your overlap
Table: Window | Their time | Your time.
## Call rhythm
Table: Day | Type | Length | Notes.
## Rituals
## Between calls
## Doing things together
## Visits
## Check in on the plan
</output_format>
