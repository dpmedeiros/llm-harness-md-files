# Engineering writing validation results

Version 0.1.0 passed the structural checks and installed through the repository marketplace using Codex CLI 0.166.0. Five guided writing samples met the [briefs' criteria](scenarios.md); the baseline also met all five briefs' factual and format criteria.

## Behavioral samples

Each brief ran once without the skill and once with it, in separate fresh agent contexts with no model override. The brief text stayed the same. Baseline agents were instructed to use only the brief; guided agents were instructed to load only the skill and the references it routes to. The implementation author manually assessed both sets against the published criteria.

The raw [baseline](baseline.md) and [guided responses](with-skill.md) are retained for inspection.

| Brief | Baseline | With skill | Observed difference |
| --- | --- | --- | --- |
| Causal explanation | Pass | Pass | Both explained expiration, ownership clearing, eligibility, and unknown takeover time. The guided sample also defined “lease” explicitly. |
| New-reader quickstart | Pass | Pass | Both put readiness before submission and preserved the commands and event. The guided sample used numbered steps. |
| Change summary | Pass | Pass | Both preserved the exact headings and validation limits. The baseline opened with “Send”; the guided sample used the default past tense, “Changed.” |
| Work message | Pass | Pass | Both preserved the dates, scope, options, recommendation, and decision request within 70 words. The guided sample used one paragraph. |
| Voice and template | Pass | Pass | Both used two short paragraphs, retained all factual limitations, and followed the conversational sample. Differences were punctuation only. |

The imperative opening in the baseline change summary differs from the source guide's preferred past-tense default. It is a style difference, not a factual failure. The extracted instructions preserve that default while yielding to a repository convention or explicit request.

These samples show that the skill can support the intended tasks while preserving explicit format and voice requirements. They do not demonstrate a general quality improvement, repeated-run reliability, performance on other models, or successful automatic selection. The guided tests explicitly loaded the skill.

## Package checks

The skill passed Skill Creator's `quick_validate.py`. The portable manifest passed validation against the published `https://agent-plugins.org/schemas/1.0.0/plugin.schema.json`, using `jsonschema` 4.26.0 installed only in a temporary validation directory.

Metadata parsing, reference resolution, archive extraction, standalone skill validation, and tracked-file coverage passed. `WRITING.md` matched the starting Git revision byte for byte. Its SHA-256 is `ee15d1c775bded80995bc8b9255823c49aa406f6c43ad4e2c80ce911899a6f6b`, from Git revision `ec32647ce66cf32251dc5594d2569981c203e251`.

The ZIP contains seven package files, with `plugin.json` at its root. Its SHA-256 is `d3457056288270f287cb9e2917b323f0af8480e0196d69bbfc6743ed35082283`. A separately copied standalone skill passed validation and resolved all of its references.

Independent reviews of design coverage and repository standards found no actionable issues. Reviewers checked the staged files, the retained responses, the archive, and the isolated installation. These reviews supplement the sample results; they do not establish automatic discovery or desktop behavior.

## Client installation

Registered the repository marketplace and installed `engineering-writing@llm-harness-md-files` with a temporary Codex home. The CLI returned version `0.1.0` and an installed cache directory. The user's normal Codex configuration and plugin installation were untouched.

The CLI emitted a warning that it would not create helper binaries under `/tmp`; both marketplace registration and plugin installation completed successfully. Desktop installation and automatic skill selection have not been tested. Public submission and licensing are outside this local-package validation.
