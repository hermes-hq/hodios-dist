---
name: write-product-principles
description: Writes five to seven ranked product principles a team can use to settle trade-offs, each with its meaning, what it rules out and an example decision, tested against real debates.
license: CC0-1.0
arguments:
  - product_and_strategy
  - recurring_debates
argument-hint: <product_and_strategy> [recurring_debates]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: product-strategy
  source: https://hermes-ide.com/prompts/write-product-principles
  catalog: 2026.1004.3
---

# Write product principles

## Inputs

- `product_and_strategy` (required): The product, its users, the strategy or vision it serves, what makes it different, and any values or principles the company already has.
- `recurring_debates` (optional): Trade-offs the team argues about again and again (for example power features versus simplicity, speed versus polish, customisation versus defaults), with a real example of each. Optional but strongly recommended.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a product leader who has written principles that teams actually cite in design reviews. Most principle lists fail because they are platitudes nobody would argue against ("Be user-friendly", "Quality matters"), so they settle nothing. A useful principle takes a side in a real trade-off: its opposite is something a reasonable team might choose. The "X even over Y" form makes the trade-off explicit, where both X and Y are good things. Principles are also ranked, so when two point in different directions the team knows which wins.
</context>

<task>
<product_and_strategy>
$product_and_strategy
</product_and_strategy>
Only if recurring_debates was provided: 

<recurring_debates>
$recurring_debates
</recurring_debates>

If you cannot tell who the users are or what the product is trying to win at, ask for that and stop.

1. **Find the tensions.** From the strategy and the debates, list the trade-offs this team faces where both sides have merit. Principles come from these, not from generic best practice.
2. **Draft five to seven principles.** For each:
   - A short, memorable name (two to five words).
   - The statement in "X even over Y" form, or as a clear stance whose opposite is reasonable.
   - What it means in practice for this product (two or three sentences).
   - What it rules out: concrete things the team will say no to because of it.
   - An example decision, taken from the debates where possible, showing how it settles the call.
3. **Apply the opposite test.** Discard or rewrite any principle whose opposite is absurd ("We value security" fails; "Safe defaults even over fewer clicks" passes).
4. **Rank them** and state how to resolve a conflict between two principles, with one example.
5. **Test against the debates.** For each recurring debate, show which principle settles it and the resulting call. If a debate is not settled by any principle, say so: that is a gap or a decision for leadership.
6. **What we left out.** Candidate principles you dropped and why (too generic, really a goal or metric, already a company value).
7. **How to use them.** Three or four practical suggestions: cite them in specs and design reviews, revisit them on a set cadence, and name an owner.
</task>

<constraints>
- No platitudes, no slogans without consequences, no principle that is only a goal ("Grow revenue") or a metric.
- Ground every principle in the strategy or the debates given; when you infer a stance the input does not support, mark it "proposed - confirm with the team".
- Keep the whole set readable in two minutes: each principle's statement under 15 words.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Principles
For each, ranked:
### 1. Name
**Statement.**
- Means: …
- Rules out: …
- Example decision: …

## Ranking and conflicts
## Tested against our debates
| Debate | Principle that settles it | Call |
## What we left out
## How to use them
</output_format>

<examples>
<example>
Platitude: "Simple and intuitive."
Principle: "Sensible defaults even over configurability." Rules out: settings pages for choices most users never change; per-user toggles requested by one large customer. Example decision: ship one export format with good defaults instead of a builder with twelve options.
</example>
</examples>
