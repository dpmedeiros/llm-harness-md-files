# Engineering writing

Draft and revise engineering communication with enough context for a new reader, explicit causal steps, and claims that match the evidence. The skill adapts its defaults to your audience, voice, templates, and project conventions.

## Use the skill

Use it for documentation and explanations, change summaries, review comments, and work messages. For example:

```text
Use $engineering-writing to revise this explanation for an engineer new to the service.
```

It can also be selected automatically for relevant tasks. Installing it makes it available to the model; selection on every reply is not guaranteed. It requires no other skills, account connections, or configuration.

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

Copy the entire `skills/engineering-writing/` folder, including `references/` and `agents/`, into an agent's supported skills directory. For Codex, a repository can use `.agents/skills/engineering-writing/`. Copying only `SKILL.md` loses its focused references.

## Test and maintain

The entry point owns the shared rules. Its three references add guidance for particular kinds of communication. The plugin manifest supplies installation metadata; it adds no hooks, tools, or global instructions.

In the source checkout, use `docs/evaluations/engineering-writing/scenarios.md` for behavioral checks. The adjacent `results.md` distinguishes structural validation, writing samples, and client installation evidence. Those development records live outside the plugin archive.

The original `WRITING.md` remains the author's personal guide and is unchanged by this extraction. The package maintains its own rules; shared improvements require deliberate transfer during this initial version.

## Release status

Version 0.1.0 is a local package for review and testing. No license is declared in the package; select one before public release. No public directory submission is included.
