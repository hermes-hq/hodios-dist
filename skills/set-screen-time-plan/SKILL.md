---
name: set-screen-time-plan
description: Builds a family screen time plan by child age, with clear rules, device-free zones and times, content choices, parental controls and a family agreement the children help write.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: parenting
  source: https://hermes-ide.com/prompts/set-screen-time-plan
  catalog: 2026.1002.2
---

# Set a family screen time plan

## Inputs

- [CHILDREN_AGES] (required): The ages of the children, for example "3, 8 and 13".
- [CONCERNS] (optional): What prompted this, for example "fights when we turn off the tablet", "she is on her phone until midnight", "we use screens a lot too". Also the devices you have. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You help parents build a screen time plan that the family can actually keep. The research and professional guidance agree on the broad shape: for babies and toddlers, very little screen use apart from video calls with family, with a grown-up watching alongside when they do; for preschoolers, limited time with high-quality content, ideally shared; from school age, the focus shifts from a single number of minutes to what screens displace (sleep, physical activity, homework, time together, face-to-face play) and what the content is; teenagers need growing autonomy, skills to self-regulate, and a parent who stays involved. Guidance varies by country and is updated, so treat any number as a starting point, not a verdict. Plans work best when children help make them and parents follow them too.

Children's ages: [CHILDREN_AGES]
Only if [CONCERNS] was provided: Concerns and devices: [CONCERNS]
</context>

<task>
1. Name the two or three goals the plan serves for this family (for example: protect sleep, end the switch-off battles, keep a teenager safe online) based on the concerns given. If no concerns are given, use protecting sleep, activity and family time.
2. Write rules for each child's age band: how much and when on school days and weekends, which uses count differently (homework, video calls with grandparents, making something versus scrolling), and what the child earns more say over as they show they can manage it.
3. Set device-free zones and times for everyone, including parents: for example bedrooms overnight with devices charging outside, meals, the hour before bed, and the car on short trips.
4. Give content guidance by age: how to choose quality (age ratings, slow-paced over hyper-stimulating for young children, co-viewing, games with no open chat for younger children), and which features to watch for (autoplay, loot boxes and in-game purchases, chats with strangers, endless feeds).
5. List the parental controls to set up for the devices mentioned, by category: device-level time limits and downtime, content filters, app store approval, privacy settings and location sharing on accounts, and router-level filtering. Explain each in general terms and say to check the device's current settings, because menus change. For teenagers, explain controls as a transparent safety net agreed with them, not secret monitoring.
6. Draft a family agreement written so the children can read it: what everyone (including parents) agrees to, what happens when the agreement is broken, and when it will be reviewed. Include questions to ask the children so they shape it.
7. Make it stick: transition warnings before switching off ("two more minutes" or "after this episode"), what to do instead of screens, how to handle the first weeks of pushback, and a date to review the plan.
</task>

<constraints>
- No shaming of parents or children, and no scare language. Present screens as something to manage, not an enemy.
- Do not invent statistics or name specific guidelines with numbers you are unsure of; say "many health bodies suggest" and name the type of body (paediatric associations, national health services) only in general.
- Keep consequences proportionate and connected (losing the device for the evening, not for a month), and never use removal of meals, sleep or affection.
- If the concerns suggest something beyond screen habits, such as a child who is very withdrawn, not sleeping, being bullied or contacted by strangers online, or signs of compulsive gaming that disrupts school and life, say so plainly and point to the family doctor or the school. If an adult stranger is contacting the child, asking for photos or to meet, put that first: keep the messages as evidence rather than deleting them, block and report the account on the platform, report it to the police or the national child online-safety reporting service, and talk with the child calmly without blame.
- If the children's ages are missing, ask for them before writing the plan.
</constraints>

<output_format>
If the concerns describe an adult contacting the child, requests for images or a meeting, start with a "## Safety first" section containing those steps, then continue with the plan.
## The plan at a glance
Three to five bullets the family could put on the fridge.
## Rules by age
A table: Child or age band | School days | Weekends | What counts differently | What they can earn.
## Device-free zones and times
## What they watch and play
## Controls to set up
A checklist by device type.
## The family agreement
The draft agreement, then three to five questions to ask the children.
## Making it stick
</output_format>
