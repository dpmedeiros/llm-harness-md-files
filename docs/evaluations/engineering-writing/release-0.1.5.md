# Engineering writing 0.1.5 migration

Moved writing-guide ownership into the skill. The guide at `plugins/engineering-writing/skills/engineering-writing/WRITING.md` is the only maintained copy; the repository-root copy and its synchronization procedure were removed.

## Agent routing and guide preservation

The repository's `AGENTS.md` now routes all writing, including chat replies, to the engineering-writing skill. Its repeated writing rules and direct guide references were removed. Other repository agent instructions were preserved.

The global Codex `AGENTS.md` also had an obsolete leading Writing section that referenced the removed root file. Removed that section and preserved its complete LLM harness section byte for byte. That bootstrap still loads the repository's agent instructions, which point to the skill. This global-file change is outside the repository's Git commit.

Preserved `ea55c0c:WRITING.md` byte for byte during migration, with SHA-256 `ed992ab0c8b7d85c4b80520e49ce153c1f59ff64b60d504e3683cfaf1bdbc62e`. The user then requested one qualification: run the Humanizer pass when that skill is installed. The current guide includes that qualification; the skill workflow and focused references remain unchanged. Updated current READMEs and the design document to describe editing the guide inside the skill; historical release records remain unchanged.

## Validation

The independent test-writing agent revised the previous normalization checks for the user's explicit migration request. Before implementation, eight checks ran with three expected failures: the root guide remained, repository agent instructions lacked the skill pointer, and the root README linked to the former guide location. Preserved guide bytes and standalone resources already passed.

A ninth check exposed the stale global startup reference before its correction. The test requires the entire remaining global file to match the captured harness section, preserving all other startup instructions. Separate implementation and fixing agents handled the repository migration and global correction; neither changed the tests.

All nine checks now pass, including standalone copying, archive extraction, contained file links, heading anchors, agent routing, and guide preservation apart from the requested Humanizer qualification. Skill Creator's validator and `git diff --check` passed. An independent review found no actionable issues.

Installed version 0.1.5 in the temporary Codex home used for the previous release check, before the final Humanizer qualification. The CLI returned the expected version and cache path; the installed guide matched the canonical skill guide at that time. The normal installed plugin was not refreshed. The previous targeted API-reference sample and original five behavioral samples were not rerun for 0.1.5.

## Archive

Archive: `/tmp/engineering-writing-0.1.5.zip`.

SHA-256: `592f4948874c2bd2814f3137b67b03b88cc13fe8fdda8c016f1359da773058e0`.

Archive integrity passed. The package contains the canonical guide inside the complete standalone skill, with the existing references, metadata, icon, license, and policy pages. No OpenAI Platform upload, submission, or publication was performed.
