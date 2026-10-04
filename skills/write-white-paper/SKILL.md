---
name: write-white-paper
description: Writes a B2B white paper that frames an industry problem with cited evidence and sets out a solution approach, citing a supplied source for every factual claim and flagging unsupported ones.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: business-writing
  source: https://hermes-ide.com/prompts/write-white-paper
  catalog: 2026.1004.2
---

# Write a white paper

## Inputs

- [TOPIC] (required): The problem the paper addresses, your organisation's point of view or approach to it, and what you want readers to do after reading.
- [EVIDENCE] (required): Your sources: statistics, studies, customer results, expert quotes and internal data, each with where it comes from (publisher, title, year, link or 'internal data, 2025'). The paper will cite only these.
- [AUDIENCE] (optional): Who reads it, for example "IT directors at mid-size hospitals evaluating patient-data platforms", including what they already know and what they are sceptical of.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A white paper earns trust by teaching before it sells. Its readers are evaluators, often sceptical specialists building a case internally, who will forward it only if it is accurate, specific and fair. White papers fail when they are brochures with footnotes: vague market claims, statistics without sources, a "solution" section that is just the product, and no acknowledgement of trade-offs or alternatives. The structure that works is problem, cost of the problem, why common approaches fall short, a principled approach (criteria a good solution must meet), how to apply it, and a short, honest note on how the author's organisation fits.
</context>

<task>
Write a white paper on:
<topic>
[TOPIC]
</topic>

Evidence you may cite (and nothing else):
<evidence>
[EVIDENCE]
</evidence>
Only if [AUDIENCE] was provided: 
Audience: [AUDIENCE]

1. If the evidence has fewer than three usable sourced items, or the sources are not identified, ask for more or for their origins and stop.
2. Identify the reader's core question and the paper's thesis in one sentence each. If no audience was given, infer the most likely evaluating reader from the topic, state that assumption above the paper, and pitch the depth to them.
3. Outline before writing: title, executive summary, the problem, its cost or consequences, why current approaches fall short, the recommended approach as a set of principles or criteria, implementation steps or a maturity path, a short section on the author's offering if the topic mentions one, and a conclusion with a next step.
4. Write the paper at 1,500 to 2,500 words, in confident, plain, specific prose for this audience. Use subheadings that state the point, short paragraphs, and a table or numbered list where it clarifies a comparison or process. Suggest one or two figures (what they show and which source they use).
5. Cite every factual claim (number, trend, study finding, quote, customer result) inline with a numbered reference [1] that maps to the evidence, and list references at the end in a consistent format. Any sentence that states a fact but has no source in the evidence must be rewritten as an opinion, removed, or marked `[SOURCE NEEDED]`.
6. Keep the solution vendor-neutral until the dedicated section; the principles should be useful even to a reader who never buys.
</task>

<constraints>
- Never invent statistics, studies, quotes, customer names or results, and never attribute a claim to a source that does not support it. Do not upgrade a claim beyond its source ("a survey of 200 firms" does not become "the industry").
- Distinguish clearly between evidence, the author's interpretation and recommendations.
- Acknowledge at least one limitation, trade-off or situation where the approach does not fit.
- Avoid hype words (revolutionary, game-changing, best-in-class, seamless) and unexplained jargon.
- Internal data is allowed but must be labelled as such, with its sample and period if given.
</constraints>

<output_format>
## White paper
Title, subtitle, executive summary (about 150 words), then the sections with stated-point subheadings, conclusion and next step, and a References list numbered to match the in-text citations.
## Claim and source check
A table: Claim (short) | Reference | Exact supporting detail from the evidence. Include every factual claim.
## Gaps
Each `[SOURCE NEEDED]` and any evidence that would strengthen a weak section. "None" if none.
## Repurposing notes
Three short ideas for reuse (a blog post, a slide, a sales email line), each pointing to the section it comes from.
</output_format>
