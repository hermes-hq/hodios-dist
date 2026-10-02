<context>
A model decides which tool to call, and with what arguments, from the tool's name, description and parameter schema alone. Agents misbehave when tools overlap so the model guesses between them, when one tool per REST endpoint forces long brittle call chains, when parameters are free-form strings the model has to invent a format for, when results are huge raw payloads, and when errors are bare status codes that give the model nothing to correct. Tools are an interface for a reader that is literal and cannot ask questions, so they need more explanation than an API for humans, not less.
</context>

<task>
Design the tools for these capabilities:
[CAPABILITIES]

1. List the user goals the agent must reach. Map them to the smallest set of tools with distinct, non-overlapping purposes. Combine steps that are always done together into one tool, and do not mirror the existing API one to one; say which endpoints each tool combines.
2. For each tool write:
   - a `verb_noun` name in snake_case, with a shared prefix when tools belong to one service;
   - a description of three to six sentences: what it does, when to use it, when not to use it and which tool to use instead, what it returns, and any side effects;
   - an input JSON Schema: `type: object`, a description on every property, enums for closed sets, explicit formats in the description (dates as ISO 8601, amounts in minor units), sensible defaults, a minimal `required` list and `additionalProperties: false`;
   - the output shape: only fields the model needs next, stable ids it can pass to other tools, and truncation or pagination for large results with a note telling the model how to get more;
   - side effects: read-only, idempotent, or destructive. Destructive or costly tools take an explicit confirmation or `dry_run` parameter and say so in the description.
3. Define the errors each tool can return. Every error message tells the model what went wrong and what to do next, for example "No customer matches 'Jon Smiht'. Call search_customers with a partial name."
4. Write 6 to 10 selection tests: a user request and the expected tool call with arguments, including near misses where no tool or a different tool should be used.
5. If a capability is too vague to define a safe tool, ask about it instead of guessing.
</task>

<constraints>
- Use a portable JSON Schema subset: `type`, `properties`, `required`, `enum`, `items`, `description`, `default`, `minimum`, `maximum`, `maxLength`. Avoid `$ref`, top-level `oneOf` or `anyOf`, and conditional schemas, which some providers reject.
- Never put credentials, tenant ids or authorisation decisions in parameters. The host application supplies identity and enforces permissions.
- Keep the set under about 15 tools unless the capabilities truly need more, and say why if they do.
- Do not invent endpoints or fields of the existing API. Mark anything you assumed.
</constraints>

<output_format>
## Tool set
Table: name | purpose | side effects | wraps.

## Definitions
One fenced JSON array of tool objects with `name`, `description` and `input_schema`, followed by each tool's output shape.

## Error catalogue
Table: tool | condition | message returned to the model.

## Selection tests
Numbered: user request, then the expected call or "no tool".

## Notes
Assumptions and open questions.
</output_format>
