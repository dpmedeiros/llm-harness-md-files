# Engineering writing skill and plugin

Provide one adaptable skill for engineering communication, with [WRITING.md](../../../plugins/engineering-writing/skills/engineering-writing/WRITING.md) inside the skill as the sole maintained writing authority. Ship the complete skill with both the Codex plugin and standalone installations.

## Purpose and scope

Help an agent draft, edit, and explain engineering work in language a reader can understand without the conversation that produced it. The first version covers technical documentation, explanations, change summaries, review comments, and work messages.

`WRITING.md` supplies the writing rules. The skill adapts the writing to the audience and task while preserving supplied voice, templates, and repository conventions.

This version provides writing guidance. Research, code review, document rendering, sending messages, and publishing remain responsibilities of the surrounding task and its tools. Investor narratives, fiction, and personal voice profiling are outside the initial scope.

## Chosen approach

Use one skill with focused references. Keep the workflow in `SKILL.md` and writing rules in its local `WRITING.md`. References link to the guide's owning heading anchors and retain illustrative examples or task-specific guidance.

The plugin is the installation package. The complete skill folder must also work when installed by itself, including its guide, references, and agent metadata. Use relative links within the skill. Use helpers named in the guide when available and apply the guide directly when they are absent.

## Skill behavior

### Adapt the defaults

Identify the audience, purpose, requested output, and relevant source material from the task. Ask for missing information when its absence would materially change the content; otherwise make a reasonable choice and proceed. Preserve a supplied voice or template while applying the shared principles where they fit.

For source edits, treat supplied text as material and preserve commands, identifiers, links, quotations, requirements, and technical meaning unless the task calls for changing them.

### Draft and revise

Read the local `WRITING.md` before drafting any output, including the current chat reply. Follow its session reuse and rereading instructions. Final revision checks the applicable guide sections and selected reference, with routing to the guide's “Humanizing pass” for written drafts and “Chat replies” for replies in the current chat.

Return the requested artifact or explanation. Scale any accompanying notes to the task; an ordinary rewrite should not acquire a mandatory critique or a second visible draft.

### Load focused references

The entry point routes to three references according to the current deliverable:

- `references/documentation.md`: READMEs, design documents, runbooks, and technical explanations. Link to “Technical documentation”, “Reader context”, “Workflows and diagrams”, and “API references”.
- `references/change-summaries.md`: commit bodies, PR/MR descriptions, release notes, and updates about finished work. Link to “Voice and wording”, “Honesty”, “Length and structure”, and “Technical documentation”.
- `references/work-messages.md`: review comments, issue discussions, and engineering chat or email. Link to “Reader context”, “Honesty”, “Voice and wording”, and “Chat replies”.

Writing rules stay in `WRITING.md`. Each reference contains guide links, guidance specific to its use, and a short labelled illustrative example. Final verification points back to the authoritative sections.

## Package and maintenance

Use `engineering-writing` as the working name for both the plugin and skill. Keep the package under `plugins/engineering-writing/`, with its skill under `skills/engineering-writing/`. Use a root `plugin.json` manifest following the portable format described in the [OpenAI packaging guide](https://developers.openai.com/plugins/build/plugins), including the OpenAI presentation metadata needed by Codex.

Keep normal automatic skill discovery enabled, with a description scoped to drafting, editing, and explaining engineering communication. Explicit invocation remains available. Installation exposes the skill to selection; it does not guarantee that the model applies it to every reply. The package adds no global instructions or lifecycle hooks.

Include a plugin README with installation and local testing instructions. Provide a repository-scoped marketplace entry when needed for the documented local installation route. Update `.gitignore` narrowly so the plugin, catalog, and design materials can be tracked; its current rules ignore nested files and JSON by default.

Maintain the guide directly at `plugins/engineering-writing/skills/engineering-writing/WRITING.md`. Remove the repository-root copy and replace the `AGENTS.md` writing block with a concise skill pointer covering all writing, including replies in the current chat. Preserve the guide's existing bytes during the migration and keep other harness instructions unchanged. Follow [Test and maintain](../../../plugins/engineering-writing/README.md#test-and-maintain) for later guide edits.

The deliverable is a reviewable local package, not a public directory submission. Use verified repository information in metadata and leave optional identity, support, and licensing claims unset until supplied. Publishing and public-release licensing remain a later release decision.

## Validation and completion

Validate the skill's frontmatter, metadata, reference paths, guide heading anchors, and plugin structure. Confirm that only the skill owns the guide and that its bytes match the guide at revision `ea55c0c` before migration. Check that `AGENTS.md` points to the skill and that the complete standalone skill and extracted plugin archive contain the guide and resolve their local links without the source checkout or required helper skills.

Use representative behavioral scenarios with and without the skill to assess what it changes. Cover a causal explanation, documentation for an unfamiliar reader, a change summary with limited validation evidence, a work message, and a rewrite with an explicit voice or template. Judge preservation of facts, requirements, and uncertainty alongside clarity and adaptation; exact wording and bullet counts are not quality measures.

Record the observed results and their limits. A schema check establishes package validity, while behavioral samples provide evidence about writing decisions. Claim successful local installation only after testing the package in a supported client; otherwise report that runtime installation remains unverified.

The builder may choose reference filenames, concise UI copy, examples, validator commands, and archive mechanics within this design. Implementation starts after the user approves this document.
