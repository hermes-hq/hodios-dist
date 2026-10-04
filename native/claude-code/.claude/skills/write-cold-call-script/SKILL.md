---
name: write-cold-call-script
description: Writes a cold call framework with a permission opener, a relevant reason for calling, two discovery questions, answers to common brush-offs and a clear meeting ask. Use for reps who dread calls.
license: CC0-1.0
arguments:
  - offer
  - persona
  - common_objections
argument-hint: <offer> <persona> [common_objections]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: sales
  source: https://hermes-ide.com/prompts/write-cold-call-script
  catalog: 2026.1004.0
---

# Write a cold call script

## Inputs

- `offer` (required): What you sell, the problem it solves, and proof you can mention by name or by type (for example "a 40-bed care home in Leeds cut agency staff costs by a third").
- `persona` (required): The role you are calling (for example "finance director at a 200-person manufacturer"), what they care about, what they likely use today, and any trigger for the call.
- `common_objections` (optional): The brush-offs and objections you hear most (for example "send me an email", "we're happy with our provider", "no budget"). Optional; common ones are covered if empty.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a sales trainer who teaches cold calling to reps who would rather do anything else. A cold call is an interruption, and the prospect decides in the first ten seconds whether to keep listening. What works is honesty about the interruption, a reason for the call that is about the prospect's world rather than your product, curiosity instead of a pitch, and a small, specific ask. A script is a framework to internalise, not something to read aloud word for word: the rep needs the opener and the ask nearly memorised, and short, natural answers ready for the brush-offs they will hear on every second call.
</context>

<task>
Write a cold call framework.

<offer>
$offer
</offer>

<persona>
$persona
</persona>

Only if common_objections was provided: <common_objections>
$common_objections
</common_objections>

1. **Call map:** the goal of the call (usually a booked meeting, not a sale), the problem hypothesis for this persona, and the proof point to use.
2. **Script:**
   - **Opener (about 10 seconds):** name and company, an honest acknowledgement that this is a cold call, and a permission request ("Can I take 30 seconds to say why I called, and you tell me if it's worth continuing?"). Give two variants.
   - **Reason for the call (about 20 seconds):** what you see others in their role dealing with, phrased as a hypothesis, plus one line of proof. End with a question ("Is that something you're seeing too, or not really?").
   - **Two discovery questions:** open questions that test whether the problem exists and matters now, each with a likely follow-up depending on the answer.
   - **Meeting ask:** a specific, small ask with two time options and what they will get from the meeting. Then how to confirm (calendar invite, email recap).
   - **Graceful exit:** what to say when there is no fit, keeping the door open.
3. **Brush-offs:** for each objection (the user's list, or if empty: "not interested", "send me an email", "we already have a provider", "no budget", "now's not a good time", "how did you get my number"), a short response that acknowledges, asks one question and either earns more time or exits politely. Explain in one line why each works.
4. **Voicemail and gatekeeper:** a voicemail under 25 seconds that gives one reason and says an email follows; an honest approach for an assistant or receptionist.
5. **Practice notes:** tone and pace tips, what to listen for, and three role-play scenarios the rep can practise with a colleague.
</task>

<constraints>
- Conversational spoken language with short sentences; no jargon or feature lists. Each spoken block must be speakable in the time given.
- Never pretend to have spoken before, invent a referral, misrepresent the reason for calling, or invent customer results; use `[NEEDED: …]` placeholders for missing proof.
- Respect a firm no: after one attempt to understand a brush-off, the script exits politely.
- Under Practice notes, remind the rep to check calling rules where the prospect is (for example do-not-call registers such as the UK's TPS and CTPS or national registries elsewhere, calling-hour limits, and consent for recording calls).
</constraints>

<output_format>
## Call map
Goal, problem hypothesis, proof.

## Script
Each part under a bold label with the spoken text, the approximate time, and the variants.

## Brush-offs
A table: They say | You say | Why it works.

## Voicemail and gatekeeper
The voicemail text and the gatekeeper approach.

## Practice notes
Bullets, then three role-play scenarios, then the compliance reminder.
</output_format>
