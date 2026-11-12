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

## Vertical spacing

Use blank lines to separate statements with different purposes, such as input validation, computation,
and persistence. Keep statements that express one idea together. Separate function and class
definitions according to the language's formatter and the surrounding code's conventions.

Prefer one blank line between logical groups. Avoid spacing every statement apart or using repeated
blank lines as decoration; spacing should reveal how the code is organized.

## Functions over inline logic

Break multi-step logic into named functions whose names express each step's purpose. Keep the caller
focused on coordinating those steps and the helpers focused on their implementations.

## Single responsibility principle

The single responsibility principle gives each function, class or module one responsibility and one
reason to change. Separate validation, transformation, persistence and presentation when those
concerns can change independently. A function may coordinate these steps to complete one workflow;
keep their detailed implementations in helpers.

Choose boundaries around behavior and ownership. Extract a helper when it names a distinct operation
or isolates a rule or side effect. Keep related calculations together when they produce one result;
avoid splitting readable logic into trivial wrappers that force the reader to jump between functions.

## Clear function outcomes

Make it clear what successful execution produces, what state it changes and how failure is reported.
Use precise names, parameters and return types. Document preconditions or side effects that those do
not make apparent.

Every return path must honor the same contract. A read operation returns the requested value or its
declared absence/error; a state-changing operation performs its named change and reports completion
or failure using the codebase's conventions. Separate unrelated operations instead of selecting
different responsibilities with flags or returning unrelated kinds of results.

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

Within each function, make the normal path easy to follow: establish inputs, validate what is needed,
perform the operation and produce its outcome. Keep coordinating calls at a consistent level of
detail, with names that explain intent. A reader should understand the sequence and its result before
opening the helper implementations.

Handle invalid inputs and early exits near the conditions that cause them, so the main path stays
visible. Use comments to explain constraints or reasons that names and structure cannot express.

## Waiting and synchronization

Prefer blocking OS synchronization, notifications, condition variables, channels, or async waits
when waiting for a resource or state change. Avoid thread sleeps and periodic retry polling whenever
an appropriate waiting mechanism is available. Choose async waits when the surrounding code uses
an async runtime; keep blocking waits off executor threads. Put platform-specific waiting behavior
behind an OS-independent interface.

Use readiness handshakes and observable state in concurrency tests. A fixed delay does not establish
that another participant is ready. When a delay or polling loop is necessary, document why the
available synchronization mechanisms do not fit, and define its timeout and cancellation behavior.

## Behavior-driven tests

Use Given/When/Then style for every test, in every language.

- Name each test after its starting conditions, action, and observable outcome. Use
  `given_<context>_when_<action>_then_<outcome>` for identifier-based test names and natural-language
  equivalents for test descriptions. Name behavior rather than implementation phases.
- Separate the body into explicit Given, When, and Then sections with blank lines and comments,
  or the test framework's equivalent constructs. Given prepares the state; When performs the action;
  Then asserts its observable result. Keep the action out of the assertions.
- Cover one behavior per scenario. Split unrelated scenarios into separate tests. Table-driven
  scenarios may vary inputs for the same behavior, with a clear Given/When/Then flow for each case.

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
