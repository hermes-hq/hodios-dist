---
name: build-user-journey-map
description: Builds an evidence-based journey map with stages, actions, thoughts, emotions, pain points and opportunities, marking every assumption. Use after interviews or studies about one segment.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: ux-research
  source: https://hermes-ide.com/prompts/build-user-journey-map
  catalog: 2026.1004.2
---

# Build a user journey map from research

## Inputs

- [PERSONA_OR_SEGMENT] (required): The one persona or segment the map is for, e.g. "first-time landlords renting out one flat".
- [RESEARCH] (required): Interview notes, transcripts, survey verbatims, support tickets or analytics findings about this segment. Label sources where possible (I3, ticket 1182).

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Most journey maps are workshop guesses dressed up as research: tidy stages named after the company's funnel, emotions drawn as a smooth wave nobody measured, and pain points nobody can trace to a person. A useful map follows one segment through one scenario in their own terms, says where each cell came from, and ends in opportunities specific enough to act on.
</context>

<task>
Build a journey map for **[PERSONA_OR_SEGMENT]** from this research:

<research>
[RESEARCH]
</research>

1. Define the scope: the scenario and goal the journey covers, where it starts (the trigger) and where it ends (goal met or abandoned). If the research covers several scenarios, pick the best-evidenced one and list the others.
2. Name 4 to 7 stages from the person's point of view ("Realising the boiler is broken", not "Awareness"). Stages can happen outside the product.
3. For each stage, fill these lanes:
   - **Doing:** actions and steps;
   - **Touchpoints:** channels, people and tools involved, including ones the company does not own;
   - **Thinking:** questions and thoughts, as verbatim quotes where the research has them;
   - **Feeling:** an emotion score from -2 to +2 with the emotion named and the evidence for it;
   - **Pain points:** what goes wrong, and why;
   - **Opportunities:** what could change.
4. Tag every cell with its source (I3, ticket 1182, survey) or "assumption". Do not fill a cell from imagination without that tag; leave it "no data" if nothing supports it.
5. Mark the moments that matter most: where people abandon, where emotion drops lowest, and where a single good experience changes the outcome.
6. Turn the top pain points into 3 to 6 "How might we..." opportunity statements, ranked by severity and by how often the research shows them, each linked to the stage and evidence.
7. If the research is too thin for a credible map (for example one interview or only opinions about features), say so and either produce a clearly labelled hypothesis map with the research needed to validate it, or ask for more material.
</task>

<constraints>
- One persona or segment and one scenario per map. If the research mixes segments whose journeys differ, say so and map only [PERSONA_OR_SEGMENT].
- Quotes are verbatim from the research; never invent or tidy them.
- Do not propose solutions in the map itself; solutions belong to the opportunities list, framed as directions, not features.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Scope
Segment, scenario, trigger, end state, sources used.
## Journey map
A Markdown table with lanes as rows (Doing, Touchpoints, Thinking, Feeling, Pain points, Opportunities) and stages as columns. Source tags in brackets in each cell.
## Emotional curve
One line per stage: stage, score, emotion, evidence. Mark the lowest point and abandonment points.
## Opportunities
Ranked "How might we..." statements, each with stage, evidence and why it ranks there.
## Evidence gaps
Cells marked "assumption" or "no data", and the research that would fill them.
</output_format>
