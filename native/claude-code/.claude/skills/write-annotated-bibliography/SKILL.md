---
name: write-annotated-bibliography
description: Writes an annotated bibliography with a summary, evaluation and relevance note per source in the chosen citation style, flagging missing details instead of inventing them. For students.
license: CC0-1.0
arguments:
  - sources
  - topic
  - style
argument-hint: <sources> <topic> [style]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: literature-review
  source: https://hermes-ide.com/prompts/write-annotated-bibliography
  catalog: 2026.1002.2
---

# Write an annotated bibliography

## Inputs

- `sources` (required): The sources to annotate. For each, give the citation details and the text, abstract or your notes; annotations can only be as good as what you provide.
- `topic` (required): The research question or assignment topic the bibliography supports, used to judge each source's relevance.
- `style` (optional; default: APA): Citation style, for example APA, MLA, Chicago or Harvard, plus any assignment rules such as word count per annotation.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
An annotated bibliography shows that the writer has read and judged each source, not just found it. Each annotation does three jobs: it summarises the source's argument, method and main findings; it evaluates the source's authority, evidence and limits; and it explains how the source serves the writer's question, including how it relates to the other sources. Weak annotations restate the abstract, praise every source and never say why it matters. Citation details must be accurate; an invented page range or DOI is worse than a visible gap.
</context>

<task>
Write an annotated bibliography in $style style for this topic:
<topic>
$topic
</topic>
<sources>
$sources
</sources>

1. Format each citation in $style from the details given. Wherever a required element is missing (authors, year, title, journal, volume, issue, pages, DOI or URL, publisher), insert a visible marker such as [missing: issue number] and list it under Missing details.
2. For each source, write an annotation of about 120–180 words (or the length the user's assignment sets) in three parts:
   - **Summary:** the question or argument, the type of source and method, and the main findings or claims, from the material given.
   - **Evaluation:** the author's expertise or the venue as far as the material shows, the strength and limits of the evidence, currency, and any bias or conflict of interest stated.
   - **Relevance:** how it answers or complicates the topic, what part of the user's paper it could support, and how it agrees or disagrees with other sources in this list.
3. Order entries alphabetically by first author unless the style or user asks otherwise.
4. After the list, note gaps in the set as a whole: perspectives, methods, time periods or kinds of evidence that are missing for this topic.
</task>

<constraints>
- Use only what the user provides about each source. If you only have a citation and no content, write the citation and say that an annotation needs the abstract or text; do not summarise from memory.
- Never invent DOIs, page numbers, issue numbers or URLs.
- Apply the citation style's rules for author names, capitalisation, italics and punctuation consistently. If the style edition matters (for example APA 7 versus APA 6), use the latest edition unless told otherwise and say which.
- Keep the evaluation fair: name real strengths as well as limits.
- Write in the third person and in the user's academic register, not in marketing language.
</constraints>

<output_format>
## Annotated bibliography
For each source: the formatted citation on its own line (apply the hanging indent when you paste it into your document), then the annotation as one paragraph or three short labelled paragraphs if the user asked for labels.
## Missing details
Table: source | missing element | where to find it.
## Gaps in the set
Two to five bullets.
</output_format>
