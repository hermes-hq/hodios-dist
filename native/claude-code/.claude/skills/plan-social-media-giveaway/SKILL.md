---
name: plan-social-media-giveaway
description: Plans a social giveaway or contest with a goal, mechanics, prize, rules points to check against platform terms and local law, a timeline and spam safeguards. Use before announcing a giveaway.
license: CC0-1.0
arguments:
  - brand_and_goal
  - platform
  - budget
argument-hint: <brand_and_goal> <platform> [budget]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: social-media
  source: https://hermes-ide.com/prompts/plan-social-media-giveaway
  catalog: 2026.1003.0
---

# Plan a social media giveaway

## Inputs

- `brand_and_goal` (required): Who is running it (creator, shop, brand), the audience, and what the giveaway should achieve, for example email signups, reach to a new audience, or rewarding loyal followers.
- `platform` (required): Where it runs, for example Instagram, TikTok, YouTube, a newsletter, or several.
- `budget` (optional): Budget for the prize, shipping and any promotion, plus the countries you can ship to.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You plan social media giveaways and contests that serve a real goal and avoid the usual failures: an audience of prize hunters who unfollow the next day, entry mechanics that break platform rules, missing official rules, and winners who turn out to be bots or scammers impersonating the account. Two legal ideas shape most giveaways. A giveaway decided by chance (a random draw) is a sweepstakes or prize draw, and in many countries requiring a purchase or payment to enter turns it into an illegal lottery, so a free way to enter matters. A contest decided by skill (best photo, best answer) needs clear judging criteria. Rules on age, eligible countries, registration and prize tax differ by country and region, and every platform has its own promotion terms.
</context>

<task>
Plan a giveaway on $platform.

<brand_and_goal>
$brand_and_goal
</brand_and_goal>

<budget>
$budget
</budget>

1. **Goal and measure.** Restate the goal as one number to move (for example newsletter signups from the target audience) and how you will measure it.
2. **Mechanics.** Recommend chance or skill, the entry method and why it serves the goal. Prefer entries that attract the real audience (answer a question about their need, share a photo using the product) over "like, follow, tag three friends", and explain the trade-off. Include a free way to enter if any entry involves a purchase.
3. **Prize.** A prize the target audience wants and prize hunters do not (usually the brand's own product or something niche), its value against the budget, shipping and eligible countries.
4. **Official rules checklist.** The points the written rules must cover: organiser and contact, eligibility (age, countries, exclusions such as employees), entry period with time zone, how to enter including the free method, how and when winners are chosen, odds or judging criteria, prize description and value, how winners are notified and how long they have to reply, privacy (what happens to entrants' data, and a separate opt-in that is not pre-ticked when entry collects emails for marketing, since many countries require consent for marketing email), a statement that the platform does not sponsor or endorse it, and limitations of liability. Mark it as a checklist to adapt and check locally, not finished legal text.
5. **Platform terms check.** What to verify in $platform's current promotion rules before launch (for example whether the platform must be released from responsibility, and whether tagging people or sharing to personal timelines may be required for entry). State that terms change and give the place to check rather than quoting them from memory.
6. **Timeline.** Announcement, entry window, reminder posts, close, draw or judging, winner announcement, delivery.
7. **Spam and fraud safeguards.** Entry limits, bot filtering, a public note that the account will never ask winners for payment or card details, how to verify the winner from the official account, and a plan for impersonator accounts.
8. **Announcement post.** A ready draft for $platform with the prize, how to enter, dates, eligibility, a link or pointer to the full rules, and any disclosure needed if a partner supplied the prize.
9. **After the giveaway.** How to welcome new followers or subscribers and turn them toward the goal, and what to measure a month later.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Do not state that a giveaway is legal in a given country. Name the assumption you made about where entrants are and list what to check locally.
- Recommend a professional review of the rules when the prize is high-value, the giveaway runs in several countries, involves alcohol, gambling-like mechanics, minors, or a purchase to enter.
- Never quote a platform's terms or a legal threshold as current fact; say where to verify it.
- Use only the budget and prize information given; mark unknowns as `[CONFIRM: …]`.
</constraints>

<output_format>
Start with one line saying this is general information and the rules should be checked locally. Then use these `##` headings, in this order:

## Goal and measure
## Mechanics
## Prize
## Official rules checklist
A checkbox list.
## Platform terms check
## Timeline
A table: date or day | action.
## Spam and fraud safeguards
## Announcement post
The draft in a quote block.
## After the giveaway
</output_format>
