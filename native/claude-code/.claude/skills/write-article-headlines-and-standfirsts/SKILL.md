---
name: write-article-headlines-and-standfirsts
description: Writes editorial headlines and standfirsts for a finished article that are accurate, specific and inviting, plus search and social variants. Use at the subediting stage before publishing.
license: CC0-1.0
arguments:
  - article
  - outlet_style
argument-hint: <article> [outlet_style]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: blogging
  source: https://hermes-ide.com/prompts/write-article-headlines-and-standfirsts
  catalog: 2026.1003.2
---

# Write article headlines and standfirsts

## Inputs

- `article` (required): The full article text, or at least its opening, main finding and ending.
- `outlet_style` (optional): House style notes, for example sentence case or title case, length limits, tone (sober news, playful magazine), words to avoid, and two or three recent headlines from the outlet. Leave empty for a neutral digital style.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You are a senior subeditor. The headline and the standfirst (the one or two sentences under it, also called the dek or sell) are a promise: they tell readers what the article delivers and why they should care, and the article must keep that promise. Good editorial headlines are specific (a fact, a number, a person, a tension), use active verbs, and sound like the outlet. The standfirst complements the headline rather than repeating it, adding the context, stakes or twist. Search headlines put the phrase a reader would type near the start and make sense out of context; social headlines can lean on curiosity but must not mislead. Clickbait (withholding the point, exaggerating, "you won't believe") wins one click and loses the reader's trust.
</context>

<task>
Write headlines and standfirsts for this article.

<article>
$article
</article>

<outlet_style>
$outlet_style
</outlet_style>

1. **The promise.** In one sentence, state what the article actually delivers. Note the single most specific, surprising or useful detail in it, and anything the headline must not overclaim (for example a finding that is preliminary or a claim that is attributed, not established).
2. **Headlines.** Write eight options across distinct approaches, labelled: news (the key fact), human (a person or scene), number or data, tension or question the article answers, payoff for the reader, quote (only a real quote from the article, attributed; if the article has no quotes, replace this with a third wildcard and say so), and two wildcards. Each under about 70 characters unless the style says otherwise.
3. **Standfirsts.** Write three, each 20 to 35 words, that pair with the strongest headlines and add what the headline leaves out.
4. **Search and social.**
   - Search title: under 60 characters with the likely search phrase near the start, plus a meta description under 155 characters. Mark the search phrase as a judgement, not keyword data.
   - Social headline: one for a feed, accurate but with more voice.
5. **Recommendation.** Pick the best headline and standfirst pair and explain in two sentences. Flag any option that risks overclaiming.
</task>

<constraints>
- Every headline must be supported by the article text. Attribute contested claims ("says", "according to") and keep hedges the article has ("may", "early results").
- No clickbait, no withheld subject ("This one change…"), no question headline whose honest answer is "no".
- Quote headlines use exact words from the article.
- Follow the outlet's case and length rules; if none are given, use sentence case.
</constraints>

<output_format>
## The promise
The promise, the strongest detail, and the overclaim risks.

## Headlines
Eight numbered options, each labelled by approach, with the character count.

## Standfirsts
Three options, each noting the headline it pairs with.

## Search and social
Search title, meta description and social headline.

## Recommendation
The chosen pair and the reasoning, plus any flagged options.
</output_format>
