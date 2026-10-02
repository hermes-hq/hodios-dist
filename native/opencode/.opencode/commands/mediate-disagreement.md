---
description: Mediates a disagreement neutrally by restating each position fairly, finding the interests underneath, separating factual from value differences and proposing options both sides can accept.
---

# Mediate a disagreement

## Inputs

- [POSITIONS] (required): Each side's position in their own words where possible (paste messages or summarise), labelled by person or team.
- [CONTEXT] (optional): Optional background, such as the relationship, constraints (deadline, budget, policy), what has been tried and who decides if they cannot agree.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
Most disagreements stall because each side argues for a position (what they want) instead of explaining their interests (why they want it), and because factual disputes, value differences and constraints get mixed together. Interest-based negotiation (Fisher and Ury's "Getting to Yes") separates the people from the problem, looks for options that serve both sides' interests, and agrees on fair criteria for choosing. A mediator earns trust by restating each side so well that its own holder says "yes, that's exactly it", and by not taking sides.
</context>

<task>
Mediate this disagreement:
<positions>
[POSITIONS]
</positions>
Only if [CONTEXT] was provided: 
Context:
<context_notes>
[CONTEXT]
</context_notes>

1. If fewer than two positions are described, ask for the other side's view in their own words and stop. If only one side's account is available, say that the restatement of the other side is a guess to be checked.
2. Check whether mediation is appropriate. If the input involves harassment, abuse, discrimination, threats, or a serious misconduct complaint, do not mediate it as a disagreement between equals: say it should go to HR, a manager with authority, or the relevant authority, and stop.
3. Restate each position neutrally and in its best form, using the person's own reasoning, so each side would accept it as fair.
4. For each side, infer the interests underneath: needs, worries, goals, constraints. Mark inferred interests as such.
5. List genuine common ground, including shared goals.
6. Classify the real differences: facts (resolvable with evidence; say what evidence), predictions (resolvable with a test or pilot), values or priorities (need a trade-off or a decision rule), constraints, or misunderstanding (they actually agree).
7. Propose three to five options that serve both sides' interests, including at least one creative option and one way to reduce the stakes (a trial, a review date, splitting the decision).
8. Suggest objective criteria to choose among options, and who should decide if they still cannot agree.
</task>

<constraints>
- Stay neutral. Do not declare a winner, and do not split the difference by reflex. If the evidence clearly favours one side on a factual question, say what the evidence shows and leave the decision to them.
- Use neutral wording throughout; describe behaviour, not character.
- Do not invent facts about either side; ask through the questions section.
- If one side has power over the other (manager and report, parent and child), name it and account for it in the options.
</constraints>

<output_format>
## Positions restated
One short paragraph per side.
## Underlying interests
Per side, bullets, inferred ones marked "(inferred)".
## Common ground
Bullets.
## The real differences
A table: Difference | Type (fact, prediction, value, constraint, misunderstanding) | How it could be resolved.
## Options
A table: Option | Serves A because… | Serves B because… | Trade-off.
## Questions for each side
Two or three per side that would move things forward.
## Suggested next step
One concrete next step, with the decision criteria and who decides if needed.
</output_format>

Arguments: $ARGUMENTS
