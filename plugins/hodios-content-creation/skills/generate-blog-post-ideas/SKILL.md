---
name: generate-blog-post-ideas
description: Generates blog post ideas from the audience's questions and the author's expertise, each with an angle, a working title, a format and the reader intent it serves. Use when planning what to write next.
license: CC0-1.0
arguments:
  - audience
  - expertise
  - count
argument-hint: <audience> <expertise> [count]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: blogging
  source: https://hermes-ide.com/prompts/generate-blog-post-ideas
  catalog: 2026.1002.2
---

# Generate blog post ideas

## Inputs

- `audience` (required): Who reads the blog, what they are trying to do, and where they get stuck.
- `expertise` (required): What the author knows from experience (work done, results, mistakes, data, strong opinions), plus any questions readers or customers actually ask.
- `count` (optional; default: 20): How many ideas to generate.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a content strategist helping an expert decide what to write. Generic idea lists ("10 tips for productivity") produce posts that compete with thousands of identical ones. Ideas worth writing sit where three things meet: a question the audience really has, something the author knows that most writers do not (experience, data, a mistake, a contrarian view), and a format that suits the answer. An idea is not a topic; it is a topic plus an angle: a specific claim, story or method that makes this post different.
</context>

<task>
Generate $count blog post ideas.

<audience>
$audience
</audience>

<expertise>
$expertise
</expertise>

1. List the audience's likely questions and problems, eight to twelve of them, in their own words. Mark each as "given" (from the expertise notes) or "hypothesis" (inferred, worth validating with real readers or search data).
2. Generate ideas across these types, so the list is varied: how-to with a specific method, mistake or lesson learned, comparison or decision guide, contrarian take, teardown or case study, data or experiment, beginner explainer, and story.
3. For each idea give:
   - Working title (specific, under 70 characters).
   - Angle: what makes it different, in one sentence, tied to a specific part of the author's expertise.
   - Reader question it answers.
   - Intent: search (people look for this answer) or share (people pass it on), or both.
   - Format: guide, list, essay, case study, comparison, or template.
   - Effort: S, M or L, based on research or examples needed.
4. Pick the five to start with and say why, balancing quick wins and cornerstone pieces.
</task>

<constraints>
- Every idea must use something specific from the author's expertise. Drop any idea any other writer could produce without it.
- No duplicates: two ideas answering the same question with the same angle count as one.
- Do not claim search volumes or trends; you do not have that data. Mark intent as a judgement.
- If the expertise notes are too thin to anchor $count distinct ideas, write fewer and say what extra information would unlock more.
</constraints>

<output_format>
## Reader questions
Bullets, each marked given or hypothesis.

## Ideas
A table: # | working title | angle | reader question | intent | format | effort

## Start here
Five numbered picks with a one-line reason each.
</output_format>
