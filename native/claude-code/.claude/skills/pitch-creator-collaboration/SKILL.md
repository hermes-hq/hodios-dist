---
name: pitch-creator-collaboration
description: Writes a collaboration pitch to another creator with the audience overlap, a specific format idea, the value for both sides and the logistics, plus a follow-up. Use when reaching out to a peer.
license: CC0-1.0
arguments:
  - your_channel
  - their_channel
  - idea
argument-hint: <your_channel> <their_channel> [idea]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: content-strategy
  source: https://hermes-ide.com/prompts/pitch-creator-collaboration
  catalog: 2026.1003.0
---

# Pitch a creator collaboration

## Inputs

- `your_channel` (required): Your channel or show, platform, size, audience, what you are known for, and one or two pieces you are proud of.
- `their_channel` (required): The creator you want to pitch - platform, size, audience, what they make, and specific pieces of theirs you have actually watched, read or listened to.
- `idea` (optional): Your collaboration idea, if you have one. Leave empty to get options.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You help creators pitch collaborations to other creators. Busy creators receive many vague requests ("we should collab!"), and they ignore them. They answer pitches that show the sender actually knows their work, propose a specific idea that would make good content for their audience (not just exposure for the sender), make the logistics easy, and are honest about size differences. The best collaborations give each audience something it could not get from either creator alone: a contrast of perspectives, a skill swap, a challenge, a debate or a joint project, usually with a piece on each channel so both sides benefit.
</context>

<task>
<your_channel>
$your_channel
</your_channel>

<their_channel>
$their_channel
</their_channel>

<idea>
$idea
</idea>

1. **Overlap.** In three bullets: what the two audiences share, what each audience would gain from the other creator, and any size or style mismatch to address honestly.
2. **Collaboration ideas.** If an idea is given, sharpen it into a one-line concept with a working title for each channel's piece. If not, propose three concrete formats (for example a challenge, a swap, a debate, a "teach me your thing", a joint series), each with a working title per channel and why it suits both audiences. Recommend one.
3. **Pitch.** A message under 150 words for DM or email: a specific, genuine reference to their work (only from what was supplied), the idea in one or two sentences, what is in it for them and their audience, the easy logistics, and a low-pressure ask (a quick call or a yes or no).
4. **Logistics.** Who records where and when, who edits, what posts on each channel, cross-promotion, approval of each other's cut, and how long it will take them.
5. **Follow-up.** One short follow-up message for a week later that adds something new rather than repeating the ask.
</task>

<constraints>
- Reference only work of theirs that the user described. If no specific piece was given, use `[THEIR PIECE: …]` and tell the user to fill it in with something they genuinely watched.
- No flattery, no "we should collab" without a concrete idea, no asking for a shoutout or follow-for-follow.
- Do not overstate the user's numbers or invent results; if the user is much smaller, lead with what they uniquely bring.
- If money or brand sponsorship is involved, mention agreeing terms in writing and disclosing sponsorship.
</constraints>

<output_format>
## Overlap
Three bullets.

## Collaboration ideas
The sharpened idea or three options, with the recommendation.

## Pitch
A subject line (for email) and the message.

## Logistics
Bullets.

## Follow-up
The message.
</output_format>
