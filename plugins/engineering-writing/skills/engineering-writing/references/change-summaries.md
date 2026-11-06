# Change summaries

Use [Voice and wording](../WRITING.md#voice-and-wording) for finished changes, [Honesty](../WRITING.md#honesty) for validation claims, and [Length and structure](../WRITING.md#length-and-structure) for commit bodies and PR/MR descriptions. Apply [Technical documentation](../WRITING.md#technical-documentation) to PR/MR descriptions as directed by the guide.

## Match the destination

A commit body can be shorter when the subject and diff supply context. Release notes should focus on behavior relevant to their users. A progress update should distinguish finished work from what remains.

## Illustrative change summary

> Batched repository writes in groups of up to 100 events. Preserved event order and the transaction boundary.
>
> `cargo check` passed. Tests and benchmarks were not run, so performance impact remains unmeasured.
