# Code Style: JavaScript / TypeScript

## No arrow-function/lambda expressions for named, reusable logic

Use `function name(...) {}`, not `const name = (...) => {}`, for anything that amounts to a named,
reusable unit of logic — including a block that only closes over outer variables because it was
never given explicit parameters; prefer passing those in explicitly so the function can stand alone.
Trivial inline callbacks passed to `.map`/`.filter`/`.find`/`.reduce` stay as arrows — that's the
exception: inline brevity for a one-expression transform is a real advantage, a named multi-statement
block hiding behind `const` is not.

Exempt: framework-idiomatic patterns. React function components (`const Foo = () => {}`) and custom
hooks (`const useThing = () => {}`) are written as arrow consts by convention — hooks in particular
are almost universally arrows, and a project's own ESLint config often enforces it. Same logic for
any other framework with its own established arrow-const idiom (Vue composition functions, etc.).
Don't rewrite idiomatic framework code to chase this rule — it exists for general-purpose logic, not
to override an ecosystem's own conventions.

## Destructured object params, but only where the risk is real

Positional parameters are fine when a wrong-order call fails loudly — a crash, or a type error at
the call site. They become a hazard when two adjacent parameters share a type (two strings, two
numbers, two arrays, two booleans): a transposed pair compiles, runs, and produces a plausible wrong
result instead of an error. That's when to switch to a destructured object parameter.

The object form works because each argument travels with its key. `fn({ ticketKey, designPath })`
is shorthand for `fn({ ticketKey: ticketKey, designPath: designPath })`: the property names come
from the identifiers, the callee destructures by name, and order inside the literal is irrelevant,
so `fn({ designPath, ticketKey })` is the same call. Getting a name wrong is a compile error in
TypeScript (missing required property, excess property), so the only way to transpose is to write
`fn({ ticketKey: designPath, designPath: ticketKey })` explicitly — which type-checks, but reads as
wrong on the page. The protection is visual rather than enforced, and that's enough: the mistake
has to be spelled out rather than slipped in.

Count is not the criterion. `indexComponentMethods(idx, components, bucket)` stays positional at
three params because an object / array index / short enum string can't be transposed into a valid
call. Converting every multi-param function to an object, adjacency or not, is the opposite mistake:
ceremony that buys nothing.

Call-site cost is usually near zero: when the caller already holds a local per field, shorthand
applies and the object adds only braces. An object parameter is also cheap to extend later — a new
optional field doesn't touch existing call sites — but that's a bonus, not the reason to use one.