---
description: Produces an ordered response plan for an exposed API key, token or password, from revocation and rotation to usage audit and prevention. Use right after a secret is committed, logged or shared.
---

# Respond to a leaked secret

## Inputs

- [SECRET_KIND] (required): What leaked, without the value. For example "AWS access key", "GitHub fine-grained token", "Stripe live secret key", "Postgres password".
- [EXPOSURE] (required): Where and how it leaked, since when, and who could see it. For example "pushed to a public GitHub repo 2 hours ago, force-pushed away 10 minutes later".
- [USED_BY] (optional): Services, environments or people that use this secret today, if you know.

Read each value from the arguments below. If a required value is missing, ask for it once.

<context>
A secret that left its intended boundary must be treated as compromised. Automated scanners pick up keys from public repositories within minutes, and deleting the commit, force-pushing or making the repo private does not undo the copies already made. The only real fix is to make the leaked value useless, then find out whether anyone used it.
</context>

<task>
A [SECRET_KIND] was exposed: [EXPOSURE]
Only if [USED_BY] was provided: 
It is used by: [USED_BY]

Write the response plan.
1. Rate the severity from what the secret can do (its scopes and permissions), how public the exposure was, and for how long.
2. Order the steps so the leaked value is revoked first. Where revoking it at once would cause an outage, say so and give the fastest safe order: create a second credential, deploy it, then revoke the old one, with a time limit on that window.
3. If the repository is available, search it for every place the secret is read (environment variable names, config keys, secret manager paths) so the rotation misses no consumer. List the places you found.
4. Say how to check whether the secret was used during the exposure window: which audit or access logs this kind of credential has, what to filter on, and what unexpected use looks like.
5. Cover history clean-up as optional hygiene, after revocation, and say what it does not fix.
6. Recommend the two or three controls that would have prevented this specific leak.
</task>

<constraints>
- Never ask for the secret's value. If the user pasted it, tell them in the first line that it is now exposed in this conversation too and must be rotated regardless.
- Never present deleting the commit, rewriting history or making a repository private as a fix.
- Give exact console paths or CLI commands only when you are sure of them for this provider. Otherwise name the provider's official documentation page to follow. Do not invent flags.
- Do not run or recommend any command that changes production. The user runs the steps.
- Keep it short enough to follow during an incident: imperative sentences, one action per line.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Severity
One line: critical, high, medium or low, and why (what an attacker could do with it).

## Do now
Numbered steps for the next 15 minutes, revocation first.

## Rotate
Numbered steps to issue the new secret and update every consumer, with the consumers found in the repo.

## Investigate
Which logs to check, the time window, the filter, and what counts as suspicious use.

## Clean up
History and cache clean-up, marked optional, with what it does and does not achieve.

## Prevent
Two or three controls, each tied to how this leak happened.

## Unknowns
Facts you need from the user that would change the plan. "None" if none.
</output_format>

Arguments: $ARGUMENTS
