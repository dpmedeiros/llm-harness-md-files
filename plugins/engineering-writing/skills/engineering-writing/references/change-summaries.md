# Change summaries

Describe what changed and what the available checks establish. Apply the shared principles in [the skill entry point](../SKILL.md).

## Lead with the change

For finished work, prefer a concrete past-tense verb: “Moved the parser into the import module” or “Preserved event order across batches.” Follow repository conventions for commit subjects and any supplied template for the body.

Give the purpose or useful result when it helps a reviewer understand the change. Include a concrete trigger or example when the behavior would otherwise be hard to assess. Keep the description centered on the final implementation and its relevant implications.

Use a short paragraph or flat list for a small change. For several changes that each need an explanation, use focused sections in the order a reviewer should read them. Number sections when that makes review references easier. Let the repository template and the complexity determine the structure.

## Report validation precisely

Name the check and state its observed result. A compile check establishes compilation; test results cover the cases actually run. Identify checks that remain unperformed when they matter to the assessment. Treat expected performance or reliability benefits as expectations until measurements support them.

State material risks and limitations supported by the change or its evidence. Keep an unknown as an unknown. If a template requires a risk section and no specific risk is established, state the relevant validation limit plainly.

Illustrative example:

> Batched repository writes in groups of up to 100 events. Preserved event order and the transaction boundary.
>
> `cargo check` passed. Tests and benchmarks were not run, so performance impact remains unmeasured.

## Match the destination

A PR or MR description should make sense to a reviewer who has not seen the chat. A commit body can be shorter when the subject and diff supply context. Release notes should focus on behavior relevant to their users. A progress update should distinguish finished work from what remains.
