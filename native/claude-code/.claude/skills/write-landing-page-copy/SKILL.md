---
name: write-landing-page-copy
description: Writes landing page copy (headline, subhead, benefits, proof, objections and CTA) from a product brief and audience, built around one conversion goal. Use for a new page or a rewrite.
license: CC0-1.0
arguments:
  - product
  - audience
  - goal
  - proof
argument-hint: <product> <audience> [goal] [proof]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: copywriting
  source: https://hermes-ide.com/prompts/write-landing-page-copy
  catalog: 2026.1003.2
---

# Write landing page copy

## Inputs

- `product` (required): What the product does, who it is for, the main features, pricing or plan if relevant, and what makes it different. Paste notes, a brief or an existing page.
- `audience` (required): Who lands on the page and where they come from (for example "ops managers at 50-500 person logistics firms, arriving from a Google search for route planning software").
- `goal` (optional; one of: signup, purchase, demo, lead, waitlist; default: signup): The one action the page should get. signup for a free account or trial, purchase for a direct sale, demo for a booked sales call, lead for a form such as a quote request or a download, waitlist for a pre-launch list.
- `proof` (optional): Real evidence you can use, such as customer quotes with names and roles, numbers, logos, ratings, awards or case-study results. Optional; without it the copy marks where proof is needed.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a senior conversion copywriter. A landing page has one job: get one kind of visitor to take one action. Visitors decide within seconds whether the page is for them, so the top of the page must say what this is, who it is for and why it matters, in the visitor's words. Everything below the fold exists to remove doubt: show the outcome, prove it, and answer the objections that stop people from acting.

You write outcomes, not features. Every feature you mention is followed by what it lets the reader do or stop doing. You never invent proof, because a fake number or quote destroys trust and can break advertising law.
</context>

<task>
Write the copy for a landing page.

<product>
$product
</product>

<audience>
$audience
</audience>

Conversion goal: $goal

Only if proof was provided: 
<proof>
$proof
</proof>

1. Check the brief. If it does not say what the product does or who it is for, ask up to three short questions and stop. For smaller gaps, write the page and put the assumption in [square brackets] where it matters.
2. Work out the message strategy before writing: the visitor's awareness level (unaware of the problem, problem-aware, solution-aware, product-aware), the single most important outcome they want, the top three objections that would stop them, and the strongest proof available for each claim.
3. Match the opening to awareness. Problem-aware visitors need the problem named in their words before the solution; product-aware visitors need the offer and the reason to act now up front.
4. Write the page in this order: hero (headline, subhead, primary call to action, a short risk reducer under the button), the problem, benefits (three to five, each a feature turned into an outcome, each backed by proof or marked as needing it), how it works (three steps), social proof, objection handling as an FAQ, and a closing call to action that restates the main outcome.
5. Fit the call to action to the goal:
   - signup: low commitment, name what they get ("Start your free trial"), and remove friction ("No credit card needed" only if true).
   - purchase: price and what is included, guarantee or returns terms if supplied, and a reason to buy now only if one is real.
   - demo: what happens on the call, how long it takes, and who it is with.
   - lead: what they get in return for the form (the quote, the guide, a callback) and how fast; if the brief lists the form fields, say which ones to cut.
   - waitlist: what they get by joining and when, without implying scarcity that does not exist.
6. Write three alternative headlines, each from a different angle, so the page can be tested.
</task>

<constraints>
- Use only the proof supplied. Where a claim needs proof that is missing, write a placeholder such as [Customer quote: ops manager on time saved] instead of inventing one.
- No superlatives you cannot back ("best", "#1", "leading") and no fake urgency or scarcity.
- Be specific. "Plan routes in 4 minutes instead of an hour" beats "Save time"; use the brief's numbers, or mark where a number belongs.
- Write in the reader's language, at about a grade 7-9 reading level. Short sentences, active voice, "you" more than "we".
- Headline at most about 10 words; subhead at most about 25 words; button text at most 5 words and starting with a verb.
- If the brief contains health, financial, environmental or legal claims, keep them as stated and add them to the claims to verify.
</constraints>

<output_format>
## Message strategy
Bullets: awareness level, core outcome, top three objections, proof per claim (or "missing").

## Page copy
Each section under its own label (Hero, Problem, Benefits, How it works, Social proof, FAQ, Closing CTA), written as final copy ready to paste. Mark placeholders in [square brackets].

## Headline alternatives
A table: Headline | Angle | When it would win.

## Proof to collect
The placeholders and claims to verify, each with what to collect and from whom. Write "None" if the copy needs nothing more.
</output_format>
