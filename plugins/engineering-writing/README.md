# Engineering writing

Draft and revise engineering communication using the bundled [WRITING.md](skills/engineering-writing/WRITING.md). The skill adapts the writing to your audience, voice, templates, and project conventions.

## Use the skill

Use it for documentation and explanations, change summaries, review comments, and work messages. For example:

```text
Use $engineering-writing to revise this explanation for an engineer new to the service.
```

It can also be selected automatically for relevant tasks. Installing it makes it available to the model; selection on every reply is not guaranteed. It uses helpers named in the guide when available and applies the guide directly when they are absent. It requires no account connections or configuration.

## Publisher and icon

Daniel Medeiros maintains Engineering writing. The logo combines code brackets with lines of text to represent engineering communication. The listing and composer use the same high-contrast mark.

Use [GitHub Issues](https://github.com/dpmedeiros/llm-harness-md-files/issues) for support. A GitHub account is needed to file an issue.

## Install from this checkout

This repository includes a marketplace at `.agents/plugins/marketplace.json`. From the repository root, register it with:

```sh
codex plugin marketplace add .
```

On a client that provides `codex plugin add`, install it with:

```sh
codex plugin add engineering-writing@llm-harness-md-files
```

In a supported desktop client, the repository marketplace is also a local source in the Plugins directory. Install **Engineering writing**, then start a new chat and select the skill to try the example above. See the [OpenAI packaging guide](https://developers.openai.com/plugins/build/plugins) for client-specific marketplace and refresh behavior.

The package uses the portable root `plugin.json` format. If a client cannot find it, check that client's support for this format before changing the manifest. Update the source and refresh or reinstall the local plugin when testing edits; clients may run a cached copy.

## Install the standalone skill

Copy the entire `skills/engineering-writing/` folder, including `WRITING.md`, `references/`, and `agents/`, into an agent's supported skills directory. For Codex, a repository can use `.agents/skills/engineering-writing/`. The complete folder supplies the guide and references for standalone use.

## Test and maintain

The repository-root `WRITING.md` is the sole authored authority for writing rules. The skill bundles an exact distribution copy at `skills/engineering-writing/WRITING.md` so an installation can read the guide locally. Edit the root guide, then refresh and compare the bundled copy from the repository root:

```sh
cp WRITING.md plugins/engineering-writing/skills/engineering-writing/WRITING.md
cmp WRITING.md plugins/engineering-writing/skills/engineering-writing/WRITING.md
```

`SKILL.md` owns the workflow and routes to the guide. Its three focused references link to the owning guide sections and provide examples or task-specific guidance. The plugin manifest supplies installation metadata; it adds no hooks, tools, or global instructions.

In the source checkout, use `docs/evaluations/engineering-writing/scenarios.md` for behavioral checks. The adjacent `results.md` distinguishes structural validation, writing samples, and client installation evidence. Those development records live outside the plugin archive.

## Release status

Version 0.1.4 makes `WRITING.md` the writing authority, bundles an exact copy, and replaces duplicated rules with guide links. Its listing links point to `main`. The package includes icon assets, a [privacy policy](PRIVACY.md), and [terms of service](TERMS.md).

Local structural checks cover this package. The behavioral samples above cover version 0.1.0 and have not been rerun for 0.1.4. OpenAI's submission checks and developer identity verification happen in the submission dashboard; preparing the package does not submit or publish it.

The package declares availability in all supported countries and no payments or purchases. It is licensed under [Apache-2.0](LICENSE).
