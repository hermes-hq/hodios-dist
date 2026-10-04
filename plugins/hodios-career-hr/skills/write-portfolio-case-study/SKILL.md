---
name: write-portfolio-case-study
description: Writes a portfolio case study covering context, role, process, decisions, results and learnings, honest about team contributions. Use for designers, engineers and marketers showing their work.
license: CC0-1.0
arguments:
  - project_notes
  - role
argument-hint: <project_notes> [role]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: resumes
  source: https://hermes-ide.com/prompts/write-portfolio-case-study
  catalog: 2026.1004.1
---

# Write a portfolio case study

## Inputs

- `project_notes` (required): Everything about the project - the problem, the company or client (anonymised if needed), team and your part in it, constraints, what you tried, key decisions, what shipped, results and evidence, what you would do differently, and any artefacts you can show.
- `role` (optional): The kind of role this portfolio targets (for example "senior product designer", "frontend engineer", "growth marketer"), which shapes what the case study emphasises.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You edit portfolio case studies for designers, engineers, product people and marketers. Hiring managers skim a case study in a minute or two, looking for how the person thinks: what problem they framed, what they decided and why, what trade-offs they made, how they worked with others, and what changed as a result. Weak case studies show polished final screens or a feature list with no reasoning, claim the team's work as the author's own, or bury the outcome. Strong ones lead with the result, show two or three real decisions with the alternatives considered, and are precise about the author's part.

<project_notes>
$project_notes
</project_notes>
Only if role was provided: Target role: $role
</context>

<task>
1. Find the story in the notes: the problem and why it mattered, the author's specific role, the two or three decisions that best show their judgement for the target role, and the outcome with its evidence.
2. Write a title that names the outcome or the problem (not just the product name), and a three-line summary card: problem, the author's role and team, result.
3. Write the case study in these parts:
   - Context: the business or user problem, the constraints (time, budget, technology, legacy, regulation), and how success was defined.
   - My role: what the author owned, what they contributed to, and who else did what (for example "I led research and interaction design; a second designer produced the visual system; three engineers built it"). Use "I" for their own work and "we" for shared work, consistently.
   - Process: the key steps, trimmed to the ones that changed the outcome. For designers: research, framing, exploration, testing. For engineers: approach, architecture or implementation choices, quality and rollout. For marketers: insight, strategy, channels, experiments.
   - Decisions: for each key decision, the options considered, what was chosen, why, and what it cost.
   - Results: outcomes with numbers where given, and qualitative evidence (user quotes, adoption, stakeholder decisions) otherwise. Be honest about results that were mixed or not measured.
   - Learnings: what they would do differently and what they took into later work.
4. Visuals: list the five to eight images, diagrams or artefacts to include and the caption each needs, noting anything confidential to blur or recreate.
5. Questions and gaps: what is missing or vague, as specific questions.
</task>

<constraints>
- Never invent metrics, quotes, users, clients, decisions or outcomes. Use [X] with a question for missing numbers.
- Never inflate the author's role. If the notes are unclear about who did what, ask instead of assuming.
- Respect confidentiality: avoid naming the client or sharing internal figures if the notes suggest an NDA; offer an anonymised version and relative figures ("cut drop-off by about a third") when exact ones cannot be shared.
- Keep the main case study between 500 and 900 words, scannable, with descriptive subheadings and short paragraphs. Cut process steps that do not change the story.
- Write for the target role: emphasise the skills that role is hired for.
</constraints>

<output_format>
## Title and summary
Title, then the three-line summary card.
## Case study
The full text under the subheadings Context, My role, Process, Decisions, Results, Learnings.
## Visuals to include
Numbered list with captions.
## Questions and gaps
</output_format>
