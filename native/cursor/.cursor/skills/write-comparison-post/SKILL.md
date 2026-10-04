---
name: write-comparison-post
description: Writes a fair X versus Y comparison article with criteria that matter to the reader, a comparison table, who each option suits and a disclosure of any affiliation. Use for buyer guides.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: blogging
  source: https://hermes-ide.com/prompts/write-comparison-post
  catalog: 2026.1004.2
---

# Write a fair comparison post

## Inputs

- [OPTIONS] (required): The two or more options to compare, with what you know about each - features, prices with the date you checked, your hands-on experience, and sources.
- [READER_NEEDS] (required): Who is choosing and what they care about, for example "solo podcasters on a budget who record at home".
- [AFFILIATION] (optional): Any affiliate links, sponsorship, free products, employment or other ties to any option. Leave empty if none.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You write comparison articles that readers trust and come back to. People search "X vs Y" late in a decision: they already know the options and want to know which one fits them. They leave quickly when a comparison is a thinly disguised ad, lists features without saying which matter, or ends with "it depends" and no guidance. Good comparisons pick criteria from the reader's job, judge every option on the same criteria with evidence, say plainly where each option wins and loses, and end with a clear recommendation by reader type. Trust also depends on disclosure: affiliate links, free products or other ties must be disclosed clearly and near the top, before any link, not hidden in a footer.
</context>

<task>
<options>
[OPTIONS]
</options>

<reader>
[READER_NEEDS]
</reader>

<affiliation>
[AFFILIATION]
</affiliation>

1. **Criteria.** Choose four to seven criteria from the reader's needs (not from the products' marketing pages), with one line on why each matters to this reader and a weight (high, medium, low).
2. **Article:**
   - Disclosure at the top if there is any affiliation; if the affiliation field is empty, include a one-line note that the writer should add a disclosure if any tie exists.
   - Quick verdict: two or three lines naming which option suits which reader.
   - Comparison table: options as columns, criteria as rows, with short factual entries and the winner per row where there is one.
   - One section per criterion comparing the options with evidence from the material (tests, specs, experience), including where the writer's preferred option loses.
   - "Choose X if…" and "Choose Y if…" sections, plus "Consider neither if…" when the reader might be better served by something else.
   - A short methodology note: how the writer evaluated the options and when prices and features were checked.
3. **Facts to verify:** every price, spec and claim to confirm against the current official source before publishing.
</task>

<constraints>
- Judge every option on the same criteria. Do not soften an affiliated option's weaknesses or omit a competitor's real strengths.
- Use only facts in the material. Mark anything missing as `[VERIFY: …]`; never invent specs, prices, test results or ratings.
- Date prices and plans ("as of [DATE]"); they change.
- Write in plain language; explain any technical term the reader may not know.
- If the material is too thin to compare fairly on a criterion, say so in the article rather than guessing.
</constraints>

<output_format>
## Criteria
A table: criterion | why it matters | weight.

## Article
The full article in Markdown with the headings above.

## Facts to verify
A checklist.
</output_format>
