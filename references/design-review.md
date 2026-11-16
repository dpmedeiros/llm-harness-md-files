# Design reduction and removal

## Architectural reduction review

Whenever an agent proposes, drafts or substantively revises a design, run an explicit architectural reduction review during drafting and before presenting the design for approval or handing it to implementation. Apply the same review to supplied designs. Follow the project's reduction and transitive-removal procedures when provided; otherwise use the procedure below. Use a read-only reviewer independent of the design author when delegation is available; otherwise perform an explicit reduction pass and report that independent review was unavailable.

Give the reviewer the current requirements, relevant existing implementation and design, and the proposal. The review must:

- Start from the existing system and test whether the requirements can be satisfied without a new mechanism.
- Challenge every proposed component, abstraction, state store and execution path. Retain an addition only with a current requirement or demonstrated constraint and evidence that reuse or a smaller change is insufficient. Check ownership and required failure behavior.
- Remove, merge, simplify or defer unjustified complexity. Speculative future needs and the existence of a proposal do not establish necessity.
- State the smallest sufficient approach and its tradeoffs. The reviewer may reject the proposal's premise and conclude: "No new mechanism is needed by this Story's requirements." Treat that as a valid, successful review outcome when supported by evidence. Work may still require a direct change to existing code, configuration, documentation or tests.

Record the verdict, current requirement evidence and unresolved findings in the work record. Apply [transitive architectural removal](#transitive-architectural-removal) to rejected proposals. Reconcile the owning requirements, design and implementation plan at the project's synchronization boundary before approval or implementation handoff, preserve required behavior, and bring requirement changes to the user. Recheck affected conclusions after substantive design changes. The reviewer recommends; the user retains approval authority.

Use `/mattpocock-skills:grill-me` to question unresolved design decisions. Investigate facts yourself first, then ask the user for decisions with a recommended answer and rationale. Follow the skill's rounds, resolving prerequisite decisions before asking questions that depend on them. Wait for answers and confirmation of shared understanding before implementing the design.

## Transitive architectural removal

When a proposed mechanism, abstraction, data structure or requirement is rejected, trace and remove its supporting design transitively.

- Identify every design element introduced solely to support the rejected proposal, including indirect dependents.
- Remove each element unless an existing requirement in the remaining scope independently justifies it. Cite that requirement and the element's remaining purpose for every retained dependent. Repeat through the dependency chain until no unsupported element remains.
- Reevaluate affected interfaces, workflows, error cases and acceptance criteria. Update current requirements, design documents, schemas, examples and implementation specifications to describe the remaining architecture. Remove definitions and references to rejected concepts from normative documentation instead of describing them as unused.
- Preserve historical decisions only in review records and only when useful.
- Verify that retained requirements, interfaces, ownership and workflows agree and that affected acceptance criteria still check required behavior. Inspect semantic dependencies as well as names and links. Complete removal only when no unsupported dependency or stale normative reference remains.
