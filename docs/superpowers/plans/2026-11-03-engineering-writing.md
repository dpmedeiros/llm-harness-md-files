# Engineering writing implementation plan

> For agentic workers: use `superpowers:executing-plans` to implement this plan. The user approved the design and explicitly authorized implementation on 2026-11-03.

**Goal:** Deliver one self-contained engineering writing skill in a locally testable Codex plugin.

**Architecture:** Shared guidance lives in the skill entry point. Three relative references supply format-specific guidance; the plugin manifest and repository marketplace provide installation metadata.

**Tech stack:** Markdown, JSON, and Codex skill UI metadata in YAML. Use existing validators and standard archive tools.

**Spec:** [Approved design](../specs/2026-11-03-engineering-writing-design.md).

## Constraints and review focus

Apply the approved design's requirements, especially the sections “Adapt the defaults” and “Package and maintenance.” Preserve `WRITING.md` byte for byte.

Review factual preservation, compliance with supplied templates, causal completeness, short-message proportionality, and references that still resolve after copying the skill or extracting the plugin archive.

## Task 1: Capture representative baseline behavior

**Files:** `docs/evaluations/engineering-writing/scenarios.md` and baseline evaluation receipts.

- [x] Write five synthetic briefs with observable criteria, using Given/When/Then descriptions.
- [x] Run each brief in a fresh agent context before creating the skill; retain each response.
- [x] Read every response and identify actual weaknesses without treating a passing baseline as a failure.

## Task 2: Build the skill and installation package

**Files:** `plugins/engineering-writing/plugin.json`, plugin `README.md`, `skills/engineering-writing/SKILL.md`, `agents/openai.yaml`, and three `references/*.md` files; `.agents/plugins/marketplace.json`; `.gitignore`; repository `README.md`.

**Interfaces:** The marketplace resolves `./plugins/engineering-writing` from the repository root. The portable manifest discovers `skills/`; the skill routes to its own relative references.

- [x] Write shared instructions and focused references from the approved design and baseline findings.
- [x] Add manifest, UI metadata, marketplace, scoped ignore exceptions, and installation documentation.
- [x] Apply the required Humanizer pass to written drafts, preserving precise triggers, paths, and instructions.
- [x] Run Skill Creator's `quick_validate.py`; parse metadata and check relative links and archive portability.

## Task 3: Evaluate, review, and deliver

**Files:** Evaluation receipts and `docs/evaluations/engineering-writing/results.md`; local ZIP output outside the source package.

- [x] Run the same five briefs in fresh contexts with the completed skill; compare the actual outputs against the scenario criteria.
- [x] Record what passed, what changed, and what the samples cannot establish.
- [x] Request an independent review of the complete change and address material findings.
- [x] Run final structural checks, verify `WRITING.md` against the starting Git revision, and inspect the extracted archive.
- [x] Commit the implementation on `codex/engineering-writing-plugin`; leave publishing and installation settings untouched.

## Execution record

The implementation uses the existing checkout on a dedicated feature branch. A second worktree would split the approved design and the visible workspace without adding useful isolation for this documentation package.

Keep behavioral execution receipts in `/tmp/engineering-writing-eval/` while working; retain the briefs, responses, and final assessment under `docs/evaluations/engineering-writing/`. Baseline tasks and guided tasks use the same briefs and separate agent contexts. Automatic discovery and desktop installation need separate runtime evidence; the behavioral test harness explicitly loads the skill.

Completed the three tasks. All five baseline samples met the factual and format criteria; the guided samples also passed. The package passed schema and portability checks, installed in an isolated Codex CLI home, and received independent standards and design reviews with no actionable findings. The [results](../../evaluations/engineering-writing/results.md) record the evidence and limits.
