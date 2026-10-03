---
name: design-support-chatbot-flow
description: Designs a support chatbot or AI agent flow - intents, answers grounded in help content, escalation triggers, human handover and quality checks. Use when adding automation to a support team.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: customer-support
  source: https://hermes-ide.com/prompts/design-support-chatbot-flow
  catalog: 2026.1003.1
---

# Design a support chatbot flow

## Inputs

- [TOP_CONTACT_REASONS] (required): Your most common contact reasons with rough volumes, and examples of real customer messages for each.
- [HELP_CONTENT] (optional): Your help-centre articles, macros or policies, or a list of what exists. The bot may only answer from this content. Leave empty to get a list of what to write first.
- [CONSTRAINTS] (optional): Limits and rules - channels, languages, hours when humans are available, actions the bot may take (look up orders, issue refunds), regulated topics, brand tone.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
You design support automation that customers do not hate. A support bot earns its place by resolving simple, frequent questions accurately and by handing everything else to a human quickly, with the context attached. Bots fail when they answer from guesswork instead of approved content, trap customers in loops with no way to reach a person, take actions without the right checks, or are measured on deflection rather than on resolution and satisfaction.
</context>

<task>
Design the bot flow.

<top_contact_reasons>
[TOP_CONTACT_REASONS]
</top_contact_reasons>
Only if [HELP_CONTENT] was provided: 
<help_content>
[HELP_CONTENT]
</help_content>
Only if [CONSTRAINTS] was provided: 
<constraints_given>
[CONSTRAINTS]
</constraints_given>

1. Automation scope: classify each contact reason as automate fully (informational, low risk, answered by existing content), automate with an action (needs a lookup or a transaction with verification), assist then hand over, or route straight to a human (complaints, vulnerable customers, legal or safety, complex billing disputes, anything regulated). Give the reason for each.
2. Intent map: for each in-scope intent, example customer phrasings (including messy ones), the information the bot must collect, and the clarifying question if the intent is ambiguous.
3. Grounded answers: for each automated intent, the answer drafted only from the help content given, with the source article named. If no content covers it, do not write an answer; list it under Content gaps.
4. Escalation triggers: explicit rules for handing over, such as the customer asks for a human, two failed attempts or a repeated question, negative sentiment or frustration, keywords for cancellations, complaints, legal threats, safety or distress, high-value or VIP accounts, low confidence, or any request outside scope.
5. Handover design: what the bot tells the customer (who will reply and when, based on human availability), the summary passed to the agent (intent, details collected, what was tried, customer sentiment), and the out-of-hours path.
6. Bot instructions: a system prompt for the bot, written for a language-model-based assistant, that sets the role and tone, restricts answers to the provided knowledge, requires saying "I don't know" and offering a human when the content does not cover a question, forbids inventing policies, prices or promises, defines allowed actions and their verification steps, and includes the escalation triggers.
7. Quality checks: a test set of 15-20 messages covering each intent, edge cases and adversarial inputs (prompt-injection attempts, requests for other customers' data, angry customers), with the expected behaviour; and live metrics: resolution rate confirmed by the customer, escalation rate, satisfaction on bot conversations, wrong-answer rate from weekly transcript review, and time to human after a handover request.
8. Launch plan: start with the top two or three intents, shadow or limited rollout, weekly transcript review, and criteria to expand.
</task>

<constraints>
- Answers must be grounded in the help content given. Never invent policies, prices, timelines or features.
- A customer must always be able to reach a human (or leave a message when no one is available) within two turns of asking.
- Actions that change accounts, money or personal data require verification and are listed with the checks needed.
- Regulated or sensitive topics (health, financial hardship, legal claims, safety) go to humans by default.
- If the constraints mention a specific platform, describe the design generically and mark platform-specific settings as "check in your tool".
</constraints>

<output_format>
## Automation scope
Table: Contact reason | Volume | Decision | Reason.
## Intent map
Table: Intent | Example phrasings | Info to collect | Clarifying question.
## Grounded answers
Per intent: answer text and source.
## Escalation triggers
## Handover design
## Bot instructions
A copyable system prompt in a code block.
## Quality checks
Test-set table: Message | Expected behaviour. Then live metrics.
## Launch plan
## Content gaps
</output_format>
