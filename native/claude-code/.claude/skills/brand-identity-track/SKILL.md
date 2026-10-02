---
name: brand-identity-track
description: Takes a brand from discovery and positioning to a brand platform, verbal identity, visual direction and guidelines, pausing for approval between steps. Use for a new business or a rebrand.
license: CC0-1.0
arguments:
  - business
  - audience
  - constraints
argument-hint: <business> <audience> [constraints]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: branding
  source: https://hermes-ide.com/prompts/brand-identity-track
  catalog: 2026.1002.2
---

# Brand identity track

## Inputs

- `business` (required): What the business sells, to whom, how it makes money, its stage, and for a rebrand what exists today (name, logo, colours, reputation).
- `audience` (required): Who the brand must win, as specifically as you can, plus anything you know about how they choose and what they use today.
- `constraints` (optional): Fixed points and limits - a name you must keep, budget, deadline, markets and languages, regulation, assets that cannot change. Optional.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Builds a brand identity in the order that makes it hold together: understand the business and audience, choose a position, write the brand platform, then the words, then the look, then the rules that keep it consistent. Each step produces one document and stops for approval, and later steps build on the approved versions instead of re-deciding them.

<business>
$business
</business>

<audience>
$audience
</audience>
Only if constraints was provided: 
<constraints>
$constraints
</constraints>

Rules for every step: never invent research findings, customer quotes, competitor claims or market figures; when evidence is missing, label the statement as a hypothesis and say how to check it. Every choice must rule something out; drop anything that could describe any company in the category. Respect the constraints and existing brand equity: for a rebrand, say what is kept and why before proposing change. Do one step at a time, show its output, and wait for approval or edits before the next.

## Steps

Work through these steps in order. Do not skip a gate.

1. discovery (discover)
2. positioning (plan)
3. platform (plan)
4. verbal-identity (design)
5. visual-direction (design)
6. guidelines (review)

### Step 1: Discovery

1. Summarise what you know about the business, the audience and the constraints in a short brief. Mark each point as given, inferred or unknown.
2. Ask the questions whose answers would change the brand, grouped and numbered, at most 12: why customers choose this business today (or would), what they use instead, the top three competitors and how they present themselves, what the founders refuse to be, the price position, where the brand will be seen most (app, shelf, sales deck, social, signage), and for a rebrand what customers already recognise.
3. List the evidence that would make the next steps stronger and the quickest way to gather each piece: 5 to 8 customer conversations, review mining, sales or support notes, a competitor screenshot wall, search terms.
4. For a rebrand, start an equity list: current assets (name, colours, symbol, phrases, characters) and a first guess at how recognised and how distinctive each one is, marked as a guess.

Stop for approval. Ask the user to answer the questions and bring any evidence before positioning.

**Gate:** stop here and wait for the user's approval before step 2 (positioning).

### Step 2: Positioning

If step 1's questions are unanswered, ask for the answers and stop.

1. Map the competitors on the two or three dimensions customers actually use to choose (from the evidence, not from what the company wishes mattered). Show the map as a table and name the space nobody occupies, or the cliché everyone shares.
2. Write two or three distinct positioning options. For each: "For <audience> who <need>, <brand> is the <frame of reference> that <key benefit>, because <reason to believe>. Unlike <alternative>, it <difference>."
3. Test each option: true today (can the business prove it), relevant (does it affect the choice), distinctive (could a competitor say it unchanged), and durable (still true in three years). Show the result per test.
4. Recommend one option and state what the brand gives up by choosing it.

Stop for approval of one positioning, edited if needed.

**Gate:** stop here and wait for the user's approval before step 3 (platform).

### Step 3: Brand platform

Build on the approved positioning only.

1. Purpose: why the company exists beyond profit, in one sentence a customer would believe.
2. Mission: what it does now, for whom, and how. Vision: the future it is working towards, specific enough to say when it is reached.
3. Values: three or four, each with a one-line meaning, two "we do" behaviours, one "we don't" and the trade-off it implies in a real decision (hiring, pricing, product, service).
4. Personality: three or four traits as "X, not Y", placed on funny-serious, formal-casual and expressive-restrained.
5. Promise and proof: the one promise every interaction must keep, and the proof points that support it today, with gaps marked.
6. Brand idea: the compressed thought (two to five words) that holds the platform together, with two alternatives.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 4 (verbal-identity).

### Step 4: Verbal identity

Build on the approved platform. If the name is not fixed by the constraints and the user wants naming, propose naming territories and 10 to 15 candidates with risk flags, and say that trademark, domain and language checks must be done before any choice.

1. Voice: three or four attributes derived from the personality, each with "this means" and "this does not mean", and an example line.
2. Tone by situation: a short table for welcome, selling, instructions, errors, money and apologies.
3. Tagline: three options, each tied to the brand idea, with the one you recommend.
4. Messaging hierarchy: the core message, three supporting messages each with proof, and an elevator line of under 25 words.
5. Vocabulary: words to own, words to avoid with replacements, and how to name products and features.
6. Before and after: four rewrites of the user's existing copy if given, otherwise of typical lines for the category, marked as illustrative.

Stop for approval.

**Gate:** stop here and wait for the user's approval before step 5 (visual-direction).

### Step 5: Visual direction

Build on the approved platform and verbal identity. This step sets direction for a designer; it does not replace one.

1. Write two or three visual directions. Each one: a name, the idea behind it and how it expresses the brand idea, mood words that rule something out, logo approach (wordmark, symbol plus wordmark, or emblem) with notes on form, a typography direction (classification and character, not specific licensed fonts unless the user names them), a colour strategy (one ownable lead colour, roles for supporting colours and neutrals, and how it differs from competitors), an imagery and illustration style, and one distinctive asset the brand could repeat for years.
2. For a rebrand, say which existing assets each direction keeps, evolves or drops.
3. Check each direction at the brand's most common touchpoints from step 1 (for example a 16-pixel favicon, a shelf at two metres, a dark-mode app header, a one-colour print) and flag where it struggles.
4. Give a short brief for each direction that a designer or an image model can work from, and say that generated images are mood references, not final artwork.
5. Recommend one direction and say why.

Stop for approval and ask the user to return with the chosen designed assets (logo files, colour values, fonts) before the guidelines.

**Gate:** stop here and wait for the user's approval before step 6 (guidelines).

### Step 6: Brand guidelines

Write the brand guidelines from the approved outputs of steps 2 to 5 and any final assets the user supplied. Use only values the user gave (colour codes, font names, logo versions); write [TBD] for anything not yet designed instead of inventing it.

Sections, as `##` headings:
1. Brand on a page: positioning, brand idea, purpose, values and personality in one screen.
2. Logo: versions, clear space, minimum sizes for print and screen, placement, and at least six misuse examples.
3. Colour: values per format, roles and approximate proportions, and contrast pairs for text.
4. Typography: families, hierarchy and fallbacks.
5. Imagery and illustration: what to shoot or draw, and what never to use.
6. Voice and tone: the summary from step 4 and the tone table.
7. Applications: the top five touchpoints from step 1 with what good looks like.
8. Do and don't: eight pairs across the whole system.
9. Governance: who approves new uses and where assets live.

End with a launch checklist: the assets still to produce, the checks still to run (trademark, accessibility, print proofs) and the order to roll them out.
