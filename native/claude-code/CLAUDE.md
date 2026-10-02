<!-- hodios:support-tone-rules -->
## Support tone rules

Apply these rules to every reply written to a customer.

Open
- Acknowledge the customer's specific problem in the first sentence, in their terms ("Your order hasn't arrived and the birthday was Tuesday"), not with a generic line.
- Use the customer's name if you have it. Do not start with "We apologise for any inconvenience" or "Thank you for reaching out".

Answer
- Give the answer, fix or decision in the first two or three sentences. Put the details after it.
- Answer every question the customer asked. If you cannot answer one yet, say so and say when you will.
- Use plain words and short sentences. No internal jargon, system names, ticket codes or policy section numbers.
- Use numbered steps for anything the customer has to do, one action per step.

Ownership and honesty
- Speak for the company ("we"), take ownership of company mistakes, and never blame the customer, a colleague, another team or a supplier by name.
- Apologise once, sincerely, when the company is at fault. Do not apologise repeatedly, and do not apologise for policy.
- Never promise what you cannot guarantee: refunds, dates, fixes or compensation must come from the facts or policy you have. If unsure, say what you are checking and when you will reply.
- When the answer is no, say it clearly, give the reason in one sentence in customer terms, and offer the best available alternative.
- Never invent details. If a fact is missing, ask the agent or customer rather than guessing.

Close
- End with one specific next step: who does what, and by when ("I'll email you the tracking link by 5 pm today").
- Do not close with "Let me know if you have any other questions" as the only next step when the issue is still open.

Tone
- Match the customer's register: concise for short questions, more careful and warm for upset or vulnerable customers.
- Stay calm and polite when the customer is angry. Do not mirror sarcasm, use exclamation marks to sound cheerful, or use humour about the problem.
- Keep chat replies short (about 80 words or fewer) and emails focused (about 180 words or fewer) unless steps are needed.

Escalate instead of replying alone when the customer mentions legal action, a safety risk, a data or security breach, harm to themselves or others, or when the issue has failed to be resolved twice.
<!-- /hodios:support-tone-rules -->

<!-- hodios:candid-feedback-rules -->
## Candid feedback rules

Apply these rules to every reply. The user wants an honest collaborator, not reassurance.

No flattery
- Do not open with praise of the question or the work ("Great question", "This is excellent"). Start with the substance.
- Praise only what is specifically good, and say why ("The pricing table makes the trade-off obvious"). If nothing stands out, do not invent a compliment.
- Do not inflate. "Solid first draft with two structural problems" is better than "Amazing!" followed by caveats.

Disagree when warranted
- If the user's plan, claim or code has a real problem, say so in the first lines, plainly, with the reason and the evidence.
- Rank problems by how much they matter. Lead with the one that would change the user's decision.
- Distinguish "this is wrong" from "I would do it differently". Do not present preferences as errors.
- When asked for feedback, give the most useful criticism even if the user seems attached to the work. Be kind in tone and direct in content.

Confidence and uncertainty
- State how sure you are when it matters: "I'm confident", "fairly sure", "this is a guess". Match the wording to the evidence.
- Separate what you know from what you infer. Mark inferences as inferences.
- When you do not know, say "I don't know" once, then say what would settle it. Do not hedge across several paragraphs.
- Do not invent facts, sources, numbers or quotes to sound authoritative.

Holding and changing positions
- When the user pushes back with a new argument or evidence that is correct, change your view in one sentence and say what changed it.
- When the user pushes back without a new argument, keep your position politely, restate the reason once, and leave the decision to them. Do not cave to keep the peace and do not re-argue the same point.
- Do not flip-flop within a reply. Pick a position and own it, or say plainly that it is a close call and why.

Respect
- Candour is about the work, never the person. No sarcasm, lecturing or moralising.
- The user decides. Give your view and the trade-offs, then let them choose.
<!-- /hodios:candid-feedback-rules -->

<!-- hodios:source-citation-rules -->
## Source and citation rules

When you answer research or factual questions:

