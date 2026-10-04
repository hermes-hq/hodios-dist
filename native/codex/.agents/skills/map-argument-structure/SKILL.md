---
name: map-argument-structure
description: Maps an argument into premises and conclusion, surfaces unstated assumptions, tests validity and soundness separately, and teaches the learner a method to do it themselves.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: tutoring
  source: https://hermes-ide.com/prompts/map-argument-structure
  catalog: 2026.1004.2
---

# Map an argument's structure

## Inputs

- [ARGUMENT] (required): The argument to analyse, as a quoted passage, an essay paragraph, an opinion piece or a claim with its reasons.
- [LEVEL] (optional): Optional level, for example "Year 10 critical thinking", "first-year philosophy", "general reader". Sets how much logic vocabulary to use.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Most people judge an argument by whether they like the conclusion. Argument mapping separates three questions: what exactly is being claimed and on what grounds (structure), whether the conclusion follows if the grounds are true (validity, or for non-deductive arguments, strength), and whether the grounds are actually true (soundness). Real arguments leave key premises unstated, and those hidden assumptions are usually where the argument is weakest. Charitable reconstruction, filling the gaps with the most plausible premise that makes the argument work, is what lets a critique hit its target.
</context>

<task>
Map this argumentOnly if [LEVEL] was provided:  for a learner at [LEVEL] level.

<argument>
[ARGUMENT]
</argument>

1. Decide whether the passage is an argument at all (a claim supported by reasons) rather than a description, explanation or story. If it is not, say so, explain the difference using the passage, and stop after a short example of how it could be turned into an argument.
2. Find the main conclusion. Use indicator words ("therefore", "so", "because", "since") and say which you used. If there are intermediate conclusions, find those too.
3. Write the argument in standard form: numbered premises (P1, P2…) and the conclusion (C), each a single clear statement paraphrased faithfully. Leave out rhetoric, repetition and examples that do not carry weight.
4. Draw the map as a text tree showing which premises support which conclusion, and whether premises work together (linked: each needs the other) or separately (convergent: each gives some support alone).
5. Supply the hidden assumptions: the unstated premises needed for the reasoning to work, chosen charitably. Mark each as added (A1, A2…).
6. Assess validity or strength: if all premises (including the added ones) were true, would the conclusion have to be true, or be very likely? Show any gap with a counterexample scenario where the premises hold and the conclusion fails.
7. Assess soundness separately: for each premise, is it true, doubtful or contested, and what evidence would settle it? Do not decide contested value questions; say they are value premises.
8. Teach the method: a short five-step routine the learner can reuse, then one new short argument for them to map, without the answer.
</task>

<constraints>
- Reconstruct charitably; do not attack a weaker version of the argument than the author made.
- Keep validity and truth separate throughout, and say explicitly that a valid argument can have a false conclusion and an invalid one a true conclusion.
- Do not take sides on the conclusion of a political or moral argument. Judge the reasoning, not the position.
- Name a formal or informal fallacy only when it explains a gap you have already shown; this is a mapping task, not a fallacy hunt.
- Use logic terms only as far as the level allows, and define each one the first time.
</constraints>

<output_format>
## Standard form
P1… C, with any intermediate conclusions marked.
## Map
A text tree, labelled linked or convergent.
## Hidden assumptions
A1, A2…, each with why it is needed.
## Validity
Valid or invalid (or strong or weak), with the counterexample if any.
## Soundness
A table: Premise | True, doubtful or contested | What would settle it.
## Do it yourself
The five-step routine, then a practice argument.
</output_format>
