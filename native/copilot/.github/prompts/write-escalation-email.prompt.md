---
description: Writes an escalation to a manager, vendor or another team that states the issue, its impact, what was already tried and the specific decision or help needed by a date, without blame.
agent: agent
argument-hint: issue history recipient
---

# Write an escalation email

<context>
An escalation asks someone with more authority or reach to unblock something you cannot unblock yourself. It works when the reader can act on it in two minutes: the ask and deadline are at the top, the impact is concrete, the history shows you made reasonable attempts, and the tone is factual rather than accusatory. It backfires when it is a complaint about a person, when it skips the people directly involved without warning them, when the ask is vague ("please help"), or when it arrives as a surprise to someone who will be embarrassed by it.
</context>

<task>
Write an escalation email.
Only if recipient was provided (leave it empty to skip): Recipient: ${input:recipient:Who you are escalating to, for example "my manager", "the vendor's account manager", "the head of the platform team", and your relationship with them.}

<issue>
${input:issue:What is blocked or going wrong, with the facts (what, since when, who is involved) and the impact on deadlines, money, customers or people.}
</issue>
Only if history was provided (leave it empty to skip): 
<history>
${input:history:What you have already tried, with dates, and the responses you got. Paste the key earlier messages if useful.}
</history>

1. If you cannot tell what is blocked, the impact, or what the recipient could do about it, ask up to three short questions and stop.
2. Check whether escalation is the right move now: has the direct owner been asked clearly, with a deadline, and told the matter would be escalated? If not, say so in "Check before escalating" and include a one-paragraph heads-up message to the direct owner first. Still write the escalation, ready for later.
3. Define the ask precisely: a decision (choose A or B), an action (assign an engineer, approve spend, call the vendor), or a priority call, with a date and the reason for that date.
4. Write the email:
   - Subject line: "[Decision/Help needed by date]: short issue".
   - First two lines: the ask, the deadline and the impact if nothing changes.
   - Context in three to five bullets: what is blocked, since when, impact in numbers where the facts allow, and who is affected.
   - What has been tried, as a short dated list, stated neutrally.
   - Options if helpful, with your recommendation.
   - A closing line offering a 15-minute call and stating what you will do in the meantime.
5. Recommend who to copy and who must be told before sending.
</task>

<constraints>
- Factual and neutral: describe actions and results, not people's character or motives. No sarcasm, no "per my last five emails".
- Use only facts from the input; mark missing figures or dates `[NEEDED: …]`.
- Keep the email under about 250 words; put long threads in an attachment or link, not in the body.
- For a vendor, refer to the contract or service level only if the input mentions it, and do not threaten legal action unless the user says that is the intent.
- If the issue involves harassment, discrimination, safety or a possible legal breach, say that the right channel may be HR, a safety officer or legal rather than a normal escalation.
</constraints>

<output_format>
## Check before escalating
Whether the direct owner has been given a fair chance, and the heads-up message if one is needed. "Ready to escalate" if so.
## Escalation email
Subject line and the email.
## Notes
Who to copy, who to tell first, `[NEEDED: …]` items, and when to follow up if there is no answer.
</output_format>
