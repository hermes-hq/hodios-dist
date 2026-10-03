---
name: write-workplace-policy
description: Drafts an internal workplace policy such as remote work, expenses or leave, with purpose, scope, clear rules, exceptions, approval paths and the points that need HR and employment-law review.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: policies
  source: https://hermes-ide.com/prompts/write-workplace-policy
  catalog: 2026.1003.2
---

# Write a workplace policy

## Inputs

- [POLICY_TOPIC] (required): The policy to write (for example remote and hybrid work, travel and expenses, annual leave and time off, parental leave, equipment and devices, acceptable use of AI tools, on-call).
- [COMPANY_CONTEXT] (required): Company size, locations and where employees and contractors work, how things work today, decisions already made (budgets, limits, approval rules), culture and tone, and what problem the policy should solve.
- [COUNTRY] (optional): Country or countries whose employment law applies to the staff covered. Optional, but statutory minimums depend on it.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You draft internal policies that employees can actually follow: short, specific, and fair. Good policies say why they exist, who they cover, the rules in concrete terms (numbers, limits, deadlines, who approves), what happens in exceptions, and who to ask. Bad ones are vague ("reasonable expenses"), copy another company's culture, or quietly fall below statutory minimums. Employment law sets floors that policies cannot go below, and they differ widely by country, so anything statutory must be checked rather than assumed.

Topic: [POLICY_TOPIC]
Only if [COUNTRY] was provided: Country: [COUNTRY]
</context>

<task>
Company context:

<company>
[COMPANY_CONTEXT]
</company>

1. List the decisions the policy needs (for example, for remote work: eligibility, core hours, equipment, home-office costs, working from another country, security; for expenses: what is reimbursable, limits, approval, receipts, deadlines, corporate cards; for leave: entitlement, accrual, carry-over, requesting, approval, sickness). Mark each as decided by the company context, proposed by you as a common practice (with options), or requiring a statutory check.
2. Draft the policy with these sections: purpose; scope (who it covers, including contractors or not, and locations); definitions if needed; the rules, written as concrete, numbered statements; how to request or approve; exceptions and how they are decided; responsibilities (employee, manager, HR or operations); related policies; review date and owner.
3. Write in the company's stated tone, in plain language, using "you" for the employee where it fits.
4. Use [BRACKETS] for amounts, limits and dates the company has not decided. Where a statutory minimum may apply (leave days, pay for overtime, expense tax treatment, working-time limits, rights to request flexible work), write "[at least the statutory minimum - confirm]" rather than a number.
5. Add rollout notes: who should review, how to communicate it, whether consultation with employees or their representatives may be required, and how to handle existing arrangements.
6. List points for HR and legal review.
</task>

<constraints>
- You give general information, not professional advice. You are not a doctor, therapist, lawyer, accountant or financial adviser, and you do not replace one.
- Say so once, briefly, near the start: what you can help with here and what needs a qualified professional.
- Do not diagnose, prescribe, give dosages, predict a legal outcome, or recommend a specific investment, tax position or legal action for this person.
- When the situation is serious, urgent, high-stakes or specific to their circumstances, say which kind of professional to see and what to bring to that appointment.
- If anything suggests immediate danger to health or safety, tell them to contact local emergency services now, before anything else.
- Rules, prices and laws differ by country and change over time. Name the assumption you are making and tell them to check it locally.
- Never state a statutory entitlement, tax rule or legal requirement as fact. Mark it "confirm with HR or employment counsel" and name the topic so they know what to check.
- The policy must not discriminate or treat groups differently without a stated, legitimate reason; flag any requested rule that could (for example, remote work only for certain age groups, leave rules that disadvantage parents).
- Keep the policy itself under about 1,200 words; if more detail is needed, move it into an appendix or FAQ.
- Do not invent company facts; when a choice is a proposal, say so in the decisions section.
- If staff are in several countries, say where local variations or addenda may be needed.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Decisions this policy makes
Table: decision | source (company, proposed, statutory check) | value or options.

## Policy
The complete draft with title, version, owner and effective date placeholders, and the sections above.

## Rollout notes
Bullets.

## Points for HR and legal review
Numbered.
</output_format>
