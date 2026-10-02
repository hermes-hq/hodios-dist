---
name: write-property-based-tests
description: Finds the invariants a function must keep and writes property-based tests with generators that shrink well. Use when example-based tests miss edge cases in parsers, encoders or pure logic.
license: CC0-1.0
arguments:
  - code
  - framework
argument-hint: <code> [framework]
disable-model-invocation: true
metadata:
  version: 1.0.0
  kind: prompt
  category: testing
  source: https://hermes-ide.com/prompts/write-property-based-tests
  catalog: 2026.1002.1
---

# Write property-based tests

## Inputs

- `code` (required): The function, module or file to test, pasted or as a path.
- `framework` (optional): Property-testing library to use, for example Hypothesis, fast-check, proptest, jqwik or QuickCheck. Detected from the repo when left empty.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
Property-based tests state a rule that must hold for every valid input and let a generator search for a counterexample, then shrink it to the smallest failing case. They find the bugs example tests miss, but only when the property is genuinely true of the specification (not a restatement of the implementation) and the generators produce valid, varied, shrinkable inputs. A property that re-implements the function proves nothing; a generator that filters away 90% of its draws is slow and shrinks badly.
</context>

<task>
Write property-based tests for:
$code

Library: Only if framework was provided: $framework. If no library is named, detect it from the project's manifests and existing tests (Hypothesis for Python, fast-check for JavaScript and TypeScript, proptest for Rust, jqwik for Java, FsCheck for .NET, rapid for Go; the standard library's testing/quick is frozen and shrinks nothing). If none is installed, pick the standard one for the language and say how to add it.

1. Read the code and state its contract: valid inputs, outputs, errors it may raise, and side effects. If the contract is ambiguous (for example, what happens on empty input), ask or state the assumption you test against.
2. Find candidate properties, preferring these patterns:
   - round-trip: decode(encode(x)) == x, parse(print(x)) == x;
   - invariants: output is sorted, length preserved, total conserved, no duplicates, within bounds;
   - idempotence: f(f(x)) == f(x);
   - oracle or model: agrees with a simpler, obviously correct implementation or an in-memory model of a stateful system;
   - metamorphic: a known change to the input causes a predictable change to the output;
   - algebraic: commutativity, associativity, identity elements where the domain promises them;
   - robustness: never crashes or hangs on any input of the right type, and fails only with documented errors.
   Keep only properties that follow from the contract. Discard any that just mirror the implementation.
3. Build generators from the domain, not from raw types: construct valid values directly (map, compose, build strategies) instead of generating anything and filtering. Include the edge values the type allows: empty, single element, zero, negative, maximum sizes, Unicode beyond ASCII, NaN and infinities for floats where relevant. Bound sizes so a run stays fast.
4. Write the tests in the project's style and test runner. Make failures reproducible: rely on the library's seed reporting and example database or replay, and add any shrunk counterexample you discover as an explicit regression example.
5. If you can run the tests, do so and report the result. If a property fails, report the minimal counterexample and whether the bug is in the code or in your property. Do not change the code under test.
</task>

<constraints>
- Every property must name the contract clause it checks. No property may call the function under test to compute its own expected value.
- Avoid filter or assume calls that reject more than a small fraction of draws; restructure the generator instead.
- Keep default example counts unless there is a reason to change them, and say why if you do.
- Do not fix bugs you find; report them.
- Read the relevant code before making a claim about it. Do not guess what a file, function or config contains.
- If the information you need is not available, say what is missing and how to get it instead of inventing it.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
</constraints>

<output_format>
## Properties
Table: Property | Pattern | Contract clause it checks.
## Generators
One line per generator: what it builds and which edge values it covers.
## Tests
The complete test file in one code block, with imports.
## Counterexamples
Shrunk failing inputs with a one-line diagnosis each, or "None found" with the number of examples run. If you could not run the tests, say so.
## How to run
The exact command, including how to replay a failure from its seed.
</output_format>
