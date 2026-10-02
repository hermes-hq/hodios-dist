<context>
`terraform apply` does what the plan says, not what the author meant. Outages from infrastructure as code usually come from lines nobody read in a long plan: a database marked for replacement because one attribute changed, a bucket destroyed by a renamed resource, or drift that the apply silently reverts. Your job is to read every line so the person applying does not have to guess.
</context>

<task>
Review this plan for the unknown environment.


[PLAN]

1. Count the actions: create, update in place, replace (destroy then create, or create then destroy) and destroy. Check your counts against the plan's own summary line.
2. List every destroy and replace. For each, name the attribute that forces replacement if the plan shows it, and say whether the resource holds state or traffic (databases, volumes, buckets, DNS records, load balancers, encryption keys, IAM roles in use, queues).
3. Flag security exposure: ingress open to `0.0.0.0/0` or `::/0`, public buckets or ACLs, IAM policies with wildcard actions or resources, encryption or logging turned off, deletion protection removed.
4. Compare every change against the intent. Changes the intent does not explain are likely drift, a provider upgrade or a mistake; list them.
5. Note values that are `(known after apply)` on attributes other resources depend on, and any sensitive values the plan prints in clear text.
6. Give the checks to run before applying: backups or snapshots to take, `moved` blocks or state moves that would turn a replace into an in-place change, `lifecycle` settings such as `prevent_destroy` or `create_before_destroy`, and whether to split the apply.
</task>

<constraints>
- Report only what is in the plan. Never invent resources, attributes or values.
- If the plan is truncated or you cannot tell whether an action is a replace, say so and treat it as a replace.
- Quote resource addresses exactly as they appear (`module.db.aws_db_instance.main`).
- Do not suggest running apply or any state-changing command yourself.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Verdict
One line: `apply`, `apply-with-care` (state the condition) or `do-not-apply`, and the main reason.

## Summary
`N to add, N to change, N to replace, N to destroy`, and whether it matches the plan's summary.

## Dangerous changes
Numbered, most dangerous first: resource address — action — why it is dangerous — how to make it safe. "None" if empty.

## Unexpected changes
Changes the intent does not explain, each with its likely cause. "None" if empty or if no intent was given.

## Before you apply
A short checklist of concrete actions.
</output_format>
