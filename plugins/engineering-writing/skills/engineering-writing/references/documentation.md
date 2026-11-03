# Documentation and technical explanations

Help the reader understand or use the subject from the point where they arrive. Apply the shared principles in [the skill entry point](../SKILL.md).

## Start with the useful result

Open a document with a short statement of what it is for, usually one to three sentences. Introduce the concrete problem or result before naming the machinery that produces it.

Supply prerequisites beside the action that depends on them. Order a procedure so the reader can perform it: starting conditions, action, observable result, then the next action. Describe a check precisely enough that the reader can recognize success.

Order explanatory sections by how often the reader needs them. Put the common path first and disclose full option lists, internals, and rare cases later. Each section should give a correct understanding even if the reader stops there.

## Introduce terms through their use

Usually use an unfamiliar term in a concrete sentence, then define its local meaning immediately afterward. Bold the term at its first definition when the document's style supports it, and keep identifiers in code formatting. Expand an abbreviation before relying on it elsewhere.

For a process, identify who acts, what they read or write, and what that operation produces. Connect those operations to the outcome. A diagram can show ownership, dependencies, or state changes; define its terms before relying on them and explain the relevant result afterward.

Illustrative example:

> A worker holds a **lease**, a stored claim on a job that expires at a recorded time. If the worker stops renewing it, the recovery scanner clears the expired claim. The job then becomes available for another worker to claim; the actual start time depends on when a worker next polls.

The stored claim, the scanner's write, and the job's availability explain the causal relationship. Add exact timing only when the source establishes it.

## Describe the current behavior

Explain the state or contract the reader will use. Architecture and design documents may include concise rationale and meaningful tradeoffs. Give migration history a place when the document's purpose requires it.

Keep qualifications beside the claims they qualify. For an API, describe its purpose, inputs, outputs, and side effects at its authoritative declaration or reference location. Scale examples and detail to what the reader needs to act or understand.
