---
name: write-editorial-guidelines
description: Writes editorial guidelines for a blog or publication's contributors covering voice, formats, sourcing and fact rules, AI use, formatting and the review process. Use before taking outside writers.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: content-strategy
  source: https://hermes-ide.com/prompts/write-editorial-guidelines
  catalog: 2026.1003.1
---

# Write editorial guidelines

## Inputs

- [PUBLICATION_AND_AUDIENCE] (required): What the publication is, who reads it and why, the kinds of pieces it runs, who writes for it (staff, freelancers, guest contributors), and examples of pieces you are proud of.
- [EXISTING_RULES] (optional): Any rules or habits you already have, for example a style guide you follow, banned words, how you handle corrections, your stance on AI-written text, or payment terms.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a managing editor who writes contributor guidelines that people actually follow. Good guidelines save editing time and protect the publication's credibility: they show the voice through examples rather than adjectives, make sourcing rules concrete, say exactly what a submission must include, and set expectations for the review process. They are short enough to read before a first piece and organised so a contributor can find an answer quickly. They also take positions where a publication must: how facts are checked, how corrections work, conflicts of interest, and how AI tools may or may not be used in research, drafting and images.
</context>

<task>
<publication>
[PUBLICATION_AND_AUDIENCE]
</publication>

<existing_rules>
[EXISTING_RULES]
</existing_rules>

Write contributor guidelines with these sections:

1. **Who we are and who we write for:** the reader in two or three sentences and what they come for.
2. **What we publish:** each format with a length range, purpose and an example headline in the publication's style.
3. **Voice and tone:** five to seven specific principles, each with a short "write this / not this" pair.
4. **Sourcing and facts:** link to primary sources, how to handle statistics (source, date, what they measure), quotes (accurate, attributed, interviewee aware they are on the record), claims about people or companies, anonymous sources, and the corrections policy.
5. **AI use:** what is allowed and what is not in research, outlining, drafting, editing and images, what must be disclosed and to whom, and that contributors remain responsible for every fact. Base it on the existing rules; if there are none, offer two options (strict and permissive) and put the choice in Decisions for you.
6. **Conflicts of interest and disclosure:** what contributors must declare (employment, clients, investments, free products, affiliate links) and how it appears to readers.
7. **Formatting:** headings, paragraph length, lists, links, images (rights, credit, alt text), and the file or tool format for submissions.
8. **Process:** pitch (what to include), commissioning, draft deadline, edit rounds, fact check, approval, publication, promotion, and fees and rights as placeholders unless given.
9. **What we do not publish.**

Then write a one-screen contributor checklist and a list of decisions the owner must make.
</task>

<constraints>
- Build on the existing rules; do not contradict them. Where you add a rule they did not have, keep it consistent with the publication's audience and mark it as a proposal in Decisions for you.
- Do not invent payment rates, rights terms, legal language or past pieces; use `[DECIDE: …]` placeholders.
- Keep the whole document readable in about ten minutes: concrete rules, short examples, no filler.
- Write the guidelines in the publication's own voice.
</constraints>

<output_format>
## Guidelines
The full document in Markdown with the nine sections above.

## Contributor checklist
Checkboxes a contributor ticks before submitting.

## Decisions for you
Each open decision with the options and a recommendation.
</output_format>
