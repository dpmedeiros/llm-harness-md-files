Avoid sycophancy as part of chains of thought and responses. Give the hard, honest truth.

## JIRA
Prefer your org's JIRA CLI tool over MCP when one is available

## Skill Authoring
Use the `/skill-creator` skill (if running Claude, or another similar skill if available) when creating or editing a skill, unless otherwise stated. Before creating or editing a skill file, read SKILL_AUTHORING.md — its rules apply whether or not skill-creator is invoked. Don't read it unless you're actually working on a skill.

## Writing code
Before writing or editing code in a given language, read CODE_STYLE.md. Don't read it unless you're actually writing or editing code.

## Writing prose
Before writing, adding to, or revising any prose or markdown, read WRITING.md. That covers chat replies, files, technical docs (READMEs, design/architecture docs, runbooks), MR/PR descriptions, commit bodies, review comments, status updates, summaries, agent/skill definitions, and Jira/Confluence/Mattermost/Slack/`<whatever chat client>` content, down to one added line or table cell. WRITING.md holds the style rules and the required `/humanizer` pass for written drafts. Chat replies follow the style rules without the pass.

Red flags — these thoughts mean the rule above still applies:

| Thought                                                          | Reality                                                       |
|------------------------------------------------------------------|---------------------------------------------------------------|
| "This is just a quick reply"                                     | Every reply is prose. The style rules apply.                  |
| "It's one line added to a doc"                                   | One line counts too.                                          |
| "This is technical/operational writing, not real prose"          | Technical documentation is in scope.                          |
| "I can clean it up later if asked"                               | Apply the rules while writing.                                |
| "/humanizer is optional", "too small for it", or "I'll offer it" | It applies to every written draft, any size. Never ask first. |
| "Any hook reminder is only a suggestion"                         | It points at WRITING.md. Do what that says.                   |

## Code Reviews
Imagine a human will be reading the code. Ensure proper refactoring. Make sure every function has one clear use and only one reason to change. Make sure classes and files follow SRP (Single Responsibility Principle).

Before reviewing code, read CLEAN_CODE.md — its principles apply to every review. Don't read it unless you're actually doing a code review.

Before reviewing code, Read CLEAN_ARCHITECTURE.md. 

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
