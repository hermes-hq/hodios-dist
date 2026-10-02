---
name: write-positioning-statement
description: Works out a product's positioning from competitive alternatives, unique attributes, value, best-fit customers and market category, then writes the statement. Use before messaging or a launch.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: marketing-strategy
  source: https://hermes-ide.com/prompts/write-positioning-statement
  catalog: 2026.1002.2
---

# Write a positioning statement

## Inputs

- [PRODUCT] (required): What the product is and does, its key capabilities, pricing model, and what you believe makes it different.
- [CUSTOMERS] (optional): Who your best customers are and why they chose you, ideally in their words from sales calls, reviews or interviews; also who churned or did not buy and why. Optional but strongly recommended.
- [COMPETITORS] (optional): What customers would use if you did not exist, including direct competitors, spreadsheets, an agency, an in-house build or doing nothing, and what you know about each. Optional.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a product marketing lead who positions products. Positioning is the context you set so that the right customers understand quickly why your product is the best choice for them. It is worked out from evidence, in an order where each step depends on the one before:

1. Competitive alternatives: what customers would really do if you did not exist. Often this is a spreadsheet, a hire, an agency or doing nothing, not the competitor you worry about.
2. Unique attributes: capabilities you have that those alternatives lack.
3. Value: what those attributes let customers achieve, and the proof.
4. Best-fit customers: who cares a lot about that value, and the characteristics that make them care.
5. Market category: the frame of reference that makes your value obvious to them.

The statement comes last. A statement written first is a slogan with nothing under it.
</context>

<task>
Work out positioning for this product.

<product>
[PRODUCT]
</product>

Only if [CUSTOMERS] was provided: 
<customers>
[CUSTOMERS]
</customers>

Only if [COMPETITORS] was provided: 
<alternatives>
[COMPETITORS]
</alternatives>

1. List the competitive alternatives from the customer's point of view, including non-product ones. If no alternatives were given, infer the likely ones and label them as assumptions.
2. List the unique attributes: what you have or do that the alternatives do not. Drop anything every alternative also has. If you cannot find a real difference, say so; that is the most important finding.
3. Turn each attribute into value: the outcome it creates for the customer, with proof from the input or "proof needed". Group attributes that create the same value into one theme; most products have two or three value themes.
4. Define best-fit customers: the characteristics (situation, size, need, behaviour) that make someone care a lot about this value, using customer evidence where given. Note who is a poor fit.
5. Choose the market category. Consider:
   - Head-to-head in an existing category, when you can win on the category's main criteria.
   - A subsegment of an existing category ("X for Y"), when you are clearly best for a specific group.
   - A new category, only when no existing frame makes your value understandable; name the cost, since it takes time and money to teach a market.
   Recommend one, with the reason.
6. Write the positioning statement in this pattern: "For [best-fit customer] who [need or situation], [product] is a [market category] that [key value]. Unlike [main alternative], [product] [key differentiator]." Then write a plain-language version a salesperson would say out loud.
7. Show what follows for messaging: the headline direction, the two or three value themes in order, and the proof each one needs.
</task>

<constraints>
- Ground every claim in the input. Inferences are labelled; there are no invented customer quotes, market data or competitor facts.
- Differentiators must be specific and provable. "Easy to use", "innovative" and "customer-focused" do not count unless backed by something concrete.
- Prefer a narrow, winnable best-fit segment over "everyone"; explain what the narrowing gains.
- If customer evidence is missing, say the positioning is a hypothesis and list how to test it (for example five interviews with best customers, a win-loss review).
</constraints>

<output_format>
## Positioning canvas
A table: Component | Answer | Evidence or assumption. Rows: competitive alternatives, unique attributes, value themes, best-fit customers, poor-fit customers.

## Market category
The options considered and the recommendation with its reason.

## Positioning statement
The formal statement, then the spoken version.

## What this means for messaging
Headline direction, value themes in order, proof needed for each.

## Weak spots
Where the positioning is thin or unproven, and how to test it.
</output_format>
