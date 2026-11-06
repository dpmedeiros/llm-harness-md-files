# Documentation and technical explanations

Use [Technical documentation](../WRITING.md#technical-documentation) for document structure, [Reader context](../WRITING.md#reader-context) for explanations and terms, and [Workflows and diagrams](../WRITING.md#workflows-and-diagrams) for processes. For interface contracts, read [API references](../WRITING.md#api-references).

For procedures, describe each check precisely enough that the reader can recognize success before continuing.

## Illustrative explanation

> A worker holds a **lease**, a stored claim on a job that expires at a recorded time. If the worker stops renewing it, the recovery scanner clears the expired claim. The job then becomes available for another worker to claim; the actual start time depends on when a worker next polls.
