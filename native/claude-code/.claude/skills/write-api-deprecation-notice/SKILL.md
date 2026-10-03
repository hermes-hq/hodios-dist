---
name: write-api-deprecation-notice
description: Writes the notice to API consumers for a deprecation or breaking change, covering what changes, the timeline, migration steps and where to get help. Use before announcing an API change.
license: CC0-1.0
arguments:
  - change
  - dates
  - channel
  - support
argument-hint: <change> <dates> [channel] [support]
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: writing
  source: https://hermes-ide.com/prompts/write-api-deprecation-notice
  catalog: 2026.1003.2
---

# Write an API deprecation notice

## Inputs

- `change` (required): What is being deprecated or changed, why, what replaces it, and who is affected (endpoints, fields, SDK versions, auth methods).
- `dates` (required): Key dates such as the announcement, deprecation, brownouts and removal or sunset, with time zone if relevant.
- `channel` (optional; one of: email, changelog-post, docs-banner, all; default: all): Where the notice will be published, which sets its length and shape.
- `support` (optional): Where consumers get help, such as a forum, support email, migration office hours or an issue tracker.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A deprecation notice is read by a busy developer who maintains an integration they wrote a year ago. They need to answer three questions in under a minute: does this affect me, what exactly must I change, and by when. Notices fail when they lead with the company's reasons, bury the date, say "some endpoints" instead of naming them, or promise a migration path that is not documented yet. A good notice is specific, scannable and calm, and every date and step in it can be acted on.
</context>

<task>
Write the consumer notice for this change:
<change>
$change
</change>
Dates: $dates
Channel: $channel
Only if support was provided: 
Support: $support

1. Extract the facts: what is affected (exact endpoints, fields, parameters, SDK or API versions, auth methods), what replaces each, the behaviour after the removal date (error code, ignored field, redirect), and every date. If an essential fact is missing (what is removed, the replacement, or the removal date), list it under "Missing information" and use a clearly marked placeholder such as `[REMOVAL DATE]` rather than inventing it.
2. Write the full notice in this order:
   - A subject or headline that names the API and the action and date, for example "Action required by 2027-03-31: Orders API v1 is being retired".
   - Who is affected, and how a consumer can tell whether they are (a request header, a dashboard filter, a log query, an SDK version check).
   - What changes, as a before and after table for each affected item.
   - The timeline as a dated list: announcement, deprecation (still works, now marked deprecated with Deprecation and Sunset headers if the API uses them), any brownouts, removal. State the exact behaviour after removal.
   - Migration steps, numbered, each one concrete, with a short request or code snippet where the change is mechanical and a link placeholder to the full migration guide.
   - Why, in two sentences at most, after the steps.
   - Where to get help and how to request an extension, if extensions are possible.
3. Produce the short versions for $channel: "email" gets an email of at most 150 words with the date in the subject line; "changelog-post" gets a changelog entry that links to the full notice; "docs-banner" gets a one-sentence banner for the affected reference pages; "all" gets all three.
4. Add a sender checklist of what must exist before the notice goes out.
</task>

<constraints>
- Lead with the action and date, not the backstory. No marketing language and no "we're excited".
- Name every affected item exactly as it appears in the API; never say "some endpoints" or "certain fields".
- Write dates in an unambiguous format (2027-03-31, or 31 March 2027) with a time zone when a time is given.
- Do not promise extensions, credits, SDK releases or support that the input does not mention.
- If the timeline gives consumers less than 90 days for a breaking change to a public API, say so in the sender checklist as a risk, without changing the dates.
- Keep the tone respectful of the consumer's time: acknowledge the work you are asking for once, without apologising repeatedly.
</constraints>

<output_format>
## Missing information
Bullets of facts you could not find and the placeholders used, or "None".
## Notice
The full notice in Markdown, ready to publish.
## Short versions
The email, changelog entry and docs banner required by the channel, each under its own bold label.
## Sender checklist
Checkboxes: migration guide published, replacement live and documented, deprecation headers or SDK warnings shipped, affected consumers identified and contacted directly, support staffed, brownout and removal dates in the team calendar, plus any risks.
</output_format>
