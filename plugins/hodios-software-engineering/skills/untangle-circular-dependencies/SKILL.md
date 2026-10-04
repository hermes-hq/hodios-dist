---
name: untangle-circular-dependencies
description: Finds circular dependencies between modules and plans breaking each cycle with interfaces, inversion or extraction in safe steps. Use when import cycles cause build errors or tangled code.
license: CC0-1.0
arguments:
  - dependency_info
argument-hint: <dependency_info>
disable-model-invocation: true
metadata:
  version: 1.0.1
  kind: prompt
  category: refactoring
  source: https://hermes-ide.com/prompts/untangle-circular-dependencies
  catalog: 2026.1004.1
---

# Untangle circular dependencies

## Inputs

- `dependency_info` (required): The cycle report or import graph (from a tool such as madge, dependency-cruiser, import-linter, jdeps or a compiler error), plus the relevant import lines or files; or a repository path if the assistant can read it.

Arguments fill these in order. If a required value is empty, take it from the user’s message or ask for it once.

<context>
A dependency cycle means two or more modules cannot be understood, tested, built or deployed apart. Cycles cause import-order bugs (a value undefined at load time), slow incremental builds and modules that can never be extracted. The fix is rarely "move the import inside the function"; that hides the cycle. The real fix depends on why the edge exists: a shared type that belongs lower down, a callback that should be inverted, a misplaced function, or two modules that are really one. The right break is the edge that is least essential, chosen so that dependencies point from volatile, high-level code toward stable, low-level code.
</context>

<task>
Analyse these dependencies:
<dependency_info>
$dependency_info
</dependency_info>

1. List every cycle as a path (`a → b → c → a`). If the input is a large graph, list the strongly connected components and the shortest cycles inside each. If you can read the repository, confirm each edge by finding the import and what it uses; otherwise mark edges you could not confirm.
2. For each edge in a cycle, record what crosses it: types only, a function call, a constant, a class to instantiate, a registry or event. Note whether the use is at load time (top-level) or at call time.
3. Diagnose each cycle and pick a technique:
   - **Move down:** a shared type, constant or pure helper used by both belongs in a lower module (often a new `types`, `contracts` or `shared` module). Keep that module free of dependencies on its users.
   - **Invert:** the lower module calls back into the higher one. Define an interface or callback in the lower module and have the higher module provide the implementation (dependency injection, a port, an event).
   - **Move the function:** one function is in the wrong module; moving it removes the edge.
   - **Merge:** the modules change together and share invariants; merge them, then split along a better seam later if needed.
   - **Extract:** both depend on a cohesive piece that should become its own module.
   State why you chose the technique over the others, and which direction the dependency will point afterwards.
4. Order the work so each step compiles, passes tests and could ship alone. Break the cheapest, most-shared edges first. For each step give the files touched, the change, and a small code sketch in the project's language for non-obvious moves.
5. Propose a guardrail that fails CI if a cycle returns: a rule for the project's tool (dependency-cruiser `no-circular`, import-linter contracts, ArchUnit, eslint `import/no-cycle`, Go's compiler already forbids package cycles) or a layered-architecture rule that also fixes the intended direction.
</task>

<constraints>
- Do not propose lazy or in-function imports, `require` inside functions, or forward-declaration tricks as the fix. Mention them only as a temporary unblocker, labelled as such.
- Type-only imports (TypeScript `import type`, Python `if TYPE_CHECKING:`) are a legitimate fix when the edge carries types and nothing else: they remove the runtime cycle and its load-order bugs. Say that the design-level coupling remains, and whether the cycle tool will still report the edge (check its type-only setting).
- Keep behaviour identical; this is a refactor. Flag any step that could change load order or initialisation side effects.
- Do not rename or restructure beyond what breaking the cycles needs.
- Base the analysis on the edges given or read; never invent modules or imports.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
- Separate what you verified from what you inferred. Mark inferences as such.
- When you do not know, say "I don't know" once and state what would settle it.
</constraints>

<output_format>
## Cycles found
Numbered cycle paths, with what crosses each edge and whether it is load-time or call-time.
## Diagnosis
Per cycle: the edge to break, the technique, why, and the dependency direction afterwards. Include a Mermaid `graph LR` showing before and after for the largest cycle.
## Break plan
Numbered steps, each independently shippable: files, change, code sketch where needed, how to verify.
## Guardrail
The CI rule or configuration, in a fenced block.
## Questions
Anything you need to confirm, or "None".
</output_format>
