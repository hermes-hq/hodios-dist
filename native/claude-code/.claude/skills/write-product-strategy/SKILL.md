---
name: write-product-strategy
description: Writes a one-page product strategy with a diagnosis of the core challenge, a guiding policy, coherent actions and an explicit list of what the team will not do.
license: CC0-1.0
arguments:
  - context
  - goals
  - constraints
argument-hint: <context> [goals] [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: product-strategy
  source: https://hermes-ide.com/prompts/write-product-strategy
  catalog: 2026.1002.2
---

# Write a product strategy

## Inputs

- `context` (required): The product, customers, market, competitors, current performance, what has been tried, and anything leadership has said about direction.
- `goals` (optional): Company or product goals for the period, with targets if known. Optional.
- `constraints` (optional): Budget, team size, deadlines, technical debt, regulatory or partner constraints. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a product leader who writes strategy the way Richard Rumelt describes it: a diagnosis that names the crucial challenge, a guiding policy that says how the team will deal with it, and a set of coherent actions that reinforce each other. Most "strategies" are really goal lists ("grow 40%"), wish lists of every initiative, or fluff ("be the customer-centric leader"). A real strategy makes choices, so it is as clear about what the team will stop or refuse to do as about what it will do. It fits on one page so that people actually read it and use it to make decisions.
</context>

<task>
Context:

<context_notes>
$context
</context_notes>

Only if goals was provided: Goals:
<goals>
$goals
</goals>
Only if constraints was provided: Constraints:
<constraints_given>
$constraints
</constraints_given>

1. Diagnose. Identify the one to three facts that explain why the situation is hard, and name the crucial challenge: the obstacle that, if overcome, unlocks the most progress. Use evidence from the context. If the context is too thin to diagnose, ask up to five targeted questions and stop.
2. Set the guiding policy: one or two sentences that describe the approach to the challenge and rule out reasonable alternatives. Name the alternatives considered and why they lose.
3. Choose three to five coherent actions that follow from the policy, use the team's real advantages, and reinforce each other. For each, say how it addresses the challenge and what it needs (people, time, partners).
4. Write what the team will not do: specific segments, features, channels or requests it will decline or stop, including at least one thing someone in the organisation currently wants.
5. Define how the team will know the strategy is working: leading indicators and one or two lagging outcomes, with targets if the goals provide them.
6. List the key assumptions and the evidence that would make you change course.
7. Test the draft: would a reasonable competitor choose differently? Could a team member use it to decide between two requests? If not, sharpen it.
</task>

<constraints>
- One page: about 400 to 600 words for the strategy itself, excluding assumptions and questions.
- Goals are not strategy; do not let the guiding policy restate a target.
- Every action must follow from the diagnosis; drop anything that does not, however attractive.
- Do not invent market data, competitor moves or customer numbers. Mark any inference from general knowledge as an assumption.
- Plain language. No "synergy", "leverage", "best-in-class", "world-class" or "customer-centric" without a concrete meaning.
</constraints>

<output_format>
## Diagnosis
A short paragraph ending with "The crucial challenge is ...".

## Guiding policy
One or two sentences, then "Alternatives we rejected:" with one line each.

## Coherent actions
Numbered: action, how it addresses the challenge, what it needs.

## What we will not do
Bullets, each with a one-line reason.

## How we will know
Bullets: indicator, target or direction, review date.

## Assumptions and risks
Bullets: assumption, evidence that would change our mind.

## Open questions
Bullets, or "None".
</output_format>
