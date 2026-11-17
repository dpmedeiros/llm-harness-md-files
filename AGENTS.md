Avoid sycophancy as part of chains of thought and responses. Give the hard, honest truth.

## JIRA
Prefer your org's JIRA CLI tool over MCP when one is available

## Skill Authoring
Use the `/skill-creator` skill (if running Claude, or another similar skill if available) when creating or editing a skill, unless otherwise stated. Before creating or editing a skill file, read SKILL_AUTHORING.md — its rules apply whether or not skill-creator is invoked. Don't read it unless you're actually working on a skill.

## Writing code
Before writing or editing code in a given language, read CODE_STYLE.md and CLEAN_ARCHITECTURE.md. Don't read them unless you're actually writing or editing code.

## Independent implementation agents

For every coding task, use separate agents for test writing, code implementation and fixes, including work performed through skills. Follow the project's role procedure when provided; otherwise read the [independent implementation procedure](references/implementation.md) before writing code or dispatching a coding agent.

## Writing prose

Use the [engineering-writing skill](plugins/engineering-writing/skills/engineering-writing/SKILL.md) for all writing, including every reply in the current chat. Read it before the first user-facing reply and follow it throughout the task.

## Learn from clarification and confusion

When the user asks for clarification, expresses confusion or corrects an explanation or design, read the [clarification procedure](references/clarification.md#learn-from-clarification-and-confusion) to address the cause in the project and relevant guidance.

### Document synchronization checkpoints

During a design discussion or handoff, follow the project's checkpoint procedure when provided; otherwise read the [document synchronization procedure](references/clarification.md#document-synchronization-checkpoints). A checkpoint grants no approval or implementation authorization.

## Design reviews
Exercise independent architectural judgment when reviewing a design or when the user supplies one. Evaluate it against the problem, constraints, and existing system. State your assessment and recommended approach, including where you disagree and why.

### Architectural reduction review

Before proposing, drafting or substantively revising a design, and when reviewing a supplied design, apply the project's reduction procedure when provided; otherwise read the [reduction review procedure](references/design-review.md#architectural-reduction-review). Recheck before presenting the design for approval or handing it to implementation. Use an independent read-only reviewer when available; otherwise perform an explicit reduction pass and report that independent review was unavailable. The reviewer recommends; the user retains approval authority.

#### Transitive architectural removal

When a proposed mechanism, abstraction, data structure or requirement is rejected, apply the project's transitive-removal procedure when provided; otherwise read [transitive architectural removal](references/design-review.md#transitive-architectural-removal).

## Code Reviews

Before reviewing code, read [CLEAN_CODE.md](CLEAN_CODE.md) for readability, responsibility and duplication checks and [CLEAN_ARCHITECTURE.md](CLEAN_ARCHITECTURE.md) for SOLID principles, component responsibilities and dependency rules. Apply those guides to the actual requirements and existing system. For design changes proposed by the review, follow the [design-review procedure](#design-reviews).

## Inspecting third-party library internals (Java/Maven)
Don't use `javap` to inspect library bytecode. Instead, download the sources jar and read the
real source: `mvn dependency:get -Dartifact=<groupId>:<artifactId>:<version>:jar:sources`, then
unzip the resulting `*-sources.jar` from the local `~/.m2` repo and read the `.java` files
directly. Also check the library's official reference docs/Javadoc online for documented
behavior/recommendations before relying solely on source-reading inference.

## Reviewing GitLab/GitHub MRs/PRs
When reviewing a GitLab merge request or a GitHub PR, don't pull file contents one-by-one through the GitLab MCP/API (base64 blobs, per-file diff calls) — fetch the source branch (`git fetch origin <branch>`) and check it out into a worktree (`git worktree add <scratch-path> FETCH_HEAD`), then use normal local tools (`git diff develop...HEAD`, Read, Grep) against it. Much cheaper and less error-prone than decoding API responses.

## Command output

When RTK hooks are available, follow [RTK.md](RTK.md) for filtered output, recovery and tool commands.
