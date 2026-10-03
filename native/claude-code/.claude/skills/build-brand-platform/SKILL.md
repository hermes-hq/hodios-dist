---
name: build-brand-platform
description: Defines a brand platform with purpose, mission, vision, values with behaviours, positioning, personality and promise, each tested for distinctiveness. Use when setting brand foundations.
license: CC0-1.0
arguments:
  - company
  - audience
argument-hint: <company> [audience]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: branding
  source: https://hermes-ide.com/prompts/build-brand-platform
  catalog: 2026.1003.2
---

# Build a brand platform

## Inputs

- `company` (required): What the company does, its business model, stage, competitors, what it does differently, what the founders or leaders believe, and any customer evidence (reviews, interviews, win and loss reasons).
- `audience` (optional): The customers the brand must win - who they are, the job they hire the product for, how they choose and what they use today. Optional but strongly improves the positioning.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Brand platforms tend to be interchangeable: a purpose about "empowering people", a mission to "deliver innovative solutions", values of integrity, passion and customer focus. Nobody can disagree with them, so they guide no decision. A useful platform is specific to this company and audience, every element rules something out, values come with the behaviours and trade-offs they imply, and the promise is one the business can keep today.
</context>

<task>
Build the brand platform.

<company>
$company
</company>
Only if audience was provided: 
<audience>
$audience
</audience>

1. **Inputs and gaps.** Summarise what you know and list what is missing. If there is no clear offer, customer or difference, ask up to four questions and stop. If there is no audience input, infer the audience, mark it as an assumption, and recommend customer interviews to confirm it.
2. **Purpose.** Why the company exists beyond making money, in one sentence that this company could credibly claim and its customers would care about. Give two options.
3. **Mission and vision.** Mission: what the company does now, for whom and how, in one sentence. Vision: the future state it is working towards, concrete enough that progress could be seen. Keep them distinct; a vision is not a bigger mission.
4. **Values.** Three or four values. For each: a name that is not a generic virtue unless it is made specific, a one-line meaning, two "we do" behaviours, one "we don't", and the trade-off it implies in a real decision (for example "we'll lose a deal rather than overpromise a delivery date"). Drop any value that implies no trade-off.
5. **Positioning.** For the target audience: the frame of reference (what category or alternative they compare it to), the point of difference that matters to how they choose, and the reasons to believe. Write it as: "For <audience> who <need>, <brand> is the <frame of reference> that <benefit>, because <reasons to believe>. Unlike <alternative>, <difference>."
6. **Personality.** Three or four traits as "X, not Y", each with how it shows up in words, visuals and service.
7. **Promise and proof.** The single promise every interaction must keep, the proof points that support it today, and the gaps between promise and current delivery that the business must close.
8. **Brand idea.** The platform compressed into two to five words that guide creative work, with two alternatives.
9. **Stress test.** Test the platform: could a named competitor say the same thing unchanged; is every claim true today; would an employee know what to do differently on Monday; does it fit the audience evidence. Revise any element that fails, and show what changed.
</task>

<constraints>
- Use only facts from the input. Do not invent customer insights, market data, competitor claims or proof points; mark assumptions as such.
- Ban empty words unless made specific by a behaviour: innovative, passionate, customer-centric, world-class, excellence, integrity.
- Write in plain sentences people inside the company could repeat without notes.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
Markdown with the contract's sections as `##` headings. Values as a table: | Value | Meaning | We do | We don't | Trade-off |. Close with "Brand platform on a page": all the chosen elements in under 200 words.
</output_format>
