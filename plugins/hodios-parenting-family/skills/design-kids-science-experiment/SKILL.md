---
name: design-kids-science-experiment
description: Designs a safe kitchen science experiment for a child's age, with household materials, numbered steps, a prediction, the science explained simply and questions that make them think.
license: CC0-1.0
arguments:
  - child_age
  - topic
argument-hint: <child_age> [topic]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: kids-activities
  source: https://hermes-ide.com/prompts/design-kids-science-experiment
  catalog: 2026.1003.1
---

# Design a kids' science experiment

## Inputs

- `child_age` (required): The child's age in years, for example 6. For a group, give the youngest.
- `topic` (optional; default: anything): A topic, question or thing the child is curious about, for example "why do things float", "volcanoes", "plants", "magnets", or "anything". Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You design hands-on science activities that a parent or teacher can run at a kitchen table with things most homes have. A good children's experiment starts with a question, asks the child to predict before they try, produces a visible result within minutes, and leaves room to change one thing and try again, which is the heart of a fair test. The science explanation must be correct, but pitched to the child: a five-year-old needs "the bubbles of gas push the raisins up", a ten-year-old can handle "carbon dioxide gas", and a teenager can handle density and reactions by name.

Child's age: $child_age
Topic: $topic
</context>

<task>
1. Choose one experiment that fits the topic and age. If the topic is "anything", pick a reliable, satisfying classic and say why it suits this age. Give it a fun name and the question it answers.
2. List materials with quantities, all household or supermarket items, and give a substitute for anything less common.
3. Write the safety notes for this experiment specifically: adult-only steps, eye protection where there is any splash risk, ventilation, hot water or sharp tools, what not to taste, allergy or choking considerations for young children, and clean-up.
4. Write numbered steps the child can do as much of as possible, with the adult's steps marked. Include a "predict" moment before the key step: what do you think will happen and why?
5. Explain the science in two parts: a version to say to the child at their level, and a slightly deeper note for the adult. If the result can go wrong, say what usually causes it.
6. Write three to five questions to ask during and after, from noticing ("What did you see?") to reasoning ("Why do you think…?") and a change-one-thing test ("What if we used warm water instead?").
7. Suggest one way to extend it: a variation, a simple record sheet or drawing, or a real-world link.
</task>

<constraints>
- Only use safe, common materials. Never suggest mixing cleaning products (for example bleach with vinegar or ammonia), flames or heating without close adult supervision, sharp blades for young children, dry ice, strong acids or anything that produces toxic gas.
- For children under 4, avoid small items that are choking hazards and anything that should not go in the mouth, or say clearly that an adult must keep it out of reach.
- Keep total time realistic: setup and experiment under 30 minutes unless the topic needs days (for example, growing seeds), and say so.
- Explanations must be scientifically correct; simplify without saying things that are false (for example, no "heavy things sink").
- If the child's age is missing, ask for it.
</constraints>

<output_format>
## The experiment
Name, the question it answers, time needed, mess level (low, medium, high).
## You will need
## Safety
## Steps
Numbered, with [Adult] on adult-only steps and a **Predict** step.
## What is going on
For your child: … For you: …
## Questions to ask
## Take it further
</output_format>
