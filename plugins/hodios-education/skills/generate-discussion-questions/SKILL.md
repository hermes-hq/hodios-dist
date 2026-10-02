---
name: generate-discussion-questions
description: Writes sequenced discussion questions for a text or topic across Bloom's levels, with probes and likely student responses. Use when preparing a seminar or class discussion.
license: CC0-1.0
arguments:
  - text_or_topic
  - grade_level
  - count
argument-hint: <text_or_topic> [grade_level] [count]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: teaching
  source: https://hermes-ide.com/prompts/generate-discussion-questions
  catalog: 2026.1002.1
---

# Generate discussion questions

## Inputs

- `text_or_topic` (required): The text (paste it or name a widely known work with the chapter) or the topic to discuss.
- `grade_level` (optional): Optional grade or audience, e.g. "Grade 8", "AP Literature", "adult book club".
- `count` (optional; default: 10): Number of main questions.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Good discussion questions have more than one defensible answer, send students back to the text for evidence, and build on each other. Weak ones are quiz questions in disguise ("What colour was the car?") or so open that nobody knows where to start ("What did you think?"). The teacher also needs the follow-ups: what to ask when the answer is thin, when a student is right for the wrong reason, or when the room goes quiet.
</context>

<task>
Write $count discussion questions on the text or topic belowOnly if grade_level was provided:  for $grade_level.

<text_or_topic>
$text_or_topic
</text_or_topic>

1. Identify the 3 or 4 central ideas, tensions or choices in the material worth discussing.
2. Spread the questions across Bloom's levels, weighted toward the higher ones: about 20% remember and understand (to establish shared ground), 30% apply and analyse, 50% evaluate and create.
3. Sequence them as a discussion would flow: an accessible opener, then deeper questions that build on earlier answers, then a closing question that connects to students' lives or a larger issue.
4. For a text, make most questions text-dependent: they require citing a passage, a line or a detail as evidence.
5. For each question, add:
   - Two follow-up prompts: one to probe ("What in the text makes you say that?") and one to push or complicate ("How would someone who disagrees respond?").
   - One likely student response or misconception, so the teacher can prepare.
</task>

<constraints>
- Higher-level questions must have more than one defensible answer; do not hide a single expected answer in an "evaluate" question.
- If you are asked about a specific text you do not know well enough to quote or reference accurately, say so and ask for the text or the passage. Never invent quotations, page numbers or plot details.
- Keep vocabulary and themes appropriate for the grade level. For sensitive material, add a facilitation note on how to keep the discussion safe and respectful.
</constraints>

<output_format>
## Questions
Numbered in discussion order. Each item:
**Question** (Bloom level)
- Probe: …
- Push: …
- Likely response: …

## Facilitation notes
3 to 5 bullets: which questions to use if time is short, a good structure (pairs first, then whole class), and norms for sensitive moments if relevant.
</output_format>
