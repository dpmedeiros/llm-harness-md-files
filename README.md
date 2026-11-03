# llm-harness-md-files

Personal global instructions for Claude Code (also usable with other harnesses): the markdown files that tell it how to write, review and style code, plus a statistical fingerprint of my writing voice. The repository also includes a standalone engineering writing skill packaged as a Codex plugin.

## Engineering writing plugin

[Engineering writing](plugins/engineering-writing/README.md) adapts the principles in `WRITING.md` for documentation, change summaries, and work messages. It works without other skills and respects the user's voice, templates, and project conventions. The plugin README covers installation.

## What's in the repo

- `AGENTS.md` holds the top-level rules and tells Claude which of the other files to read before a given task: `CODE_STYLE.md` before writing code, `WRITING.md` before writing prose, `CLEAN_CODE.md` and `CLEAN_ARCHITECTURE.md` before a code review, and `SKILL_AUTHORING.md` before editing a skill.
- `CLAUDE.md` and `RTK.md` configure RTK, a command-output filter that shortens shell output to save tokens.
- `WRITING.md` has the prose rules: voice, honesty, structure for MR/PR descriptions and technical docs, and a required humanizer pass on written drafts.
- `CODE_STYLE.md` has language-agnostic defaults for writing and refactoring code.
- `CLEAN_CODE.md` and `CLEAN_ARCHITECTURE.md` are cribbed summaries from github (original source forgotten) of the two Robert C. Martin books, used as review checklists.
- `SKILL_AUTHORING.md` has the rules for writing Claude Code skill files.
- `voice-fingerprint.sanitized.json` is the voice fingerprint described below.

## Voice fingerprint

`voice-fingerprint.sanitized.json` describes how I write as numbers and short notes, so the [humanizer skill](https://github.com/adelaidasofia/humanizer) can rewrite AI-sounding drafts toward my style instead of toward generic clean prose. It was computed from 32 files and about 17,800 words of my own writing.

### Sources

The samples fall into seven registers, because my PR descriptions, chat messages and talk scripts don't sound alike:

- 4 PR descriptions
- 11 Jira tickets and comments (3 were too short for the indexer, so the stats cover 8)
- 34 Mattermost messages in 3 files
- 6 technical design and spec docs (about 9,760 words, with template headers and code stripped)
- 3 pieces of fiction
- 8 talk scripts (2 are excerpts, and scripture quotes inside them are not my voice)
- 4 Spanish talk outlines (1,458 words after removing quotes and pasted publication text). They sit in their own `talks_es` register and are not counted in the totals above, which cover the other six registers.

### How it was derived

1. `voice-indexer.py`, a stdlib-only Python script from the [humanizer skill](https://github.com/adelaidasofia/humanizer) by adelaidasofia (MIT license), read the samples and computed the statistics: sentence length (mean, standard deviation, 25th, 50th and 75th percentiles), paragraph length, punctuation per sentence or per 100 words (commas, colons, semicolons, parentheticals, em dashes, ellipses), connector frequency per 1,000 words, the most common sentence-opening words, vocabulary richness (type-token ratio), and the share of Spanish words.
2. The script's output blends the six English registers, which understates engineering prose, so the same statistics were recomputed per register and merged into a `registers` section. Chat gets its own sentence boundaries per message, since the indexer merges messages that lack final punctuation.
3. Each register also got `markers` (patterns to match), `avoid` (patterns to keep out) and sometimes a `caution`. These are qualitative notes written from reading the samples, not computed values.
4. This published copy had work-specific content removed: the most common content words, opening words that were domain terms, coworker names and internal system names. The style statistics and the register notes are otherwise unchanged.

### Setting up your own

1. Install the humanizer skill from the Claude official marketplace. On other harnesses, install it from the [GitHub repo](https://github.com/adelaidasofia/humanizer).
2. The marketplace install includes `voice-indexer.py`, but only in the plugin cache (`~/.claude/plugins/cache/anthropic-plugin-directory/humanizer-adelaidasofia/<version>/`), not at the `~/.claude/skills/humanizer/` path the skill tells you to run it from. Copy it to `~/.claude`. On other harnesses, download it from the GitHub repo.
3. Run the skill and ask Claude to set up a fingerprint. It needs a corpus of your writing, so have the files ready. It will write `voice-fingerprint.json` to your `~/.claude` (or wherever) directory and use it in `/humanizer` skill invocations.

### Limits

- Some registers are small. The PR register is 4 files and 640 words, and `talks_es` is 4 files and 1,458 words, so their statistics move a lot with each added sample.
- A few Jira samples read like AI-assisted drafts, and the `jira` register's `caution` says so.
- The spec stats come from PDF text and some co-authored docs, so the mean sentence length is inflated. Use the median and 75th percentile.
- The fingerprint measures surface style. It doesn't capture whether the content is right.
