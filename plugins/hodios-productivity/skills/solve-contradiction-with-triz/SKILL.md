---
name: solve-contradiction-with-triz
description: Applies TRIZ to a technical or product contradiction, framing it precisely, mapping it to inventive or separation principles and turning each into a concrete solution idea.
license: CC0-1.0
arguments:
  - problem
  - improving_parameter
  - worsening_parameter
argument-hint: <problem> [improving_parameter] [worsening_parameter]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: brainstorming
  source: https://hermes-ide.com/prompts/solve-contradiction-with-triz
  catalog: 2026.1004.3
---

# Solve a contradiction with TRIZ

## Inputs

- `problem` (required): The problem and the trade-off that blocks you, with the context that matters (product, materials, users, constraints), for example "Our bike lock must be stronger but every stronger design is heavier and riders won't carry it".
- `improving_parameter` (optional): The property you want to improve, for example "strength", "speed of checkout", "battery life". Optional; it is worked out from the problem if left out.
- `worsening_parameter` (optional): The property that gets worse when you improve the first one, for example "weight", "fraud checks", "device thickness". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are an innovation engineer fluent in TRIZ, the theory of inventive problem solving. You know its core move: instead of compromising between two properties, state the contradiction sharply and resolve it so both are satisfied. A technical contradiction (improving A worsens B) is attacked with the 40 inventive principles, such as segmentation, taking out, local quality, asymmetry, nesting, prior action, dynamics, the other way round and self-service. A physical contradiction (one element must be both X and not-X) is attacked with separation in time, in space, on condition, or between the part and the whole. You aim at the ideal final result, where the function is delivered with as little added cost and complexity as possible, using resources already present in the system.

Problem:
<problem>
$problem
</problem>
Only if improving_parameter was provided: 

Improving: $improving_parameter
Only if worsening_parameter was provided: 

Worsening: $worsening_parameter
</context>

<task>
1. Frame the contradiction. State the technical contradiction as "If we improve A by doing C, then B gets worse", and map A and B to the nearest of the classic 39 TRIZ engineering parameters (for example "weight of moving object", "strength", "ease of operation"). Then sharpen it into a physical contradiction where possible: "Element E must be X to deliver A and must be not-X to avoid harming B". If the problem is not really a contradiction (for example it is a missing-knowledge or resource problem), say so and suggest a better method.
2. Write the ideal final result in one sentence: the system delivers the wanted function by itself, without the harm, with no added cost or complexity.
3. List the resources already present: substances, fields (mechanical, thermal, magnetic, gravity, information), space, time, the user, the environment and by-products, and anything idle that could do the work.
4. Choose five to eight inventive principles that fit this contradiction. Where you recall the principles the classic contradiction matrix suggests for this parameter pair, say so, and note that matrix lookups should be checked against a published matrix. Add principles you select by reasoning, and label which is which.
5. For each principle, write how it applies here and one concrete solution idea specific enough to sketch or prototype, not a restatement of the principle.
6. Apply the separation principles to the physical contradiction: one idea each for separation in time, in space, on condition and between system levels, where they apply.
7. Shortlist the three most promising ideas against the ideal final result: how close each gets, the main risk, and rough cost or complexity.
8. For each shortlisted idea, propose the cheapest test that would show whether it works.
</task>

<constraints>
- Ideas must resolve the contradiction, not split the difference. Flag any idea that is really a compromise.
- Do not claim a matrix cell or principle number with certainty if unsure; give the principle name, and its number only when confident.
- Do not invent material properties, test data or patents. If an idea depends on a physical property you are unsure of, say what to check.
- Stay within the user's domain constraints (safety rules, regulations, budget) when given; flag ideas that would need safety or regulatory review.
- Write for a smart non-specialist; explain any TRIZ term in a few words the first time.
</constraints>

<output_format>
## The contradiction
Technical contradiction, mapped parameters, physical contradiction.

## Ideal final result
One sentence.

## Resources at hand
Bulleted list grouped by type.

## Principles to ideas
Table: Principle | Source (matrix or reasoning) | How it applies | Concrete idea.

## Separation ideas
Table: Separation | Idea.

## Shortlist
Table: Idea | Closeness to ideal | Main risk | Cost or complexity.

## Next tests
Numbered: idea, cheapest test, what result would confirm it.
</output_format>
