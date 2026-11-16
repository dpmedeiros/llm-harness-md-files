# Documentation and technical explanations

Use [Reader context](../WRITING.md#reader-context) for explanations and terms. Apply the sections below for document structure, interface contracts and processes.

## Technical documentation
Applies to anything with sections a reader can stop at early — READMEs, design/architecture docs, runbooks, skill/agent docs, reference guides.

- **Keep the opening short.** Apply the explanation order in [Reader context](../WRITING.md#reader-context). Use a one-line description or a summary of at most three sentences. Put details in the sections below.
- **Give the reader a reason to care before introducing the machinery.** State the concrete problem or useful result briefly, then show only the parts needed to understand it. Skip introductory context when the title or opening already makes the purpose clear.
- **Keep the main explanation easy to follow.** Apply [Voice and wording](../WRITING.md#voice-and-wording) and the example guidance in [Reader context](../WRITING.md#reader-context). Put detailed requirements and exceptions in later sections. Keep prerequisites and qualifications beside the claims they affect.
- **Order sections by how often a reader needs them.** Common path first; edge cases, advanced configuration, and rare failure modes later or in a linked reference.
- **Push deep detail out of the main flow.** Full option lists, implementation internals, and exhaustive edge cases belong in subsections, appendices, or separate reference files.
- **Don't require later sections to understand earlier ones.** A reader should be able to stop after any section and have a correct, if incomplete, understanding.
- **Maintain design documentation with the design.** When code introduces or changes a design, update the affected documentation. Revise existing sections in place and add a section only for a concept they do not already cover.

### API references

For each API reference, explain its purpose and bare contract in one or two short paragraphs stating what the operation does and who calls it. State **Input**, **Output** and **Side effects** explicitly, including "none" when applicable. These details may be comments beside a language-neutral interface definition or source comments beside the interface or trait.

Keep one interface definition instead of repeating it in a table or another rendering. Include ownership/lifetime, completion and failure rules when they affect use, and link shared types to their owning definitions. Distinguish computed or staged results from committed results, and state who may read, publish or persist them.

## Workflows and diagrams

Applies when explaining a process, design or behavior.

- **Make necessary causal steps explicit.** For workflows where the sequence matters, state the goal and prerequisites, who performs each operation, what it reads or writes, and the result. Include intermediate steps needed to explain the outcome, but don't turn a simple operation into an exhaustive walkthrough.
- **Name the kind of commit.** When discussing both databases and version control, distinguish database transaction commits from Git commits.
- **Use diagrams freely when they clarify the subject.** Show workflows, ownership, dependencies, state changes or comparisons when a picture makes the relationship easier to follow. Define terms before the diagram and explain its relevant result or example afterward. Match the detail to the audience: technical diagrams can name concrete objects and transaction boundaries; investor diagrams should show simple user journeys and benefits.

For procedures, describe each check precisely enough that the reader can recognize success before continuing.

## Illustrative explanation

> A worker holds a **lease**, a stored claim on a job that expires at a recorded time. If the worker stops renewing it, the recovery scanner clears the expired claim. The job then becomes available for another worker to claim; the actual start time depends on when a worker next polls.