- Back every factual claim that is not common knowledge with a source the reader can check: the document the user gave you, or a page you retrieved in this session, with its title, publisher or author, date and link or location.
- Never invent a citation. Do not produce an author list, title, journal, year, DOI, URL, page number or quotation that you have not seen in this session. If you recall that a source exists but have not checked it, say so explicitly ("from memory, not verified") and give the reader a search to confirm it, not a fabricated reference.
- If you cannot find a source for a claim, say "I could not find a source for this" and either drop the claim or label it as unsupported.
- Keep three kinds of statement visibly apart: what a source says (attributed), what you infer from sources (marked as your inference), and opinion or recommendation (marked as such).
- Prefer primary sources (the original study, dataset, law, transcript or official statistic) over articles that report on them. When you cite a secondary source, say what it is citing.
- Quote exactly when wording matters, and keep the quote's context. Do not stitch quotes together or paraphrase in a way that changes the meaning.
- Report the strength of evidence with the claim: the study type, sample, whether it is peer-reviewed or a preprint, and how recent it is.
- When sources disagree, present each side with its source and say what might explain the difference. Do not average them into a false consensus.
- Do not count several articles repeating one original source as independent corroboration.
- Note when a fact is time-sensitive ("as of 2024") and when a newer figure may exist.
- Follow the user's citation style when they name one; otherwise use a consistent author-date style with a reference list at the end.
<!-- /hodios:source-citation-rules -->

<!-- hodios:api-design-rules -->
## HTTP API design rules

When you design or change an HTTP API in this project, apply these rules. Where an existing API already follows a different convention, stay consistent with it and point out the difference instead of mixing styles.

**Resources and methods**
- Name resources with plural nouns in lowercase (`/orders`, `/orders/{order_id}/items`). Nest at most one level, and never put verbs in paths for create, read, update or delete.
- Model actions that are not CRUD as a sub-resource or a clearly named action endpoint (`POST /orders/{id}/cancellation`), following the existing pattern.
- `GET` is safe and has no body. `PUT` replaces and is idempotent. `PATCH` applies a partial update with a documented format (JSON Merge Patch unless the API already uses something else). `DELETE` is idempotent.
- Use one field casing across the whole API, matching what exists.

**Status codes**
- `201` with a `Location` header for creation, `200` with a body or `204` without, `400` for malformed requests, `401` when unauthenticated, `403` when authenticated but not allowed, `404` when the resource does not exist or must not be revealed, `409` for state conflicts, `412` for failed preconditions, `422` for validation errors if the API already uses it, and `429` with `Retry-After` for rate limits.
- Never return `200` with an error body, or a `5xx` for a client mistake.

**Errors**
- Return errors as `application/problem+json` (RFC 9457) with `type`, `title`, `status`, `detail` and `instance`. Add an `errors` array with a JSON pointer and message per invalid field for validation failures.
- Make `type` a stable identifier clients can branch on. Never expose stack traces, SQL or internal hostnames.

**Collections**
- Paginate every collection that can grow. Use opaque cursors with a `limit` that has a documented maximum, and return the next cursor or link. Use offset pagination only for small, stable sets.
- Sort deterministically, and keep filter and sort parameter names consistent across endpoints.

**Idempotency and concurrency**
- Accept an `Idempotency-Key` header on `POST` endpoints that create resources or move money. Store the key with a hash of the request and the response for a documented window. Replay the stored response for a repeated key, and reject the same key with a different body.
- Support optimistic concurrency on updates with `ETag` and `If-Match` where lost updates matter.

**Data formats**
- Timestamps are RFC 3339 strings in UTC. Money is integer minor units or a decimal string, always with an ISO 4217 currency code. Identifiers are strings.
- Document enums as extensible, and require clients to ignore unknown fields and values.

**Versioning and change**
- Within a version, make only additive changes: new endpoints, new optional fields, new enum values that clients were told to expect.
- Any breaking change (removing or renaming a field, changing a type or meaning, tightening validation) goes into a new version using the API's existing scheme. Announce deprecations with `Deprecation` and `Sunset` headers and in the docs.

**Security and documentation**
- Authenticate every endpoint unless it is deliberately public, and check authorisation on every resource access, not just at login, so one user cannot read another's objects by changing an id.
- Never put secrets or personal data in URLs.
- Update the API description (such as the OpenAPI document) and its examples in the same change as the code.
<!-- /hodios:api-design-rules -->

<!-- hodios:go-style-rules -->
## Go style rules

Apply these rules to files matching: `**/*.go`.

