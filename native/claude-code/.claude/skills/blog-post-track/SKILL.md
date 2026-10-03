---
name: blog-post-track
description: Takes a blog post from angle to outline, draft, edit and SEO packaging, pausing for approval between steps. Use when writing a blog post end to end.
license: CC0-1.0
arguments:
  - topic
argument-hint: <topic>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: workflow
  category: blogging
  source: https://hermes-ide.com/prompts/blog-post-track
  catalog: 2026.1003.2
---

# Blog post track

## Inputs

- `topic` (required): The post's topic or idea, with any notes, examples, data or links you already have.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

Writes a blog post about "$topic" one approved step at a time: the angle and the reader it serves, then a skimmable outline, then a full draft in the author's voice, then an edit pass, then the title, meta description and publishing package. Each step produces one artifact and stops for the author's approval or edits; later steps build on the approved versions and do not re-open settled decisions without asking. The author's knowledge is the raw material: the assistant shapes, drafts and edits, and marks every place where an example, source or fact is needed instead of inventing one. If the author asks to skip the approvals, confirm once that later steps will then build on unreviewed choices; if they agree, run the remaining steps in one reply, state the choice made at each skipped gate, and keep every placeholder visible.

## Steps

Work through these steps in order. Do not skip a gate.

1. angle (plan)
2. outline (plan)
3. draft (build)
4. edit (review)
5. package (ship)

### Step 1: Angle

Decide what the post about "$topic" argues and who it is for.

1. Ask the author, in one message, for anything not already given: the reader (who they are and what they already know), what the author knows from experience that most writers on this topic do not, the examples or data they can use, the target length, a writing sample for voice, and what the post should achieve (search traffic, sign-ups, reputation, answering a customer question).
2. When you have the answers, write:
   - **Reader:** one sentence, including the question or problem that brings them to the post.
   - **Main point:** one sentence the whole post argues or teaches.
   - **Angles:** three distinct angles (for example a how-to built on the author's method, a mistake and its fix, a contrarian take, a case study), each with a working title and why it beats the generic version of this post. Recommend one.
   - **Raw material:** examples, data and stories available, and what is still missing.
   - **Search note:** the phrase a reader would likely type, marked as a judgement, not data.

Stop and wait for the author to approve or edit the angle. Do not outline yet.

**Gate:** stop here and wait for the user's approval before step 2 (outline).

### Step 2: Outline

Outline the post about "$topic" from the approved angle.

1. Write the opening idea in two sentences: the specific moment, claim or question it starts with, and the promise to the reader.
2. List three to six H2 subheadings that each state a point, so that reading only the subheadings gives the argument. Under each, list the key points and the specific example, number or story from the approved raw material that supports it. Mark gaps as `[NEEDED: …]`.
3. Write the ending idea: the takeaway and the concrete next step for the reader.
4. Give a word budget per section that adds up to the agreed length.
5. Flag any section that does not serve the main point and suggest cutting it.

Stop and wait for approval or edits. Do not draft yet.

**Gate:** stop here and wait for the user's approval before step 3 (draft).

### Step 3: Draft

Draft the post about "$topic" from the approved outline.

1. Follow the approved outline and word budget. Keep the approved subheadings unless one clearly reads better reworded; say if you changed any.
2. Open with the approved opening idea within the first three sentences; no definitions, history or filler lead-ins.
3. In each section, explain one idea plainly with the example from the outline. Short paragraphs; lists only for sequences or options.
4. End with the takeaway and next step, not a recap or "In conclusion".
5. Match the author's writing sample in sentence length, formality, humour and phrasing. If there is none, write clear and conversational.
6. Use only facts and examples the author supplied. Keep every `[NEEDED: …]` gap visible as a placeholder, and list all placeholders and the word count after the draft.

Stop and wait for approval or edits. Do not edit or package yet.

**Gate:** stop here and wait for the user's approval before step 4 (edit).

### Step 4: Edit

Edit the approved draft about "$topic" in three passes, keeping the author's voice.

1. **Structure:** does every section serve the main point, in the best order? Is the opening specific and the ending useful? Propose moves or cuts.
2. **Clarity:** cut filler words and throat-clearing, split long sentences, replace vague claims ("many people", "significantly") with the specific detail from the notes or a placeholder, and make sure each paragraph has one job.
3. **Accuracy:** list every factual claim, number and quote, and mark each as supplied by the author or to verify. Flag anything that overstates the evidence.
4. Return the edited post in full, followed by a short change log of the substantive changes (not every comma) and the open placeholders.
5. Aim for 10 to 20% shorter than the draft unless the draft was already tight; say what you cut.

Stop and wait for approval or edits. Do not package yet.

**Gate:** stop here and wait for the user's approval before step 5 (package).

### Step 5: Package

Prepare the approved post about "$topic" for publishing.

1. **Titles:** five options under 60 characters with the main phrase near the start, each labelled with its approach (direct, how-to, number, question, contrarian). Recommend one. The title must promise only what the post delivers.
2. **Meta description:** two options under 155 characters that state the payoff in plain words.
3. **Slug:** short, lowercase, hyphenated, built from the main phrase.
4. **Internal and external links:** where in the post a link would help the reader, as `[LINK: what to link to]`. Never invent URLs.
5. **Image ideas:** one header image idea and alt text for it, plus any diagram that would make a section clearer.
6. **Social snippets:** one short post and one pull quote taken verbatim from the post.
7. **Pre-publish checklist:** open placeholders, claims to verify, links to add, and a final read-aloud check.
