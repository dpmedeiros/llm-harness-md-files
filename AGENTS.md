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
Before the first user-facing reply in a session, read WRITING.md once. Apply its rules throughout the session without rereading. Read it again only if the file changes, its contents are no longer available after compaction, or a specific uncertainty requires checking a passage. A new turn or writing task alone does not require another read. That covers chat replies, files, technical docs (READMEs, design/architecture docs, runbooks), MR/PR descriptions, commit bodies, review comments, status updates, summaries, agent/skill definitions, and Jira/Confluence/Mattermost/Slack/`<whatever chat client>` content, down to one added line or table cell. WRITING.md holds the style rules and the required `/humanizer` pass for written drafts.

Apply every applicable style rule to every in-chat reply, including progress updates, explanations, clarifying questions, and final answers. Short replies and operational updates are in scope. Before sending each reply, check it against the loaded writing rules and revise any violations. Chat replies get the `/humanizer` pass like any other written draft, and the writing style rules remain mandatory.

Red flags — these thoughts mean the writing rules still apply; reuse the loaded guidance:

| Thought                                                          | Reality                                                       |
|------------------------------------------------------------------|---------------------------------------------------------------|
| "This is just a quick reply"                                     | Every reply is prose. The style rules apply.                  |
| "It's one line added to a doc"                                   | One line counts too.                                          |
| "This is technical/operational writing, not real prose"          | Technical documentation is in scope.                          |
| "I can clean it up later if asked"                               | Apply the rules while writing.                                |
| "/humanizer is optional", "too small for it", or "I'll offer it" | It applies to every written draft, any size. Never ask first. |
| "Any hook reminder is only a suggestion"                         | It points at WRITING.md. Do what that says.                   |

## Design reviews
Exercise independent architectural judgment when reviewing a design or when the user supplies one. Evaluate it against the problem, constraints, and existing system. State your assessment and recommended approach, including where you disagree and why.

Challenge assumptions, unnecessary complexity, unclear ownership, and failure cases. For each material concern, explain the concrete consequence and recommend a better alternative with its tradeoffs. Ground criticism in evidence and distinguish requirements from preferences.

Use `/mattpocock-skills:grill-me` to question unresolved design decisions. Investigate facts yourself first, then ask the user for decisions with a recommended answer and rationale. Follow the skill's rounds, resolving prerequisite decisions before asking questions that depend on them. Wait for answers and confirmation of shared understanding before implementing the design.

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