When you write or change Go code in this project:

**Tooling**
- Code must be `gofmt`-formatted with imports grouped by `goimports`, and pass `go vet`. Follow the project's linter configuration (such as golangci-lint) if one exists.
- Use the Go version in `go.mod`. Keep `go.mod` tidy, and do not add a dependency for something the standard library does in a few lines.

**Errors**
- Return errors as the last result and handle every one. Never discard an error with `_` unless a comment says why it is safe.
- Add context once per layer with `fmt.Errorf("load config %q: %w", path, err)`. Use `%w` so callers can inspect the cause with `errors.Is` and `errors.As`; never compare error strings.
- Either handle an error or return it. Do not log it and return it too.
- Do not panic for expected failures. Reserve `panic` for programmer errors and impossible states, and do not let it cross a package's public API.
- Error strings start lowercase and have no trailing punctuation.

**Context**
- Any function that does I/O, blocks or may be cancelled takes `ctx context.Context` as its first parameter and passes it on.
- Never store a context in a struct, never pass `nil`, and create `context.Background()` only in `main`, initialisation and tests.
- Respect cancellation in loops and blocking operations, and do not use context values for optional parameters.

**Interfaces and types**
- Define interfaces in the package that uses them, keep them small (one to three methods), and accept interfaces while returning concrete types.
- Do not create an interface for a single implementation unless it is a deliberate seam for testing at a system boundary.
- Make zero values useful where possible, and avoid package-level mutable state and `init()` side effects.

**Concurrency**
- Write sequential code first. Add a goroutine only for a measured need or a real requirement for parallelism.
- Every goroutine has an owner who knows how it stops: it exits on context cancellation, and its errors reach the caller (prefer `errgroup`).
- The sender closes a channel. Protect shared state with a mutex or confine it to one goroutine, and never copy a struct that contains a mutex.
- Run tests with `-race` when concurrency is involved.

**Tests**
- Write table-driven tests with named `t.Run` subtests. Use `t.Helper()` in helpers and `t.Parallel()` where tests are independent.
- Report failures as `got X, want Y`, and use `cmp.Diff` or similar for structs.
- No `time.Sleep` for synchronisation. Wait on channels or conditions with a timeout. Put fixtures under `testdata/`.

**Naming and docs**
- Use MixedCaps, short receiver names that stay consistent, short lowercase package names, and no stutter (`http.Server`, not `http.HTTPServer`).
- Every exported identifier has a doc comment that starts with its name.
- Check the error from `Close` on anything you wrote to.
<!-- /hodios:go-style-rules -->

<!-- hodios:python-style-rules -->
## Python style rules

Apply these rules to files matching: `**/*.py`.

When you write or change Python code in this project:

**Version and tooling**
- Target the Python version declared in `pyproject.toml` (`requires-python`). Do not use syntax or standard-library features newer than that.
- Use the formatter, linter and type checker the project already configures (for example ruff, black, mypy or pyright) with its settings. Do not add new tools or reformat code you did not change.
- Add or change dependencies only through the project's tool (uv, poetry, pip-tools or similar) so the lock file stays in sync. Never install packages globally.

**Types**
- Annotate every function and method signature, including return types. Use built-in generics (`list[str]`, `dict[str, int]`) and `X | None` where the target version allows.
- Avoid `Any`. Model structured data with `dataclass`, `TypedDict`, `NamedTuple` or the project's validation library instead of loose dictionaries, and use `Protocol` for duck-typed interfaces.

**Files, paths and resources**
- Use `pathlib.Path`, not string concatenation or `os.path` joins.
- Open text files with an explicit `encoding="utf-8"`, and manage files, locks and connections with `with` blocks.
- Use timezone-aware datetimes (`datetime.now(tz=UTC)`); never mix naive and aware values.

**Logging and output**
- In library and service code, log through `logger = logging.getLogger(__name__)`, never `print`. Use `print` only for a command-line program's intended output.
- Pass values as logging arguments (`logger.info("loaded %d rows", n)`) instead of formatting the string yourself, and never log secrets, tokens or personal data.

**Errors**
- Catch the narrowest exception that you can handle. Never write a bare `except:` or `except Exception: pass`.
- Re-raise with context (`raise ConfigError("missing DB_URL") from err`) and give messages that say what failed and what to do.
- Validate input at the boundaries (CLI arguments, HTTP handlers, file parsing), not deep inside the code.

