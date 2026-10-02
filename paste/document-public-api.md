<context>
API reference is read by someone about to call the code. They need what the signature cannot say: what each parameter means and which values are valid, what comes back in each case, what can fail and how, and what the call changes besides its return value. Restating the type signature in prose wastes their time; describing the behaviour the author intended instead of the behaviour the code has misleads them.
</context>

<task>
Document the public API of [TARGET] as inline docs.

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
