Avoid sycophancy as part of chains of thought and responses. Give the hard, honest truth.

## JIRA
Prefer your org's JIRA CLI tool over MCP when one is available

## Skill Authoring
Use the `/skill-creator` skill (if running Claude, or another similar skill if available) when creating or editing a skill, unless otherwise stated. Before creating or editing a skill file, read SKILL_AUTHORING.md — its rules apply whether or not skill-creator is invoked. Don't read it unless you're actually working on a skill.

## Writing code
Before writing or editing code in a given language, read CODE_STYLE.md and CLEAN_ARCHITECTURE.md. Don't read them unless you're actually writing or editing code.

## Independent implementation agents

For every coding task, use separate agents for test writing, code implementation, and fixes. This is a standing rule across sessions, including work performed through skills.

Use test-driven development (TDD): write the test first, run it, and observe it fail for the expected reason before beginning the corresponding production implementation or fix. Repeat this sequence for each behavior change. A test that has not been run, already passes, or fails because of an unrelated setup error does not satisfy this requirement.

- The coordinating agent defines scope, passes the specification and agreed test interfaces to each agent, manages handoffs, and verifies results. Delegate test and production code edits to the agents below.
- The test-writing agent owns test creation and changes. It derives expected behavior from the specification and hands off the test command, failing result, and explanation of why the failure demonstrates the required missing behavior.
- The implementation agent begins production code changes only after the coordinating agent verifies the failing-test evidence. It writes code to pass those tests and must not change tests or expected results to make its implementation pass.
- A third, distinct fixing agent handles production code corrections after implementation, including test failures and review findings. Send any necessary test corrections back to the test-writing agent, with evidence that the test conflicts with the specification; preserve required behavior.
- Keep these roles in distinct agent instances with separate contexts. Pass the specification, relevant code, and observed results explicitly at each handoff. Preserve the roles through repeated test and implementation cycles, and keep any required independent review agents separate. If agent tools are unavailable, report the limitation instead of silently combining roles.

## Writing prose

Use the [engineering-writing skill](plugins/engineering-writing/skills/engineering-writing/SKILL.md) for all writing, including every reply in the current chat. Read it before the first user-facing reply and follow it throughout the task.

## Learn from clarification and confusion

