---
name: document-public-api
description: Writes reference docs for a module's exported functions, classes or endpoints in the native doc-comment format, covering real behaviour, errors and edge cases. Use before a release.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: docs
  source: https://hermes-ide.com/prompts/document-public-api
  catalog: 2026.1002.2
---

# Document a public API

## Inputs

- [TARGET] (required): The module, package, file, class or set of endpoints to document.
- [FORMAT] (optional; one of: inline, reference; default: inline): Where the docs go. inline writes doc comments in the code; reference writes a separate Markdown reference page.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
API reference is read by someone about to call the code. They need what the signature cannot say: what each parameter means and which values are valid, what comes back in each case, what can fail and how, and what the call changes besides its return value. Restating the type signature in prose wastes their time; describing the behaviour the author intended instead of the behaviour the code has misleads them.
</context>

<task>
Document the public API of [TARGET] as [FORMAT] docs.

1. Find the public surface: exported symbols, `__all__`, `pub` items, capitalised Go identifiers, public classes and methods, or routes in the router or OpenAPI spec. Skip private and internal helpers.
2. For each symbol, read its implementation, its callers and its tests before writing. Check the existing doc comments for conventions.
3. Document, for each symbol:
   - a one-line summary that says what it does, starting with a verb;
   - each parameter: meaning, valid range or format, units, default and what happens with null, empty or out-of-range values;
   - the return value in each case, including empty results;
   - errors, exceptions or error codes, and the condition for each;
   - side effects (I/O, mutation of arguments, global state, network, caching), concurrency or async behaviour, and notable cost;
   - a short example taken or adapted from the tests, when the usage is not obvious.
4. Use the native format for the language: TSDoc or JSDoc, Python docstrings in the style the project already uses (Google, NumPy or reST), rustdoc, Go doc comments, Javadoc or KDoc, XML docs for C#, or OpenAPI descriptions for HTTP endpoints. For `reference`, write one Markdown page grouped by module with the same content.
</task>

<constraints>
- Describe what the code does, not what the name suggests. If they differ, or the behaviour looks like a bug, document the actual behaviour and list it under "Behaviour worth reviewing". Do not change the code.
- Never invent parameters, defaults, error types or examples. If behaviour depends on code you cannot see, say so in "Questions for the author".
- Do not repeat information the type system already states (do not write "@param name - the name, a string").
- Edit only doc comments or the reference page. No reformatting, renaming or refactoring.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
</constraints>

<output_format>
Apply the documentation edits. Then reply with:
## Changes
The symbols you documented, one line each.
## Questions for the author
Behaviour you could not determine from the code, as questions.
## Behaviour worth reviewing
Places where the code's behaviour looks surprising or inconsistent with its name, each with `path:line`. Write "None" if there are none.
</output_format>
