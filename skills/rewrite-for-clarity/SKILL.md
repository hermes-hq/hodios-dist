---
name: rewrite-for-clarity
description: Rewrites technical prose so the main point comes first and every sentence is plain and specific, while keeping every fact, number and caveat. Use on design notes, emails, RFC drafts and docs.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: writing
  source: https://hermes-ide.com/prompts/rewrite-for-clarity
  catalog: 2026.1002.2
---

# Rewrite for clarity

## Inputs

- [TEXT] (required): The text to rewrite.
- [AUDIENCE] (optional; default: an engineer who knows the field but not this project): Who will read it.
- [LENGTH] (optional; one of: shorter, same, any; default: shorter): How long the rewrite may be compared with the original.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Technical writing is usually unclear for a few repeatable reasons: the conclusion is buried at the end, sentences hide the actor ("it was decided"), abstract nouns replace verbs ("perform an investigation of"), hedges pile up, and terms are used before they are defined. The fix is structural and line-level editing. Changing the meaning is not a fix: a clear sentence that says something the author did not mean is worse than the original.
</context>

<task>
Rewrite the text below for [AUDIENCE]. Length: [LENGTH].

<text>
[TEXT]
</text>

1. Find the main point: the decision, request or finding the reader must take away. Put it in the first sentence or two.
2. Order the rest by what the reader needs next: context and reasons after the point, details after the reasons.
3. Edit line by line:
   - one idea per sentence; split sentences over about 25 words;
   - name the actor and use active verbs ("the cache drops stale entries", not "stale entries are dropped");
   - turn nominalisations back into verbs ("decide", not "make a decision");
   - replace vague words with the specific fact from the text ("in 3 of 40 runs", not "sometimes");
   - cut filler and stacked hedges, but keep a hedge that carries real uncertainty;
   - define or replace jargon the audience may not know; keep terms of art they do know;
   - use a list when items are parallel, and prose when they are connected by reasoning.
4. Keep the author's voice and register. Do not make an informal note formal or the reverse.
</task>

<constraints>
- Preserve every fact, number, name, code snippet, link, commitment and caveat. Do not add claims, examples or opinions that are not in the original.
- If a sentence is ambiguous and the meaning matters, do not choose silently: pick the most likely reading and list the ambiguity under Check.
- If the text is already clear, say so and make only the edits that help. Do not rewrite for the sake of it.
- Code, commands and quoted error messages stay exactly as written.
</constraints>

<output_format>
## Rewrite
The rewritten text, ready to paste, in the original format (Markdown, plain text or email).
## What changed
At most five bullets naming the main kinds of edits.
## Check
Ambiguities you resolved and facts the author should confirm, or "None".
</output_format>
