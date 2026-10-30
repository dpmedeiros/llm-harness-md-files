# Code Style

Rules for writing and refactoring code, across any language unless otherwise specified. These are
defaults for general-purpose/backend/script code with no established convention of its own. Where a
codebase already has one — a framework idiom, an existing lint config, a pattern already dominant in
the surrounding files — follow that instead of overriding it with these defaults.

Language-specific rules live in their own file under `code-style/`. Before writing or editing code
in a given language, read that language's file if one exists (e.g. `code-style/javascript.md` for
JavaScript/TypeScript) — its rules apply on top of the ones below. Don't read a language's file
unless you're actually working in that language.

## Line width
Keep lines to 120 characters as much as possible.

## Functions over inline logic

Break multi-step logic into named functions. Each function does one thing; name it for what it does.
The caller should read as a sequence of named steps, not an inlined mix of logic and orchestration.

## Named functions over anonymous ones for reusable logic

Give any named, reusable unit of logic a proper named-function declaration rather than assigning an
anonymous or lambda function to a variable — including a block that only closes over outer state
because it was never given explicit parameters; prefer passing that state in explicitly so the
function can stand alone. Trivial inline callbacks passed to a single transform (map/filter/find/
reduce or the language's equivalent) are the exception: inline brevity for a one-expression
transform is a real advantage, a named multi-statement block hiding behind an anonymous-function
variable is not.

Per-language files give the concrete syntax for this rule and any framework-idiomatic exemptions
(e.g. `code-style/javascript.md` for React/Vue).

## Nesting

No more than one level of `if`/`for`/`while` nesting inside any function. A loop containing one
`if`, or a loop containing one more loop, is the limit. Where logic would nest deeper, extract the
inner piece into its own named function instead of adding another level.

## Always brace control flow

In languages with brace-delimited blocks, every `if`/`else` and every `for`/`while` is followed by a
`{ }` block, even for a single statement. No `if (x) doThing()`, no `for (...) doThing()`.

## Top-to-bottom readability

A script or module's executable body — the part below all function/const/schema definitions —
reads as a sequential story: resolve inputs, validate, do the steps, return. No function or schema
definitions interleaved into that body. Push every reusable or multi-statement piece of logic up
into a named function defined above it, parameterized rather than closing over body-local state, so
it can live with the other definitions instead of sitting in the middle of the flow.

## Unit tests for new scripts

Every new script gets unit tests in the same change, whatever the language: Python, shell, JS, hook
scripts, one-off tooling. Put them wherever the repo keeps its tests, in the repo's test framework.
Cover the decision logic with real inputs, including the cases that must not trigger. Keep the
script's logic in importable functions so tests can call them without running the whole script.
When a script can't be tested as written, restructure it until it can.

## Linter/smell findings: verify before complying

When a static-analysis tool (Sonar, ESLint, etc.) flags something, check whether the suggested fix
is actually safe for the code's real constraints before applying it — a generic rule doesn't know
this codebase's data dependencies, shared mutable state, or caching/replay semantics. If the finding
doesn't apply here, suppress it with a comment explaining why, rather than applying a mechanical fix
that introduces a bug. E.g. `await` inside a loop gets flagged as inefficient with a suggestion to
gather promises for `Promise.all`, but is correct to leave sequential when a later iteration depends
on an earlier one's result, or when the awaited calls mutate shared state/files that would conflict
if run concurrently.
