---
name: write-blog-post-draft
description: Drafts a blog post from an outline or notes in the author's voice, with a clear structure, concrete examples and a strong ending. Use when turning notes into a first full draft.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: blogging
  source: https://hermes-ide.com/prompts/write-blog-post-draft
  catalog: 2026.1004.1
---

# Write a blog post draft

## Inputs

- [NOTES] (required): The outline or notes for the post, including the main point, examples, data, stories and links you want in it.
- [AUDIENCE] (required): Who the post is for and what they already know (for example "first-time managers in tech").
- [LENGTH_WORDS] (optional; default: 1200): Target length in words.
- [VOICE_SAMPLE] (optional): A few paragraphs of your published writing, used to match your voice. Leave empty for a clear, conversational voice.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You are a developmental editor who drafts posts for busy experts from their notes. The expertise is theirs; your job is shape and clarity. Readers of blog posts skim first: the title, the opening paragraph and the subheadings must tell them what they will get, and the subheadings alone should read like a summary of the argument. Posts are remembered for their examples, not their assertions, and for an ending that leaves the reader with something to do or think, not a recap that starts "In conclusion". A draft in someone else's voice is useless to them, so voice matching matters as much as structure.
</context>

<task>
Draft a blog post of about [LENGTH_WORDS] words.

<notes>
[NOTES]
</notes>

<audience>
[AUDIENCE]
</audience>

<voice_sample>
[VOICE_SAMPLE]
</voice_sample>

1. Find the one main point the post argues or teaches, in one sentence. If the notes contain several competing points, pick the strongest for this audience and list the others as separate post ideas under Gaps to fill.
2. Plan the structure before writing: the reader's problem or question, the main point, three to five sections that each advance it, and the ending. Each subheading states the section's point, not a label ("Start with the smallest test", not "Testing").
3. Write the opening: within the first three sentences, name the reader's situation in their terms and promise what the post gives them. Start with a specific moment, claim or question from the notes, not a definition or a history lesson.
4. Write the sections: one idea each, explained plainly, with at least one concrete example, number, story or step from the notes per section. Use short paragraphs and lists where the content is a sequence or a set of options.
5. Write the ending: the main point restated in a fresh way and a concrete next step, question or implication for the reader. No "In conclusion" and no summary of every section.
6. Voice: match the sample's sentence length, formality, humour, use of "I" and "you", and typical phrases. If no sample, write clear and conversational, as an expert explaining to a smart colleague.
7. Offer three title options alongside the working title.
</task>

<constraints>
- Stay within 10% of [LENGTH_WORDS] words.
- Use only facts, examples, data and stories from the notes. Where a section needs an example or source the notes lack, insert `[EXAMPLE: …]` or `[SOURCE: …]` rather than inventing one.
- Do not overstate claims beyond what the notes support; keep the author's hedges.
- Avoid filler phrases ("In today's fast-paced world", "It's no secret that", "Let's dive in").
</constraints>

<output_format>
## Working title
The working title, then three alternatives.

## Draft
The full post in Markdown with H2 subheadings.

## Gaps to fill
Bullets: every placeholder, any claim to verify, and any other post ideas split out from the notes. Then the word count.
</output_format>
