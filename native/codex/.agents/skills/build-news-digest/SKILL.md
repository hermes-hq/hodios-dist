---
name: build-news-digest
description: Turns several articles into a short briefing - key developments, where sources agree or disagree, what is genuinely new and what to watch next - with every point traced to its source.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: summarization
  source: https://hermes-ide.com/prompts/build-news-digest
  catalog: 2026.1004.0
---

# Build a news digest

## Inputs

- [ARTICLES] (required): The full text of two or more articles, each with its outlet, date and headline if you have them. Separate articles clearly.
- [FOCUS] (optional): Optional - what you care about, for example "impact on EU fintech startups" or "what it means for my commute". Shapes what goes first.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
A useful digest saves the reader from reading every article without hiding how the coverage differs. It separates facts reported by several outlets from claims made by one, separates reporting from opinion, keeps attributions ("the ministry said", "according to two people familiar"), and is honest that the articles may be out of date or incomplete. It uses only the articles supplied.

<articles>
[ARTICLES]
</articles>
Only if [FOCUS] was provided: 
Reader's focus: [FOCUS]
</context>

<task>
1. Number the articles [1], [2], … in the order given, and note each one's outlet, date and type (news report, analysis, opinion, press release) where you can tell. If dates are missing, say so.
2. Extract the developments: what happened, who did it, when, and the key numbers. Merge duplicates across articles and cite every source that reports each one.
3. Compare the coverage:
   - Agreement: facts reported consistently by two or more sources.
   - Differences: conflicting numbers, timelines or explanations; claims that appear in only one source; differences in framing or what each outlet emphasises. State both sides with citations and do not resolve a conflict the articles do not resolve.
4. What is new: if the articles span time, what changed in the latest ones compared with earlier ones. If they do not, say what is new compared with the background the articles themselves give.
5. What to watch: scheduled events, decisions or data mentioned in the articles, and the open questions they leave.
6. If a focus was given, order everything by relevance to it and add one line on why it matters for that focus. Do not speculate beyond what the articles support; mark any inference.
</task>

<constraints>
- Use only the supplied articles. Do not add facts from memory, and say when something the reader would expect (for example the other side's response) is missing from the coverage.
- Keep attribution: an outlet's claim is not a fact, and an anonymous source is labelled as such.
- Opinion and analysis pieces are labelled; their arguments are not reported as events.
- Keep numbers, hedges and qualifiers exact.
- If only one article is supplied, produce a summary and say comparison needs at least two sources.
</constraints>

<output_format>
## Bottom line
Two or three sentences.
## Key developments
Bullets, most important first, each ending with citations like [1][3].
## Where sources agree
Bullets with citations.
## Where they differ
Bullets: the point, what each source says, with citations.
## What is new
Bullets.
## What to watch
Bullets with dates where given.
## Sources
Numbered list: outlet, headline, date, type.

Aim for under 400 words before the source list.
</output_format>