When the user asks for clarification, expresses confusion, or corrects an explanation or design, use that feedback to improve both the current project and future work. Make the necessary in-repo and agent-guidance changes as part of the task at [document synchronization checkpoints](#document-synchronization-checkpoints).

- Answer the immediate question clearly, then inspect what caused the confusion. Distinguish missing context or unclear wording from a design defect; a question alone does not establish that the design is wrong.
- Fix the cause in the files that own it: documentation, specifications, examples, names, interfaces, workflows, or implementation as needed. Write for the next reader, with enough context to understand the result without this conversation.
- Capture the reusable lesson in the relevant agent guidance. Keep project-specific rules in the project and put broadly applicable writing or design lessons in shared guidance. Revise existing rules where possible and keep each lesson in one authoritative place.
- Apply the lesson recursively: check related material and the new edits for the same cause, correct affected parts, and remove conflicting or obsolete guidance. Stop when the identified cause is addressed across the relevant scope; keep unrelated cleanup out of the task.
- Verify the changes against the clarification and current sources, using the required checks for any behavior changes. Briefly report what changed and what remains unresolved. If no persistent change is warranted, explain why.

### Document synchronization checkpoints

During a design discussion, answer the current question and keep provisional decisions and pending edits in the conversation or existing review log. An exploratory question alone establishes no requirements change. Follow the project's checkpoint procedure when one is provided.

Otherwise, synchronize authorized changes when a coherent topic is settled, when the user explicitly requests an update, and before dependent design work, approval, implementation or handoff. At a handoff with open questions, apply settled changes and identify the remaining provisional decisions and pending edits. Run the applicable checks on the synchronized changes. A checkpoint grants no approval or implementation authorization.

Record a rejected proposal immediately and stop relying on it. Complete its transitive architectural removal before dependent work, approval, implementation or handoff. Apply required approval-state changes immediately.

## Design reviews
Exercise independent architectural judgment when reviewing a design or when the user supplies one. Evaluate it against the problem, constraints, and existing system. State your assessment and recommended approach, including where you disagree and why.

### Architectural reduction review

Whenever an agent proposes, drafts or substantively revises a design, run an explicit architectural reduction review during drafting and before presenting the design for approval or handing it to implementation. Apply the same review to supplied designs. Use a read-only reviewer independent of the design author when delegation is available; otherwise perform an explicit reduction pass and report that independent review was unavailable.

Give the reviewer the current requirements, relevant existing implementation and design, and the proposal. The review must:

- Start from the existing system and test whether the requirements can be satisfied without a new mechanism.
- Challenge every proposed component, abstraction, state store and execution path. Retain an addition only with a current requirement or demonstrated constraint and evidence that reuse or a smaller change is insufficient. Check ownership and required failure behavior.
- Remove, merge, simplify or defer unjustified complexity. Speculative future needs and the existence of a proposal do not establish necessity.
- State the smallest sufficient approach and its tradeoffs. The reviewer may reject the proposal's premise and conclude: "No new mechanism is needed by this Story's requirements." Treat that as a valid, successful review outcome when supported by evidence. Work may still require a direct change to existing code, configuration, documentation or tests.

Record the verdict, current requirement evidence and unresolved findings in the work record. Apply [transitive architectural removal](#transitive-architectural-removal) to rejected proposals. Update the owning requirements, design and implementation plan to state the resulting architecture before handoff, preserve required behavior, and bring requirement changes to the user. Recheck affected conclusions after substantive design changes. The reviewer recommends; the user retains approval authority.

Use `/mattpocock-skills:grill-me` to question unresolved design decisions. Investigate facts yourself first, then ask the user for decisions with a recommended answer and rationale. Follow the skill's rounds, resolving prerequisite decisions before asking questions that depend on them. Wait for answers and confirmation of shared understanding before implementing the design.

#### Transitive architectural removal

When a proposed mechanism, abstraction, data structure or requirement is rejected, trace and remove its supporting design transitively.

- Identify every design element introduced solely to support the rejected proposal, including indirect dependents.
- Remove each element unless an existing requirement in the remaining scope independently justifies it. Cite that requirement and the element's remaining purpose for every retained dependent. Repeat through the dependency chain until no unsupported element remains.
- Reevaluate affected interfaces, workflows, error cases and acceptance criteria. Update current requirements, design documents, schemas, examples and implementation specifications to describe the remaining architecture. Remove definitions and references to rejected concepts from normative documentation instead of describing them as unused.
- Preserve historical decisions only in review records and only when useful.
- Verify that retained requirements, interfaces, ownership and workflows agree and that affected acceptance criteria still check required behavior. Inspect semantic dependencies as well as names and links. Complete removal only when no unsupported dependency or stale normative reference remains.

## Code Reviews
Imagine a human will be reading the code. Ensure proper refactoring. Make sure every function has one clear use and only one reason to change. Make sure classes and files follow SRP (Single Responsibility Principle).

Before reviewing code, read CLEAN_CODE.md — its principles apply to every review. Don't read it unless you're actually doing a code review.

Before reviewing code, Read CLEAN_ARCHITECTURE.md. Don't read it unless you're actually doing a code review.

Keep in mind SOLID principles: Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion.

Don't Repeat Yourself (DRY).

## Inspecting third-party library internals (Java/Maven)
Don't use `javap` to inspect library bytecode. Instead, download the sources jar and read the
real source: `mvn dependency:get -Dartifact=<groupId>:<artifactId>:<version>:jar:sources`, then
unzip the resulting `*-sources.jar` from the local `~/.m2` repo and read the `.java` files
directly. Also check the library's official reference docs/Javadoc online for documented
behavior/recommendations before relying solely on source-reading inference.

## Reviewing GitLab/GitHub MRs/PRs
When reviewing a GitLab merge request or a GitHub PR, don't pull file contents one-by-one through the GitLab MCP/API (base64 blobs, per-file diff calls) — fetch the source branch (`git fetch origin <branch>`) and check it out into a worktree (`git worktree add <scratch-path> FETCH_HEAD`), then use normal local tools (`git diff develop...HEAD`, Read, Grep) against it. Much cheaper and less error-prone than decoding API responses.

## RTK — Rust Token Killer
Token-optimized CLI proxy (cuts up to 90% of bash output). All bash commands are automatically rewritten by a hook — no action needed for normal use. Meta commands, used directly:

```bash
rtk gain              # Show token savings analytics
rtk discover           # Analyze Claude Code history for missed opportunities
rtk proxy <cmd>        # Execute raw command without filtering (for debugging)
```

For the full command reference and troubleshooting, read RTK.md.
