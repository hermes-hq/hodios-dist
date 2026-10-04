---
name: write-tech-blog-post
description: Turns engineering notes, code and results into a technical blog post with one clear takeaway, real numbers and working code, and no hype. Use for engineering blogs and write-ups of a project.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: writing
  source: https://hermes-ide.com/prompts/write-tech-blog-post
  catalog: 2026.1004.0
---

# Write a technical blog post

## Inputs

- [TOPIC] (required): What the post is about, in one line.
- [NOTES] (required): The source material, such as notes, code, measurements, incident timelines or a PR description. The post uses only facts from here.
- [AUDIENCE] (optional; default: working software engineers who do not know this codebase): Who reads the blog and what they already know.
- [WORDS] (optional; default: 1200): Target length in words.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Engineers read technical posts to learn something they can use: a technique, a trade-off, a mistake to avoid. They leave at the first sign of marketing or vagueness, and they distrust numbers without a method. The best posts follow one concrete problem from symptom to solution, show the dead ends honestly and end with a takeaway the reader can apply elsewhere.
</context>

<task>
Write a post about: [TOPIC]
For: [AUDIENCE]. Target length: about [WORDS] words.

<notes>
[NOTES]
</notes>

1. Decide the one takeaway a reader should leave with, in one sentence. Every section must serve it; cut material that does not.
2. Open with the concrete problem or surprising result in the first two sentences: a symptom, a number, a failure. No scene-setting about the industry.
3. Give only the context needed to follow along.
4. Walk through what was tried, in order, including what did not work and why. Show code or config where it carries the explanation, trimmed to the lines that matter.
5. Present the result with the numbers from the notes and how they were measured.
6. Name the trade-offs and when this approach is the wrong choice.
7. Close with the takeaway, phrased so it applies beyond this codebase.
</task>

<constraints>
- Use only facts, numbers, quotes and code from the notes. If a claim needs a figure that is not there, write `[needs number: ...]` instead of estimating.
- Code must be consistent with the notes and minimal; do not invent APIs or library features.
- No hype or filler: avoid "in today's fast-paced world", "game-changer", "seamless", "unlock", "delve", "robust" and rhetorical questions as openers.
- Use "we" for the team's work and "you" for the reader. Short paragraphs; descriptive subheadings.
- Do not name customers, colleagues or internal systems unless the notes say they can be named.
</constraints>

<output_format>
## Titles
Three title options: one plain and descriptive, one leading with the result, one leading with the problem. No clickbait.
## Post
The full post in Markdown with subheadings.
## Facts to verify
Every number, quote and factual claim in the post, each with where it came from in the notes, plus any `[needs number]` gaps.
</output_format>
