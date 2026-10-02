<context>
A README is read in about thirty seconds by someone deciding whether this project solves their problem, and then followed step by step by someone trying to run it. Both readers are failed by the same things: a vague first sentence, an install step that does not work, an example that uses an option that no longer exists. Every fact in a README must come from the repository, because a confident wrong command costs the reader more than a missing one.
</context>

<task>
Write the README for the repository in the working directory, mainly for users.

1. Gather facts before writing. Read the existing README (if any), the package manifests (for the name, description, runtime and version requirements, scripts and binaries), entry points, `--help` output or the CLI parser, example and test files, the license file, the CI config and any CONTRIBUTING file.
2. Write the opening: the project name and one sentence that says what it does and for whom, specific enough that a reader can rule it in or out.
3. Install: the real command for each supported package manager or platform, with prerequisites and minimum versions taken from the manifests.
4. Quick start: the shortest sequence that produces a visible result, copied from a test, example or the CLI definition. If you can run commands, run it from a clean state and fix the README until it works.
5. Usage: the main options or API in a table or short sections, generated from the source, not from memory. Link to fuller docs if they exist instead of duplicating them.
6. For contributors: how to set up, run the tests and lint, taken from the scripts and CI.
7. Finish with license (from the license file) and where to get help, only if the repo shows those channels.
8. If a README already exists, keep its accurate content and voice, fix what is wrong, and fill gaps. Do not rewrite sections that are correct.
</task>

<constraints>
- Every command, flag, default, version and URL must come from the repository or the notes. Mark anything you cannot confirm with `TODO(author): ...` instead of guessing.
- Do not add badges, benchmarks, logos, comparisons or testimonials that the repository does not already provide.
- No marketing language (simple, blazing fast, seamless, powerful, easy) and no emoji unless the existing README uses them.
- Code blocks have a language tag; commands have no shell prompt so they paste cleanly.
- Keep it scannable: the quick start should be visible without much scrolling.
- Do only what was asked. If you notice something else worth changing, mention it in one line at the end instead of changing it.
- Keep the change as small as it can be while still being correct.
</constraints>

<output_format>
Write `README.md` (or edit the existing one). Then reply with:
1. A list of the commands you ran to check the quick start and their real results, or "Not run" and why.
2. Every `TODO(author)` you left, as a checklist.
3. Any place where the existing docs disagreed with the code, and which one you followed.
</output_format>
