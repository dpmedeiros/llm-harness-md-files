# Engineering writing 0.1.4 normalization

Made repository-root `WRITING.md` the maintained source of the skill's writing rules. The skill includes a byte-identical copy and reads it before drafting, so plugin and standalone installations can use the same guide.

## Rules and maintenance

`SKILL.md` now handles task setup, guide loading, reference selection, and revision. The three focused references link to the guide's owning sections and retain their illustrative examples and task-specific advice. Helpers named in the guide are used when available; the guide is applied directly when they are absent.

The [plugin maintenance instructions](../../../plugins/engineering-writing/README.md#test-and-maintain) describe refreshing the bundled guide from the root source and checking that the bytes match. The root README and design document point to that procedure.

The root guide was preserved from starting revision `c10d602`. Both copies have SHA-256 `ed992ab0c8b7d85c4b80520e49ce153c1f59ff64b60d504e3683cfaf1bdbc62e`. The manifest changes only the version and release notes.

## Resource and installation checks

An independent test-writing agent created six checks in `/tmp/engineering-writing-normalization-tests.py`. Before implementation, four failed for the requested missing resources: no guide in a standalone copy, no guide in an extracted archive, no local guide link in `SKILL.md`, and no guide-section links in the focused references. Root preservation and the existing local links passed.

After the implementation, all six checks passed. The checks validate guide equality, contained file references, and heading anchors after copying or extraction. Skill Creator's `quick_validate.py`, direct `cmp` of the two guides, and `git diff --check` also passed.

Registered the repository marketplace and installed version 0.1.4 in `/tmp/engineering-writing-normalization/codex-home`. The CLI returned the expected version and cache path; the installed guide matched root `WRITING.md`. This test left the user's normal installed plugin unchanged. Automatic selection and desktop installation were not tested.

## Writing sample and independent review

A fresh agent used a copied standalone skill to write an API reference from a proposed lookup operation. It reported reading only `SKILL.md`, bundled `WRITING.md`, and the documentation reference. Its response marked the API as proposed, kept one declaration, supplied explicit Input, Output, and Side effects, and preserved the supplied behavior and limits.

This sample checks use of the guide's API-reference rules. It does not establish a general quality improvement or repeated-run reliability; the five version 0.1.0 writing samples were not rerun.

An independent reviewer found no material correctness or standalone-use problem. It identified the repeated refresh procedure in the READMEs and design document; the correction gives the procedure one home in the plugin README.

## Archive

Archive: `/tmp/engineering-writing-0.1.4.zip`.

SHA-256: `3f50199d1dbf93f31374cfb5c1a883cdcaa6c735765bf9128cb422b76e91cf82`.

The archive includes the bundled guide, skill, three focused references, agent metadata, listing metadata, icon, license, privacy policy, terms, and plugin README. Archive integrity passed. The OpenAI Platform submission process was not run.
