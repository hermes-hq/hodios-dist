---
description: Writes a clear status update for an ongoing incident, tuned to customers, internal teams or executives, without speculation or promises the team cannot keep. Use for status pages, Slack and email.
agent: agent
argument-hint: facts audience phase next_update
---

# Write an incident status update

<context>
During an incident, people judge the team by its updates as much as by the fix. Good updates are early, specific about who is affected, honest about what is not yet known, and regular. Bad ones guess at causes, blame a vendor, promise times the team cannot meet, hide behind jargon or go silent for an hour, and each of those costs trust that is hard to win back. Updates are written under time pressure, so draft immediately instead of asking questions.
</context>

<task>
Write a ${input:phase:Where the incident stands.} update for ${input:audience:Who will read it.} from these facts:
${input:facts:What is known right now. Symptoms, affected features or regions, start time with timezone, what the team is doing, any workaround, and the time now.}
Only if next_update was provided (leave it empty to skip): Next update: ${input:next_update:When the next update will come, for example "in 30 minutes" or "by 16:00 UTC".}

1. Lead with the impact in the reader's terms: what they cannot do, since when (UTC), and who is affected. Say what still works when the facts show it.
2. Say what the team is doing now, matching the phase: investigating (looking into it), identified (cause found, fix under way; describe the cause only in general terms and only if the facts confirm it), monitoring (fix applied, watching, what users may still see), resolved (back to normal, the duration with start and end times, anything users need to do, and a pointer to a follow-up review if one is planned).
3. Include a workaround only if the facts contain one.
4. End with when the next update will come. If no time was given and the phase is not resolved, use 30 minutes after the current time for investigating and identified, and 60 minutes for monitoring; if the current time is not in the facts either, add `[next update time]` for the author to fill in.
5. If a must-have fact is missing (what is affected, or since when), still write the draft, insert `[CONFIRM: what is needed]` at that spot, and list it under Held back.
6. Tune it to the audience:
   - customers: plain language, no internal system names, at most 120 words.
   - internal: the affected services, the incident channel or commander if given, the customer impact in numbers if known, what other teams should and should not do, and a suggested line for support to give customers, at most 150 words.
   - executives: business impact first (customers, revenue, SLA, regulatory exposure if the facts mention it), the decision or support needed from them if any, at most 100 words.
</task>

<constraints>
- Use only the facts given. Never guess a cause, a number of affected users or a resolution time.
- Do not blame a vendor, a team or a person.
- Do not promise a fix time unless the facts contain one the team has committed to.
- Do not apologise more than once, and do not use filler such as "we take this very seriously".
- Times in UTC unless the facts use another timezone. No emoji, no exclamation marks, no marketing language.
</constraints>

<output_format>
## Title
One line, for a status page or subject line, stating the affected feature and the phase.

## Update
The message, ready to paste.

## Short version
Under 280 characters, for an in-app banner or social post.

## Held back
Bullets: facts from the input you left out for this audience and why, plus every `[CONFIRM]` or other placeholder the author must fill before posting. "Nothing" if empty.
</output_format>
