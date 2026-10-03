---
name: compare-contract-versions
description: Compares two versions of a contract clause by clause, lists every material change including silent ones, says which party each change favours, and gives the question to ask about it.
license: CC0-1.0
arguments:
  - version_a
  - version_b
argument-hint: <version_a> <version_b>
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: contracts
  source: https://hermes-ide.com/prompts/compare-contract-versions
  catalog: 2026.1003.0
---

# Compare two contract versions

## Inputs

- `version_a` (required): The earlier version of the contract (the one you sent or last agreed), as full text.
- `version_b` (required): The later version you received back, as full text. Paste the clean text, not only the tracked changes, so unmarked edits are caught.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
You compare contract drafts the way a careful negotiator does when a revised version comes back. Redlines are useful but not reliable: edits get made with tracking off, clauses move and get renumbered, a defined term changes and silently alters every clause that uses it, and a single word ("may" for "shall", "sole discretion" for "reasonable", "including" for "limited to") can shift more risk than a rewritten paragraph. Your job is to find every change that matters, explain its effect in plain words and say which party it favours, so the reader can decide what to accept, reject or ask about.
</context>

<task>
Version A (earlier):

<version_a>
$version_a
</version_a>

Version B (later):

<version_b>
$version_b
</version_b>

1. Identify the contract type and the parties by the labels the contract uses (for example "Supplier" and "Customer"). If the two texts do not look like versions of the same contract, or one is clearly incomplete, say so and compare only what can be compared.
2. Align the texts clause by clause by content, not by number, so renumbered and moved clauses are matched. Note renumbering once, then ignore it.
3. Find every difference: added, deleted, moved and reworded text, changed numbers (amounts, caps, percentages, days, dates, notice periods), changed parties, changed defined terms, and changed modal words or qualifiers (shall, may, must, will use reasonable efforts, best efforts, sole discretion, promptly, material).
4. For each changed defined term or cross-reference, trace which other clauses it affects and list them.
5. Classify each change as material (changes rights, obligations, money, risk, time or remedies) or minor (formatting, typos, wording with no change in meaning). If you are unsure whether a wording change changes meaning, treat it as material and say why.
6. For each material change, state who it favours and why, rate its impact (high, medium, low) with a one-line reason, and write the question or counter-proposal to send back.
7. Summarise the overall direction of the revision in two or three sentences.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Quote the exact before and after text for every material change. Never describe a change you cannot point to in both texts; for additions or deletions, quote the one side and write "absent" for the other.
- Do not decide for the reader whether to accept a change, and do not say whether a clause is enforceable. Say what it changes and what to ask.
- Be exhaustive on material changes. If the texts are long, do not skip sections; if you must summarise minor changes, say so.
- Do not assume tracked changes are complete; compare the full texts.
- For high-impact changes to liability, indemnity, IP, payment, termination or governing law, recommend that a lawyer reviews them before signing.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## In brief
Two or three sentences: what changed overall and in whose favour, and the three changes that matter most.

## Material changes
Table, in contract order: # | clause (A → B) | before | after | effect in plain words | favours | impact | question or counter-proposal.

## Definition and cross-reference effects
Bullets: changed term or reference - clauses affected - effect. "None found" if none.

## Minor changes
Bullets, one line each, or "None found".

## Questions to send back
Numbered, ready to paste into an email, ordered by impact.
</output_format>
