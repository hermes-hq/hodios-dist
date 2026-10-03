---
name: write-card-message
description: Writes a short, specific card message for a birthday, wedding, graduation, new baby, retirement or get-well card that sounds like the sender rather than a greeting card.
license: CC0-1.0
arguments:
  - occasion
  - relationship_and_details
  - tone
argument-hint: <occasion> <relationship_and_details> [tone]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: interpersonal-communication
  source: https://hermes-ide.com/prompts/write-card-message
  catalog: 2026.1003.2
---

# Write a card message

## Inputs

- `occasion` (required): The occasion, for example "40th birthday", "wedding", "PhD graduation", "new baby", "retirement after 30 years" or "get well after knee surgery".
- `relationship_and_details` (required): Who the card is for, how you know them, who is signing, and one or two specifics (a shared memory, something they love, what is next for them, an inside joke).
- `tone` (optional; one of: heartfelt, funny, formal, brief; default: heartfelt): The feel of the message. brief means one or two lines for a shared office card or a gift tag.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Card messages fail in two ways: they are generic ("Wishing you all the best on your special day!") or they try too hard and run to a paragraph that will not fit the card. What makes a card worth keeping is one true, specific detail that only this sender could write, said in the sender's own voice, in about the space a card allows. The occasion sets the conventions: a wedding card looks forward to the marriage, a retirement card honours the work and the person outside it, a get-well card offers warmth without predicting recovery, a new-baby card is about the parents as much as the baby.
</context>

<task>
Write a card message.

Occasion: $occasion
Tone: $tone
<relationship_and_details>
$relationship_and_details
</relationship_and_details>

1. If the details give no concrete specific (no memory, trait, plan or shared reference), ask up to two short questions that would supply one, then also give one usable version with a single `[bracketed]` slot to fill in, and stop.
2. Pick the one or two details that will mean the most to the recipient. Do not try to use everything.
3. Write three options that differ in approach, not just wording: for example one built around a memory, one around who they are, one around what comes next.
4. Suggest a sign-off that fits the relationship, and say whether a shared card from a group needs a different line.
</task>

<constraints>
- Length: heartfelt and funny about 25 to 60 words; formal about 20 to 45 words; brief at most 20 words. Every option must fit inside a standard folded card.
- Match the sender's register from how they wrote the details: if they write casually, the card is casual. Use contractions unless the tone is formal.
- Use only facts from the details. Do not invent memories, names, ages, achievements or jokes the sender did not mention.
- Avoid stock phrases: "special day", "on this joyous occasion", "words cannot express", "you deserve it all", "another trip around the sun", "here's to many more" (unless reworked into something specific).
- Funny means warm teasing the recipient would enjoy reading aloud. No jokes about age, weight, looks, fertility, the marriage failing, or sleepless-nights clichés unless the sender's details show that exact joke is theirs.
- Get-well: no predictions ("you'll be back to normal in no time"), no "everything happens for a reason", no medical advice. Offer company or practical help only if the sender suggested it.
- Retirement: honour the work and the person; no jokes about being old or useless.
- If the occasion is a death, loss or sympathy card, do not use this celebratory approach: say that a condolence message follows different rules, write one short, plain message that names the person who died if given and offers support without platitudes, and suggest a dedicated condolence prompt for more options.
</constraints>

<output_format>
## Options
Three numbered messages, each ready to copy into the card, with a three-to-six-word label for its approach in italics above it.
## Sign-off
One or two closing lines and signatures to choose from.
## Notes
One line on which option you would pick for this person and why. Add a line for any detail you left out on purpose.
</output_format>
