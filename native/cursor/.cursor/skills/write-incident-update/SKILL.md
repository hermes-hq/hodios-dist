---
name: write-incident-update
description: Writes a clear status update for an ongoing incident, tuned to customers, internal teams or executives, without speculation or promises the team cannot keep. Use for status pages, Slack and email.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: incident
  source: https://hermes-ide.com/prompts/write-incident-update
  catalog: 2026.1002.1
---

# Write an incident status update

## Inputs

- [FACTS] (required): What is known right now. Symptoms, affected features or regions, start time, what the team is doing, and any workaround.
- [AUDIENCE] (optional; one of: customers, internal, executives; default: customers): Who will read it.
- [PHASE] (optional; one of: investigating, identified, monitoring, resolved; default: investigating): Where the incident stands.
- [NEXT_UPDATE] (optional): When the next update will come, for example "in 30 minutes" or "by 16:00 UTC".

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
During an incident, people judge the team by its updates as much as by the fix. Good updates are early, specific about who is affected, honest about what is not yet known, and regular. Bad ones guess at causes, promise times the team cannot meet, or hide behind jargon, and each of those costs trust that is hard to win back.
</context>

<task>
Write a [PHASE] update for [AUDIENCE] from these facts:
[FACTS]
Only if [NEXT_UPDATE] was provided: Next update: [NEXT_UPDATE]

1. Lead with the impact in the reader's terms: what they cannot do, since when (UTC), and who is affected. Say what still works when the facts show it.
2. Say what the team is doing now, matching the phase: investigating (looking into it), identified (cause found, fix under way), monitoring (fix applied, watching), resolved (back to normal, with the time and a pointer to a follow-up review if one is planned).
3. Include a workaround only if the facts contain one.
4. End with when the next update will come. If no time was given and the phase is not resolved, add `[next update time]` for the author to fill in.
5. Tune it to the audience:
   - customers: plain language, no internal system names, at most 120 words.
   - internal: the affected services, the incident channel or commander if given, what other teams should and should not do, at most 150 words.
   - executives: business impact first (customers, revenue, SLA, regulatory exposure if the facts mention it), the decision or support needed from them if any, at most 100 words.
</task>

<constraints>
- Use only the facts given. Never guess a cause, a number of affected users or a resolution time.
- Do not blame a vendor, a team or a person.
- Do not promise a fix time unless the facts contain one the team has committed to.
- Do not apologise more than once, and do not use filler such as "we take this very seriously".
- Times in UTC. No emoji.
</constraints>

<output_format>
## Title
One line, for a status page or subject line, stating the affected feature and the phase.

## Update
The message, ready to paste.

## Held back
Bullets: facts from the input you left out for this audience and why, plus any placeholder the author must fill. "Nothing" if empty.
</output_format>
