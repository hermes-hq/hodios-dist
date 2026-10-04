---
name: analyze-competitor-channels
description: Analyses competing creator or brand channels from their recent content and metrics to find winning formats, topics, gaps and what not to copy. Use when planning how to stand out in a niche.
license: CC0-1.0
metadata:
  version: 1.0.1
  kind: prompt
  category: content-strategy
  source: https://hermes-ide.com/prompts/analyze-competitor-channels
  catalog: 2026.1004.0
---

# Analyse competitor channels

## Inputs

- [COMPETITOR_DATA] (required): For each competitor - channel name, platform, size, and their last 20 to 30 pieces with title, format, length, publish date and views or engagement; top comments help too.
- [YOUR_CHANNEL] (optional): Your channel, audience, strengths and recent performance, so the analysis can end in moves for you.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You analyse competing channels the way a content strategist does before advising a creator. Raw view counts mislead: a big channel's average video beats a small channel's best one. The useful signal is the outlier, a piece that did far better than that channel's own norm, because it shows what the audience wanted more than usual. Comparing each piece against its channel's median (an outlier score of views divided by the median views of that channel's recent pieces) makes channels of different sizes comparable. Patterns across outliers from several channels point to demand; patterns that appear in one channel only may be about that creator's personality or audience. Gaps show up in unanswered comment questions, topics that worked once but were never followed up, formats nobody does well, and audiences nobody serves directly.
</context>

<task>
<competitors>
[COMPETITOR_DATA]
</competitors>

<your_channel>
[YOUR_CHANNEL]
</your_channel>

1. **Data check.** What each competitor's data covers (pieces, date range, metrics), what is missing, and whether pieces are old enough to compare (very recent pieces are still growing). Compute the median per channel from the data given.
2. **Outliers.** For each channel, list pieces with an outlier score of 2 or more (or the top 10% if the data is small), with the score, format, topic and packaging. Show the maths.
3. **Winning formats.** Formats that produce outliers on more than one channel, and formats that consistently underperform.
4. **Winning topics.** Topic clusters behind outliers, separating demand signals that repeat across channels from one-off hits.
5. **Packaging patterns.** Title structures, thumbnail or cover approaches and opening hooks shared by the outliers, as patterns rather than wording to copy.
6. **Gaps.** Questions in comments nobody answers, outlier topics no one followed up, under-served audience segments, and formats that are missing or done poorly.
7. **What not to copy.** Things that work for a competitor because of their personality, existing audience, budget or access; misleading packaging; formats that are saturated; and anything that would make the creator a copy rather than an alternative.
8. **Moves for you.** If your channel is described, three to five specific moves (a format to test, a topic cluster to own, a packaging change) with why it fits the creator's strengths and how to test it. If it is not described, give moves for a new entrant and say what you would need to tailor them.
9. **Limits.** What this analysis cannot tell (traffic sources, retention, revenue) and how to check.
</task>

<constraints>
- Use only the data provided. Do not invent channels, numbers, pieces or audience details; if data is too sparse for a section, say so.
- Show every calculation that drives a conclusion; mark inferences as inferences.
- Never suggest copying a competitor's content, titles or thumbnails verbatim; describe the pattern and how to make an original version.
- Note when a pattern rests on one or two pieces.
</constraints>

<output_format>
Use one `##` heading per section, named and ordered as in the task: Data check, Outliers, Winning formats, Winning topics, Packaging patterns, Gaps, What not to copy, Moves for you, Limits. Data check and Limits as bullets. Outliers as a table: channel | piece | median | views | outlier score | format | topic. Moves for you as numbered items, each with the move, the reason and the test.
</output_format>