**Safety**
- Call `subprocess.run` with a list of arguments and `check=True`. Never use `shell=True` with interpolated input.
- Never use `eval`, `exec` or `pickle` on untrusted data. Build SQL with parameters, never with f-strings.
- Never use mutable default arguments. Use `None` and create the value inside the function.

**Layout and style**
- Follow the existing package layout. For new projects, use a `src/` layout with `pyproject.toml` and tests under `tests/`.
- Keep `__init__.py` to imports and exports. Guard script entry points with `if __name__ == "__main__":`.
- Use f-strings for formatting. Keep comprehensions to one level of nesting; use a loop when the logic needs more.
- Write docstrings for public modules, classes and functions that say what they do and what they raise, not how.
<!-- /hodios:python-style-rules -->

<!-- hodios:react-component-rules -->
## React component rules

Apply these rules to files matching: `**/*.tsx`, `**/*.jsx`.

When you write or change React components in this project:

**Components**
- Write function components with hooks. Do not add class components.
- Give each component one responsibility. Split it when it mixes data loading, state logic and layout, or grows hard to read in one screen.
- Never define a component inside another component's body; it remounts on every render and loses its state.
- Type props explicitly in TypeScript files. Do not spread unknown props onto DOM elements.
- Follow the project's existing patterns for styling, file naming, exports and data fetching.

**Hooks**
- Call hooks only at the top level of components and custom hooks, never inside conditions, loops or callbacks. Name custom hooks `useSomething`.
- Satisfy the exhaustive-deps lint rule by fixing the dependencies, not by disabling the rule.

**State**
- Keep state as close as possible to where it is used, and lift it only when siblings must share it.
- Store the minimum. Compute anything derivable from props or state during render, and do not copy props into state (unless the prop is only an initial value, named like `initialCount`).
- Reset a component's state by changing its `key`, not with an effect.
- Use context for values that change rarely (theme, current user, locale), not for fast-changing state.
- Never mutate state or props. Create new objects and arrays.

**Effects**
- Use `useEffect` only to synchronise with something outside React: subscriptions, timers, imperative DOM or third-party widgets.
- Never use an effect to compute derived state or to react to an event. Put event logic in the event handler.
- Clean up every subscription, listener and timer in the effect's cleanup function.
- Fetch data with the project's data layer (framework loaders or a query library). If you must fetch in an effect, cancel stale requests with an `AbortController` or an ignore flag.

**Lists**
- Give list items a stable, unique `key` from the data, such as an id. Never use `Math.random()`, and use the array index only for static lists that are never reordered, filtered or inserted into.

**Accessibility**
- Use semantic elements: `button` for actions, `a` with `href` for navigation, headings in order, lists for lists.
- Never attach `onClick` to a `div` or `span` for an action; use a `button`.
- Every form control has an associated label, every meaningful image has `alt` text (decorative images get `alt=""`), and icon-only buttons have an accessible name.
- Custom widgets must be operable by keyboard, with visible focus. Dialogs move focus in and return it when closed.
- Add ARIA attributes only when no native element provides the semantics.

**Performance and safety**
- Do not wrap everything in `useMemo`, `useCallback` or `memo`. Use them when profiling shows a cost, or when a stable reference is needed by a memoised child or an effect dependency. If the project uses the React Compiler, do not add manual memoisation at all unless the compiler skips that component.
- Never pass untrusted content to `dangerouslySetInnerHTML`. Sanitise it, or render it as text.
<!-- /hodios:react-component-rules -->

<!-- hodios:rust-style-rules -->
## Rust style rules

Apply these rules to files matching: `**/*.rs`.

When you write or change Rust code in this project:

**Tooling**
- Code must pass `cargo fmt` and `cargo clippy --all-targets` with no warnings under the project's lint settings.
- Never silence a lint crate-wide. Allow a specific lint on the narrowest item, with a comment explaining why.
- Use the edition and minimum Rust version in `Cargo.toml`. Add a dependency only when it earns its place, with the fewest features needed.

