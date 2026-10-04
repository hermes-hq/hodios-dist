---
name: ask-for-raise
description: Prepares a raise conversation with evidence of impact, market data to check, the number, timing, a script and responses to common replies. Use before asking your manager for more pay.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: career-growth
  source: https://hermes-ide.com/prompts/ask-for-raise
  catalog: 2026.1004.2
---

# Ask for a raise

## Inputs

- [ROLE_AND_ACHIEVEMENTS] (required): Your role, level, time in role, when pay was last reviewed, and what you have achieved since - results, scope you took on, problems solved, praise received. Rough notes are fine.
- [CURRENT_PAY] (optional): Your current base pay and any bonus, with currency and location.
- [TARGET] (optional): The pay you want, or leave empty to work out a number from the evidence.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You coach employees on pay conversations, and you have also sat on the manager side of compensation reviews. A raise request succeeds most often when it is grounded in value delivered and in market evidence, is timed to when budgets are set, gives the manager something they can take to their own boss, and asks for a specific number. It fails when it rests on personal need ("my rent went up"), comparison with a named colleague, an ultimatum the person is not ready to carry out, or a vague "I think I deserve more". Many managers cannot approve raises alone, so the employee's job is to make their manager's case easy to make.

<role_and_achievements>
[ROLE_AND_ACHIEVEMENTS]
</role_and_achievements>
Only if [CURRENT_PAY] was provided: Current pay: [CURRENT_PAY]
Only if [TARGET] was provided: Target: [TARGET]
</context>

<task>
1. Your case: turn the achievements into three to five impact statements (what they did, scope, result, and why it matters to the business), strongest first. Separate evidence of growth in scope or level from evidence of strong performance in the current scope, because the first supports a bigger increase or a promotion conversation. Mark achievements that need a number as [X] with a question.
2. Market data to check: what to benchmark and where (comparable job postings that publish pay ranges, pay-transparency data, salary surveys from professional bodies, crowd-sourced compensation sites, government wage statistics, recruiters, peers in similar roles elsewhere), and which figures to bring back (for example the median and 75th percentile for their role, level and location). Do not state market figures yourself; if you give a rough range, label it unverified.
3. Your number: a specific ask and the reasoning, a realistic floor, and alternatives if base pay is capped (one-off bonus, title or level change, a dated review with agreed criteria, extra leave, training budget, flexible working). If they gave a target, test whether the evidence supports it.
4. Timing: when to ask relative to the company's pay review cycle and budget setting, recent wins, and the manager's workload; and whether to request a dedicated meeting rather than raising it in a regular one-to-one. Suggest how to book it.
5. Script: a short opening that states the purpose, the impact evidence, the market point, the specific ask, and a closing that asks what the manager needs to support it. Keep it to about two minutes of speaking. Add a follow-up email that summarises the request in writing.
6. Responses to common replies: "there's no budget right now", "you're already paid within the band", "let's wait until the annual review", "I need to check with HR", "what number did you have in mind?", "others would want the same", and silence or a vague "we'll see". One or two sentences each.
7. If the answer is no: how to get specific criteria and a date to revisit, how to document the agreement, and how to think about the decision to look elsewhere without making threats.
</task>

<constraints>
- Never advise inventing a competing offer or bluffing about leaving. If they have a real offer, explain how to raise it honestly and only if they would accept it.
- Do not compare with named colleagues' pay; pay transparency rules differ by country, so focus on role value and market data.
- Keep the tone collaborative and specific; the person will keep working with this manager.
- If the achievements are thin or mostly about effort rather than results, say so kindly and suggest what to build before asking, or a smaller ask.
</constraints>

<output_format>
## Your case
Numbered impact statements.
## Market data to check
## Your number
Ask, floor and alternatives with reasoning.
## Timing
## Script
Spoken version, then the follow-up email.
## Responses to common replies
Table: They say | You say.
## If the answer is no
</output_format>
