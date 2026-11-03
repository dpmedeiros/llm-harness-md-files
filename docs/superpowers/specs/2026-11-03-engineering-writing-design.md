# Engineering writing skill and plugin

Build one adaptable skill for engineering communication, using `WRITING.md` as its starting point. Package the skill as a locally testable Codex plugin that others can install; keep `WRITING.md` unchanged.

## Purpose and scope

Help an agent draft, edit, and explain engineering work in language a reader can understand without the conversation that produced it. The first version covers technical documentation, explanations, change summaries, review comments, and work messages.

The user's principles supply the defaults: establish the reader's context, explain causal steps, use plain language, and match claims to the available evidence. Adapt voice, length, and structure to the audience and the task. Existing templates, repository conventions, and explicit user requirements govern the deliverable's format.

This version provides writing guidance. Research, code review, document rendering, sending messages, and publishing remain responsibilities of the surrounding task and its tools. Investor narratives, fiction, and personal voice profiling are outside the initial scope.

## Chosen approach

Use one skill with focused references. Keep shared principles and the workflow in `SKILL.md`; put guidance needed for a particular kind of communication in the corresponding reference. This gives the agent one entry point and one authoritative home for each rule within the package.

The alternative was separate skills for documentation, change summaries, and messages. Those would give users independent entry points, but their shared guidance would need additional coordination. The user chose one adaptable skill and agreed to leave `WRITING.md` unchanged during initial development.

The plugin is the installation package. The skill folder must also work when installed by itself, with all of its references included. It must use relative paths and require no other skills, personal files, connectors, scripts, or local configuration.

## Skill behavior

### Adapt the defaults

Identify the audience, purpose, requested output, and relevant source material from the task. Ask for missing information when its absence would materially change the content; otherwise make a reasonable choice and proceed. Preserve a supplied voice or template while applying the shared principles where they fit.

Treat preferences such as past-tense change summaries, short paragraphs, and small lists as defaults for suitable contexts. Preserve completeness when a technical contract, reference table, or instruction needs more detail. Use formatting to make the content easier to navigate.

Preserve the distinction between style preferences and factual accuracy. Keep quantities, identifiers, requirements, exceptions, evidence, and uncertainty intact during editing. When sources leave a material gap, state the gap or ask for the missing fact. A request for stronger wording cannot turn an unsupported claim into an established result.

### Draft and revise

Lead with the concrete answer, purpose, or result appropriate to the deliverable. Establish the starting conditions before explaining what changes, what produces that change, and its consequence. Include the intermediate operation that makes the explanation follow; add a small example, quantities, or a diagram when they clarify that operation.

Write for a reader encountering the material for the first time. Define unfamiliar terms near their first use and provide the context needed to follow the current behavior. Give change history a place when the document's purpose calls for it, such as release notes or a migration guide.

Include a self-contained revision pass that checks meaning and evidence first, then clarity and natural phrasing. Remove repetition, unsupported significance, stock introductions, and formulaic sentence patterns. Preserve the precision of technical instructions while improving their wording. This pass implements the package's own guidance and requires no external Humanizer skill.

Return the requested artifact or explanation. Scale any accompanying notes to the task; an ordinary rewrite should not acquire a mandatory critique or a second visible draft.

### Load focused references

The entry point routes to three references according to the current deliverable:

- `references/documentation.md`: READMEs, design documents, runbooks, and technical explanations. Cover reader context, causal descriptions, terms, examples, and ordering common information before rare details.
- `references/change-summaries.md`: commit bodies, PR/MR descriptions, release notes, and updates about finished work. Cover concrete changes, relevant purpose, validation evidence, and material limitations. Respect the repository's commit and PR conventions.
- `references/work-messages.md`: review comments, issue discussions, and engineering chat or email. Cover the point the reader needs, supporting evidence, and any decision or action needed from them.

Shared rules stay in `SKILL.md`. Each reference contains only guidance specific to its use and can include a short illustrative example. Final verification points back to the authoritative sections instead of repeating their rules in a checklist.

## Package and maintenance

Use `engineering-writing` as the working name for both the plugin and skill. Keep the package under `plugins/engineering-writing/`, with its skill under `skills/engineering-writing/`. Use a root `plugin.json` manifest following the portable format described in the [OpenAI packaging guide](https://developers.openai.com/plugins/build/plugins), including the OpenAI presentation metadata needed by Codex.

Keep normal automatic skill discovery enabled, with a description scoped to drafting, editing, and explaining engineering communication. Explicit invocation remains available. Installation exposes the skill to selection; it does not guarantee that the model applies it to every reply. The package adds no global instructions or lifecycle hooks.

Include a plugin README with installation and local testing instructions. Provide a repository-scoped marketplace entry when needed for the documented local installation route. Update `.gitignore` narrowly so the plugin, catalog, and design materials can be tracked; its current rules ignore nested files and JSON by default.

Keep `WRITING.md` and the existing global harness setup unchanged. The package becomes authoritative for its own behavior. During this initial extraction, improvements may need deliberate transfer between the personal guide and the package; automatic synchronization would add machinery before the relationship is proven.

The deliverable is a reviewable local package, not a public directory submission. Use verified repository information in metadata and leave optional identity, support, and licensing claims unset until supplied. Publishing and public-release licensing remain a later release decision.

## Validation and completion

Validate the skill's frontmatter, metadata, reference paths, and plugin structure. Confirm that the package has no references to the author's home directory or required external skills, and that `WRITING.md` is unchanged. Check the archive's contents if an installable archive is produced.

Use representative behavioral scenarios with and without the skill to assess what it changes. Cover a causal explanation, documentation for an unfamiliar reader, a change summary with limited validation evidence, a work message, and a rewrite with an explicit voice or template. Judge preservation of facts, requirements, and uncertainty alongside clarity and adaptation; exact wording and bullet counts are not quality measures.

Record the observed results and their limits. A schema check establishes package validity, while behavioral samples provide evidence about writing decisions. Claim successful local installation only after testing the package in a supported client; otherwise report that runtime installation remains unverified.

The builder may choose reference filenames, concise UI copy, examples, validator commands, and archive mechanics within this design. Implementation starts after the user approves this document.
