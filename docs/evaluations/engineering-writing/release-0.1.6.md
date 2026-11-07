# Engineering writing 0.1.6 distribution

Bumped the plugin to 0.1.6 and packaged the committed informal-tone guidance for distribution. The guide encourages direct, approachable language and contractions when they fit, while keeping technical details precise.

## Source and contents

Updated the plugin manifest's version and release notes, plus the README's release description. Preserved all other manifest values and the complete skill contents from revision `2701bdc`. The writing guide remains owned by the skill, and Humanizer remains conditional on installation.

Prepared two ZIPs under the ignored `dist/` directory:

- `engineering-writing-0.1.6.zip`: the complete plugin, with twelve files and `plugin.json` at the archive root.
- `engineering-writing-skill-0.1.6.zip`: the standalone `engineering-writing/` folder, with its entry point, guide, three references, agent metadata, and Apache-2.0 license. The license comes from the plugin's maintained license file.

The standalone archive can be extracted into a project's supported skills directory. The complete folder supplies all local resources; another copy of the guide is unnecessary.

## Verification

Parsed the JSON and YAML, checked the manifest version, and compared unrelated metadata with the source revision. Compared every archived file with its source, checked both ZIPs' integrity, and resolved local Markdown references after extraction. Skill Creator's validator passed on both the source skill and extracted standalone skill. `git diff --check` passed.

Installed version 0.1.6 from the repository marketplace with an isolated Codex home under `/tmp/engineering-writing-release-0.1.6/`. The CLI returned the expected version and cache path, and the installed guide matched the source. The user's normal plugin installation and settings were untouched.

These checks cover packaging and local installation. Behavioral writing samples, automatic selection, and desktop installation were not tested for this release. No OpenAI Platform submission or public-directory publication was performed.

## Checksums

The distribution includes `dist/SHA256SUMS` with these SHA-256 values:

```text
810a7432c1c215150411d0fc1b3d3521438fab8209aa7c251461df6e034f0487  engineering-writing-0.1.6.zip
487481d12065ef8bcefa91f3be08c0b6e5ca7f4aea2ecd1c75c76c07a00fe0e6  engineering-writing-skill-0.1.6.zip
```