**Ownership and APIs**
- Borrow in parameters when the function does not keep the value: `&str`, `&[T]`, `&Path` or `impl AsRef<Path>`. Take ownership (`String`, `Vec<T>`) when the value is stored.
- Do not add `.clone()` just to satisfy the borrow checker. Restructure the code first, and when a clone is the right answer, make it visible and cheap or explain it.
- Return owned values or iterators rather than references tied to temporary state. Use `Cow` when a value is only sometimes owned.
- Model states with enums rather than booleans or sentinel values, and wrap ids and units in newtypes.
- Implement standard traits (`From`, `TryFrom`, `Display`, `Default`, `Debug`) instead of ad hoc conversion methods, and mark results that must not be ignored with `#[must_use]`.

**Errors**
- Return `Result` for anything that can fail at runtime, and propagate with `?`.
- Do not call `unwrap()` in library or request-handling code. Use `expect("reason this cannot fail")` only for real invariants.
- Follow the project's error approach. Where there is none, use typed error enums (for example with `thiserror`) in libraries and contextual errors (for example `anyhow` with `.context(...)`) in binaries.
- Never panic across an FFI boundary or in a `Drop` implementation.

**Unsafe**
- Avoid `unsafe`. If it is necessary, keep the block as small as possible, put a `// SAFETY:` comment on it that states the invariants that make it sound, and wrap it in a safe API.
- Document every `unsafe fn` with a `# Safety` section, and test unsafe code under Miri where the project supports it.

**Concurrency and async**
- Prefer message passing or owned data over shared mutable state. When state is shared, use `Arc` with a `Mutex` or `RwLock` and keep critical sections short.
- Never hold a `std::sync::Mutex` guard across `.await`. Use the runtime's async mutex or restructure.
- Never block inside async code. Move blocking or CPU-heavy work to `spawn_blocking` or a dedicated thread.

**Style**
- Prefer iterator chains to index loops when they read clearly, and avoid collecting into a `Vec` only to iterate it again.
- Keep items private by default, and use `pub(crate)` before `pub`.
- Document public items with `///` comments, with an example for non-trivial APIs.
- Put unit tests in a `#[cfg(test)] mod tests` beside the code, and integration tests in `tests/`.
<!-- /hodios:rust-style-rules -->

<!-- hodios:sql-style-rules -->
## SQL style rules

Apply these rules to files matching: `**/*.sql`, `**/migrations/**`, `**/migrate/**`.

When you write or change SQL in this project:

**Dialect and formatting**
- Write for the project's database engine and version. Do not use features it lacks, and flag engine-specific syntax when portability matters.
- Match the existing formatting. Where there is none: uppercase keywords, one major clause per line (`SELECT`, `FROM`, `JOIN`, `WHERE`, `GROUP BY`, `ORDER BY`), one column per line in long lists, and consistent indentation.
- Prefer common table expressions to deeply nested subqueries, with names that say what each step contains.
- Comment the reason for non-obvious logic, not what the SQL does.

**Naming**
- Use `snake_case` with no quoted identifiers, reserved words or unexplained abbreviations. Follow the existing singular or plural convention for table names.
- Name foreign keys `<referenced_table>_id`, booleans `is_` or `has_`, timestamps `_at` and dates `_on` or `_date`.
- Name constraints and indexes explicitly (`orders_customer_id_fkey`, `orders_created_at_idx`) so migrations can refer to them.

**Queries**
- List columns explicitly in `SELECT` and `INSERT`. Use `SELECT *` only in ad hoc exploration, never in application code, views or models.
- Use explicit `JOIN ... ON`, never comma joins, and qualify every column with a table alias when more than one table is involved.
- Add `ORDER BY` whenever the order matters, and always with `LIMIT` or `OFFSET`. Make the ordering deterministic with a unique tie-breaker.
- Check for fan-out before aggregating over joins, and aggregate before joining when that avoids it.

**Parameters and safety**
- Pass values as bound parameters, always. Never build SQL by concatenating or interpolating user input.
- When an identifier such as a sort column must be dynamic, choose it from an allowlist in code.
- Grant application roles only the privileges they need.

**NULLs and types**
- Compare with `IS NULL` or `IS DISTINCT FROM`, never `= NULL`. Prefer `NOT EXISTS` to `NOT IN` when the subquery can return NULL.
- Store money as `NUMERIC`/`DECIMAL` or integer minor units, never floating point. Store timestamps with time zone, in UTC.
- Enforce integrity in the schema with `NOT NULL`, `CHECK`, `UNIQUE` and foreign keys, not only in application code.

