---
name: explain-stack-trace
description: Explains an error and its stack trace in plain words, finds the frame that matters, and ranks the likely causes with the next checks to run. Use when an exception or crash is hard to read.
license: CC0-1.0
metadata:
  version: 1.0.0
  kind: prompt
  category: debugging
  source: https://hermes-ide.com/prompts/explain-stack-trace
  catalog: 2026.1002.1
---

# Explain a stack trace

## Inputs

- [TRACE] (required): The full error message and stack trace, including any "Caused by" or chained exceptions.
- [CONTEXT] (optional): What you were doing when it happened, and anything that changed recently.

Take each value from the invocation or the user’s message. If a required value is missing, ask for it once.

<context>
Stack traces are long, and most of their frames belong to frameworks and libraries. The useful information is usually three things: the real exception (often the innermost one in a chain), the first frame in the project's own code, and the value that was wrong when it got there. Each runtime prints these differently.
</context>

<task>
Explain this error:
[TRACE]
Only if [CONTEXT] was provided: 
Context: [CONTEXT]
1. Identify the language or runtime from the trace format, and read the trace in that runtime's order:
   - Python prints the most recent call last, so the failing line is at the bottom.
   - Java, Kotlin and C# put the outermost exception first; the root is the last "Caused by" or inner exception.
   - JavaScript and TypeScript traces may be cut at async boundaries and may point to compiled files; say when a source map is needed.
   - Go panics list each goroutine; the panicking goroutine comes first. Rust panics need `RUST_BACKTRACE=1` for a full trace.
2. Find the root exception and its message. Say what it means in one plain sentence.
3. Find the first frame in the project's own code, as opposed to the standard library, a framework or a dependency. If the project's code is available, read that line and the lines that feed it.
4. Reason backwards from that line: which value or state must have been wrong for this error to happen, and where could it have come from?
5. Rank the likely causes and give the cheapest check that confirms or rules out each one.
</task>

<constraints>
- Do not guess at code you have not seen. If the project's code is not available, base the explanation on the trace alone and say so.
- Quote frames exactly as they appear in the trace. Never invent file names, line numbers or function names.
- Ignore framework and library frames unless the error originates inside one. If it does, say whether the likely fault is still the caller's input.
- If the trace is truncated or minified so that the cause cannot be found, say what is missing and how to get it.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
- Lead with the answer. Add reasoning only where it changes what the reader will do.
- No preamble, no restating the request and no closing summary on a short answer.
</constraints>

<output_format>
## What happened
One or two plain sentences: the root exception and what it means.
## Where
The frame that matters, quoted from the trace, and why that frame.
## Likely causes
Numbered, most likely first. Each cause with the evidence for it.
## Next checks
Bullets: one concrete check per cause (a value to print, a line to read, a command to run).
</output_format>
