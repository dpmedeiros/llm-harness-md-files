# Engineering writing 0.1.3 release preparation

Prepared version 0.1.3 as a skills-only submission ZIP on November 3, 2026. Structural validation and an isolated Codex CLI installation passed. The behavioral samples from version 0.1.0 were not rerun.

## Release contents

Clarified the explanation order: concrete answer, definitions and starting conditions, what changes, why it changes, and the consequence. Made explicit the intermediate causal step, the use of quantities and examples, and the assumed reader context. Added a revision check before every reply in the current chat and removed repeated answer-first guidance from the documentation reference.

Moved the website, privacy, and terms listing links from the merged feature branch to `main`. Preserved the publisher, license, prompts, icon, country targeting, and commerce declaration.

The repository's separate `WRITING.md` also incorporates the global explanation and reply-check rules, session reuse instructions, and the current-chat exemption from the Humanizer pass. The standalone skill keeps its own revision process and requires no other skill.

## Archive

Archive: `/tmp/engineering-writing-0.1.3-submission.zip`.

SHA-256: `e0725cbbd06c30376466370835b69338294d42086a91df7daabbf1c86994b5e4`.

The ZIP contains eleven files with `plugin.json` at its root. Its inventory matches the plugin source; every packaged file was compared byte for byte, and the archive integrity check passed. The archive contains no marketplace, app binding, or development evaluation records.

## Validation

Validated the extracted manifest against the published Agent Plugins 1.0 schema. Checked listing text limits, prompts, publication values, icon format and dimensions, YAML parsing, and contained skill-reference links. Skill Creator's validator passed on the extracted skill, and `git diff --check` passed on the source changes.

Fetched all four listing URLs without authentication and inspected their content. The website identifies Engineering writing, the support URL opens the repository's Issues page, and the privacy and terms pages identify the plugin and publisher. Their raw published Markdown matches the packaged policy files.

Registered the local repository marketplace and installed version 0.1.3 with Codex CLI using `/tmp/engineering-writing-release-0.1.3/codex-home`. The CLI returned the expected version and cache path. It warned that helper binaries would not be created under `/tmp`; both marketplace registration and plugin installation succeeded.

These checks establish package structure and local installation. They do not establish behavioral improvement, automatic skill selection, or desktop installation. No OpenAI Platform draft was uploaded, replaced, submitted, or published; portal scans, identity verification, and applicable attestations remain portal steps.
