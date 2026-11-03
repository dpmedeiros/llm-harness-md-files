# Engineering writing submission preparation

Prepared version 0.1.1 for upload as a skills-only plugin. Local checks passed for the source and the extracted submission ZIP; OpenAI Platform's scans, verified publisher identity, attestations, and approval remain dashboard steps.

## Listing and publication

The user supplied the publisher name **Daniel Medeiros**, selected **Apache-2.0**, approved GitHub Issues for support, and chose all supported countries with no payments or purchases. The package records those choices in its manifest. The intended publishing identity has not been verified through the dashboard in this session.

The listing subtitle is “Clear writing for engineers,” at 27 characters. The description covers documentation, explanations, change summaries, and work messages, with the surrounding workflow responsible for research, code validation, and publishing. Three review prompts exactly match the previously evaluated causal explanation, PR summary, and work-message briefs.

The website points to the plugin directory on its published feature branch. The support URL points to the repository's public Issues page; a GitHub account is needed to file an issue. Both destinations were fetched without authentication and their content inspected. These links should move to a stable release location if the feature branch is later removed.

The preparation skill's listing checklist asks for four public URLs. The [current official submission guide](https://developers.openai.com/plugins/deploy/submission#listing-metadata) distinguishes MCP review from skills-only metadata validation: all four website, support, privacy, and terms URLs are required for MCP review, while skills-only validation does not require all four. This skills-only package supplies the verified website and support links. Privacy and terms URLs remain absent; no published policies were supplied or invented. Confirm any additional requirements reported by the actual portal before submission.

The plugin includes the canonical Apache-2.0 license text fetched from the Apache Software Foundation. The license declaration applies to this plugin package; the surrounding repository's files were not given a new license.

## Logo and composer icon

Used built-in ImageGen to create code brackets framing three text lines. The user requested a more code-oriented design after the initial document-and-pencil proposal. The final asset is `plugins/engineering-writing/assets/icon.png`: a 1254 × 1254 RGB PNG, 1,153,400 bytes. Both `logo` and `composerIcon` reference it. Optional dark-mode assets and brand-color fields were omitted at the user's request.

Inspected the mark at 128, 48, and 24 pixels against white and dark backgrounds. The brackets and text lines remain distinguishable at composer sizes. Preview reductions were used for visual inspection only; the packaged asset is the original generated PNG.

Final ImageGen prompt, retained as provenance:

```text
Use case: logo-brand. Create one finished square logo icon for Engineering writing, a plugin for engineers writing technical explanations and documentation. The user's specific direction is: more code/engineer-like. Build a single bold white geometric symbol consisting of left and right code angle brackets framing three short horizontal text strokes, with carefully balanced negative space. Make the outer brackets visually dominant and keep the interior strokes simple and distinct. This should suggest both code and clear written explanations. Solid uniform dark charcoal square background; centered symbol occupying about 65 percent of the canvas. Flat, crisp, extremely minimal, technically precise, no texture or lighting effects. No document outline, no pencil, no quill, no gear, no mascot, no letters or words, no gradients, no shadows, no mockup, no collage. The actual icon must remain recognizable at 24 and 48 pixels and work as a listing logo and composer icon on light and dark app interfaces. Produce the actual square asset.
```

## Validation evidence

Validated the source manifest against Agent Plugins 1.0 using `jsonschema`, then checked the OpenAI listing fields, lengths, prompt limits, publication choices, and icon requirements against Plugin Creator's submission references. The icon's file type, dimensions, size, and contained paths passed. The package includes one valid skill with its three references and existing agent metadata.

The three packaged review prompts were compared with the evaluation briefs and matched exactly. The previous behavioral results remain applicable to the unchanged skill instructions; this release's changes affect listing metadata, licensing, and assets. No new behavioral improvement is claimed.

Codex CLI 0.166.0 installed version 0.1.1 from the repository marketplace in the isolated temporary Codex home and listed it as enabled. This test left the user's normal plugin installation and configuration untouched. Desktop installation and automatic selection remain untested.

Built the public ZIP from a separate copy of the source. It contains nine files: the root manifest, README, license, icon, skill entry point, agent metadata, and three references. It contains no marketplace, `.app.json`, `apps` binding, MCP server, credentials, or dependency directory. Verified the archive's inventory and bytes against the source and repeated manifest, icon, skill, and reference checks after extraction. Skill Creator's validator passed on the extracted skill.

Archive: `/tmp/engineering-writing-0.1.1-submission.zip`.

SHA-256: `48128cbcf715816063d78f0816852193ef997a30a845fc4684817ef304a99b3b`.

An independent reviewer inspected all nine ZIP entries, compared their bytes with the source, and checked metadata, icon requirements, licensing, skill preservation, and the distinction between package and portal readiness. No actionable findings were reported. The reviewer's web fetches of the GitHub pages returned cache misses; the earlier direct, unauthenticated fetches were the basis for URL verification.

Confirmed that `WRITING.md` is byte-identical to revision `70b8bb4`, with SHA-256 `ee15d1c775bded80995bc8b9255823c49aa406f6c43ad4e2c80ce911899a6f6b`. All files under the plugin's `skills/` directory are also unchanged.

## Remaining dashboard work

Upload the ZIP under the intended organization and verified Daniel Medeiros developer identity, inspect the imported metadata, and resolve any required platform scan findings. Skills-only plugins need no MCP review cases, demo recording, or reviewer credentials. The authorized developer completes the policy attestations before submission for review; publishing follows approval as a separate action. No upload, submission, or publication was performed in this preparation.
