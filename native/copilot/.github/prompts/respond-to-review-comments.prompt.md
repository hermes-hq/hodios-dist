---
description: Triages each review comment as fix, discuss or decline with a reason, drafts the replies, and applies the agreed fixes. Use when a pull request comes back with reviewer feedback.
agent: agent
argument-hint: comments mode
---

# Respond to code review comments

<context>
Review feedback is a mix of real defects, preferences, questions and misunderstandings. Accepting everything bloats the change and sometimes makes it worse; arguing with everything burns trust. Each comment deserves a decision with a reason the reviewer can accept.
</context>

<task>
Work through these review comments:
${input:comments:The review comments, pasted or as a PR URL, ideally with file and line for each.}

Mode: ${input:mode:plan: triage and draft replies only. apply: also make the changes marked fix.}.
1. For each comment, read the code it points at, as it is now, before deciding anything.
2. Classify it:
   - **fix**: the reviewer is right, or the change is cheap and harmless.
   - **discuss**: it is a trade-off, a question, or you need information the reviewer has.
   - **decline**: it is wrong, out of scope for this change, or conflicts with another requirement. Give the concrete reason, and offer a follow-up issue when it is out of scope.
3. When two comments conflict, say so and propose one resolution.
4. In `apply` mode, make every **fix** change as the smallest edit that addresses the comment, and nothing else. In `plan` mode, change no files.
5. Draft a short reply for each comment.
</task>

<constraints>
- Be honest about reviewer mistakes, but polite. Show the evidence (code, docs, a test) instead of asserting.
- Never make an unrequested change while applying a fix.
- If a comment is ambiguous, classify it **discuss** and ask one precise question rather than guessing what the reviewer meant.
- Replies are plain and specific: what you changed and where, or why not. No thanking boilerplate, no apologies.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
## Triage
A table: # | Comment (short) | Decision (fix, discuss, decline) | Reason.
## Changes
In `apply` mode: the diff, grouped by comment number, plus the result of any test you ran. In `plan` mode: "None (plan mode)".
## Replies
For each comment number, the reply text, ready to paste.
</output_format>