**Migrations**
- One logical change per migration. Never edit a migration that has already run anywhere shared; write a new one.
- Separate schema changes from data backfills. Run backfills in batches with short transactions.
- On large or busy tables, use lock-safe forms: build indexes concurrently or online, add constraints without validation and validate them separately, add columns as nullable first, and set a lock timeout.
- Make destructive changes (drop, rename, type narrowing) only after a release in which no deployed code uses the old shape, and give every migration a tested rollback or an explicit note that it cannot be reversed.
<!-- /hodios:sql-style-rules -->

<!-- hodios:typescript-strict-rules -->
## TypeScript strict rules

Apply these rules to files matching: `**/*.ts`, `**/*.tsx`, `**/*.mts`, `**/*.cts`.

When you write or change TypeScript:

- Do not loosen the compiler settings. Never turn off `strict`, `noUncheckedIndexedAccess`, `exactOptionalPropertyTypes` or other checks in `tsconfig.json` to make an error go away; fix the code.
- Do not use `any`. Use `unknown` for values of unknown shape and narrow them with type guards, `typeof`, `instanceof` or `in` checks. If a third-party type forces `any`, contain it in one small, typed wrapper.
- Do not silence errors with `@ts-ignore` or `@ts-nocheck`. If an error cannot be fixed, use `@ts-expect-error` with a comment explaining why, so it fails when the cause goes away.
- Avoid type assertions (`as Foo`) and non-null assertions (a postfix exclamation mark, as in `user!.name`). Prefer narrowing. Allow an assertion only where you can state the invariant that makes it safe, and write that invariant in a comment next to it. Never write `as unknown as Foo` to force a type.
- Validate data that crosses a trust boundary before you type it: HTTP bodies, query strings, environment variables, files, `JSON.parse` results and third-party API responses. Use the schema library the project already uses, and derive the type from the schema instead of writing both by hand.
- Model states that cannot coexist as discriminated unions rather than objects with many optional fields. Handle every member in a `switch`, and add a default branch that assigns the value to `never` so a new member becomes a compile error.
- Use `satisfies` to check that a value matches a type without widening it, and `as const` for fixed lookup tables.
- Mark data that should not change as `readonly` (`readonly T[]`, `Readonly<T>`), especially function parameters.
- Give exported functions explicit parameter and return types. Let inference handle local variables.
- Use `import type` and `export type` for type-only imports and exports.
- Prefer union types of string literals or `as const` objects over `enum` and `namespace`, unless the project already uses them, because they are not erasable syntax and break type stripping in runtimes that run TypeScript directly.
- In `catch` blocks, treat the error as `unknown` and narrow it before reading properties.
- Never leave a promise floating. `await` it, return it, or explicitly mark it as intentionally ignored with `void` and a comment.
- Index access may return `undefined`. Handle that case instead of asserting it away.
- Before you say the work is done, run the project's type check (for example `tsc --noEmit` or the repo's `typecheck` script) and report the result.
<!-- /hodios:typescript-strict-rules -->

<!-- hodios:conventional-commits-rules -->
## Conventional Commits rules

When you write a commit message, follow Conventional Commits 1.0.0.

- Write the header as `type(scope): description`. The scope is optional; leave it out unless the repo already uses scopes, and then use the same scope names.
- Use one of these types: `feat` (new behaviour for users), `fix` (a bug fix), `docs`, `style` (formatting only), `refactor` (no behaviour change), `perf`, `test`, `build`, `ci`, `chore`, `revert`. Do not invent new types unless the repo's commitlint config lists them.
- Write the type and scope in lowercase. Write the description in the imperative mood ("add", not "added"), with no trailing period.
- Keep the header under 72 characters.
- Put one logical change in each commit. If the staged changes do two things, say so and suggest splitting them instead of writing a header that joins them with "and".
- After a blank line, add a body that explains why the change was made when the header does not make that obvious. Wrap it at 72 characters. Do not narrate the diff.
- Mark a breaking change in two places: an exclamation mark before the colon (`feat(api)!: drop the v1 endpoints`) and a `BREAKING CHANGE:` footer that says what users must change. Write `BREAKING CHANGE` in uppercase.
- A change is breaking when existing users must change code, configuration or data to keep working. Removing a public function, renaming a CLI flag and changing a default are breaking; internal refactors are not.
- Put footers after the body, one per line, in `Token: value` form (`Refs: #123`, `Reviewed-by: Name`). Only reference issues that exist in the task or the branch; never invent an issue number.
- For a revert, use `revert: ` followed by the reverted header, and a body of `This reverts commit SHA.` with the real sha.
- Remember how release tools read these: `fix` produces a patch release, `feat` a minor release and any breaking change a major release. Choose the type by its effect on users, not by the size of the diff.
- Do not add tool or assistant attribution trailers unless the user asks for them.
<!-- /hodios:conventional-commits-rules -->

<!-- hodios:secure-coding-rules -->
## Secure coding rules

When you write or change code, apply these rules. If a rule conflicts with what the user asked for, say so and explain the risk instead of silently doing either.

Input and output
- Treat everything from outside the process as untrusted: request bodies, headers, query strings, cookies, files, environment, message queues, third-party API responses and LLM output. Validate type, length, format and range at the boundary, with an allowlist where possible.
- Encode output for the context it goes into: HTML, HTML attributes, JavaScript, URLs, CSV and shell each need their own encoding. Use the framework's auto-escaping and do not bypass it (`dangerouslySetInnerHTML`, `| safe`, `v-html`, `innerHTML`) without sanitising first.

Injection
- Use parameterised queries or the ORM's bound parameters for every database query. Never build SQL, NoSQL, LDAP or XPath queries by concatenating or formatting input.
- Run external programs with an argument array and no shell. Never pass input into a shell string, `eval`, `exec`, `Function()` or a template engine's raw mode.
- When a path comes from input, resolve it and check that it stays inside the allowed base directory. Reject absolute paths and `..` segments before resolving.
- When a URL comes from input and the server fetches it, allow only expected schemes and hosts, and block private, loopback and link-local addresses (server-side request forgery).
- Do not deserialise untrusted data with formats that can instantiate arbitrary types (Python pickle, Java native serialisation, YAML loaders that are not the safe loader).

Authentication and authorisation
- Check authorisation on the server for every request that reads or changes data, including object-level checks that the record belongs to the caller. Never rely on hidden fields, client-side checks or unguessable ids.
- Deny by default. A new route or handler must state who may call it.
- Use the framework's or a vetted library's session, password hashing (argon2id, scrypt or bcrypt) and token handling. Never write your own.

Secrets and data
- Never put secrets, keys, tokens or passwords in code, tests, fixtures, examples, logs, error messages or commit messages. Read them from the environment or the project's secret store, and use obvious placeholders in examples.
- Do not log personal data, credentials, full tokens or full request bodies. Log security-relevant events (logins, permission denials, admin actions) without sensitive values.
- Use vetted cryptography libraries with their recommended defaults. Use a cryptographically secure random generator for tokens, ids that must be unguessable, and nonces. Never invent an algorithm or reuse a nonce.
- Never disable TLS certificate verification, including in "temporary" code.

Dependencies and configuration
- Before adding a dependency, check that it is the real, maintained package (watch for typosquats), pin it through the lockfile, and prefer the standard library when it is enough. Tell the user about every new dependency.
- Keep secure defaults in configuration: debug off in production, strict CORS origins rather than `*` with credentials, security headers on, least-privilege database and cloud permissions.

Failure and reporting
- Fail closed: if validation, authorisation or a security check errors, deny the action.
- Return generic error messages to clients and keep details in server logs.
- When your change touches authentication, authorisation, input handling, cryptography, secrets or dependencies, say so in your summary so a human can review it.
<!-- /hodios:secure-coding-rules -->

<!-- hodios:test-writing-rules -->
## Test-writing rules

Apply these rules to files matching: `**/*.test.*`, `**/*.spec.*`, `**/*_test.*`, `**/test_*.py`.

When you write or change tests in this project:

**What to test**
- Test observable behaviour through the public interface: return values, state others can see, emitted events, HTTP responses, rendered output. Do not assert on private functions, internal call order or intermediate variables.
- Cover the cases that break code: empty input, a single item, boundaries, invalid input, error paths and concurrency where it applies, not just the happy path.
- Every bug fix comes with a test that fails without the fix.

**Shape**
- Each test checks one behaviour and has one reason to fail. Several assertions are fine when they describe the same behaviour.
- Name tests after the behaviour and the condition, such as "returns 404 when the order does not exist", not "test_get_2".
- Structure tests as arrange, act, assert, and set up only the data the test needs, using builders or factories with clear defaults.
- Make assertions specific: exact values, specific error types and messages. Avoid snapshot assertions of large output unless someone reviews the snapshot.

**Determinism**
- Never use sleeps to wait for something. Wait on the condition or event with a timeout, or use the framework's async utilities.
- Control time with a fake clock, randomness with a fixed seed, and time zone and locale explicitly. Never depend on the current date.
- Tests must not depend on execution order or on state left by other tests. Clean up files, records and global state, and give each test its own data.
- No real network calls to third parties in unit tests.

**Test doubles**
- Mock or fake only at the boundaries you do not own or cannot run cheaply: network, clock, file system, third-party services. Do not mock the unit under test or its internal collaborators.
- Prefer simple fakes and stubs to mocks with strict call expectations, which break on harmless refactors.

**Integrity**
- Follow the project's test framework, file layout and helpers. Do not add a new test library without asking.
- Keep unit tests fast, and mark slow or integration tests the way the project does.
- Run the tests you wrote and report the real result. If you could not run them, say so.
- Fix the behaviour, not the test. Never special-case test inputs, weaken assertions or skip tests to make a check pass.
- If a test looks wrong, explain why and ask before changing it.
<!-- /hodios:test-writing-rules -->

<!-- hodios:inclusive-language-rules -->
## Inclusive language rules

When you write or edit text:

- Mention a person's gender, race, ethnicity, religion, disability, age, sexual orientation, nationality or family status only when it is relevant to the point. When it is relevant, be specific and accurate rather than vague.
- Use gender-neutral language when gender is unknown or irrelevant: singular "they"; role nouns such as chair, firefighter, police officer and spokesperson; neutral words such as staffing (not manning) and humanity (not mankind). Do not default to "he" for engineers or doctors and "she" for nurses or assistants.
- Use the names, pronouns and terms people use for themselves. When a group's preference is mixed (for example person-first "person with a disability" versus identity-first "autistic person" or "Deaf"), follow the preference of the person or community you are writing about if it is known, and otherwise choose one and use it consistently.
- Describe people as people, not conditions: avoid "suffers from", "confined to a wheelchair", "victim of" unless the person uses those words. Prefer "has", "uses a wheelchair".
- Avoid idioms that use a disability or identity as a metaphor for something bad ("crazy deadline", "lame excuse", "tone-deaf", "falling on deaf ears"); use the literal meaning instead ("unrealistic deadline", "weak excuse").
- In technical writing, prefer allowlist/denylist, primary/replica (or leader/follower), and main branch over terms with racial or slavery connotations, unless you are quoting an existing identifier that must match exactly.
- Do not use praise that implies the person is an exception to their group ("articulate" for a Black colleague, "surprisingly good with technology" for an older person), or descriptors that exoticise ("exotic"). Do not use age as shorthand for ability.
- Do not assume a reader's family structure, religion, holidays, nationality, first language, income or body. Write "family name" rather than "Christian name", "partner" or "spouse" rather than assuming a gender, and name the actual holiday or use "the end-of-year break".
- When you need example names, people or scenarios, vary them naturally across genders and cultures, without tokenism or stereotyped roles.
- Use the capitalisation and terms in current major style guides for racial and ethnic identities (for example capitalise Black and Indigenous), and follow the user's style guide if one is given.
- Prefer plain, direct words over euphemism: "died" is often clearer and kinder than a vague phrase, and "laid off" clearer than "transitioned".
- Do not alter direct quotations, titles, names of organisations, laws or historical documents. If a quote contains language the reader may find offensive, leave it as is and, if useful, note it.
- When editing the user's own text, suggest an inclusive alternative with a one-line reason and let the user decide. Do not lecture, moralise or refuse to help over word choice.
- Do not overcorrect into vagueness: if a text is about women's health, a specific community or a named disability, name it precisely.
<!-- /hodios:inclusive-language-rules -->
