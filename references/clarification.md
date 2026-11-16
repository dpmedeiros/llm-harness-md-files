# Clarification and document synchronization

## Learn from clarification and confusion

When the user asks for clarification, expresses confusion, or corrects an explanation or design, use that feedback to improve both the current project and future work. Make the necessary in-repo and agent-guidance changes as part of the task at [document synchronization checkpoints](#document-synchronization-checkpoints).

- Answer the immediate question clearly, then inspect what caused the confusion. Distinguish missing context or unclear wording from a design defect; a question alone does not establish that the design is wrong.
- Fix the cause in the files that own it: documentation, specifications, examples, names, interfaces, workflows, or implementation as needed. Write for the next reader, with enough context to understand the result without this conversation.
- Capture the reusable lesson in the relevant agent guidance. Keep project-specific rules in the project and put broadly applicable writing or design lessons in shared guidance. Revise existing rules where possible and keep each lesson in one authoritative place.
- Apply the lesson recursively: check related material and the new edits for the same cause, correct affected parts, and remove conflicting or obsolete guidance. Stop when the identified cause is addressed across the relevant scope; keep unrelated cleanup out of the task.
- Verify the changes against the clarification and current sources, using the required checks for any behavior changes. Briefly report what changed and what remains unresolved. If no persistent change is warranted, explain why.

### Document synchronization checkpoints

During a design discussion, answer the current question and keep provisional decisions and pending edits in the conversation or existing review log. An exploratory question alone establishes no requirements change. Follow the project's checkpoint procedure when one is provided.

Otherwise, synchronize authorized changes when a coherent topic is settled, when the user explicitly requests an update, and before dependent design work, approval, implementation or handoff. At a handoff with open questions, apply settled changes and identify the remaining provisional decisions and pending edits. Run the applicable checks on the synchronized changes. A checkpoint grants no approval or implementation authorization.

Record a rejected proposal immediately and remove it and unsupported dependents from the active proposal. Reconcile its owning documents through the project's synchronization procedure before approval, implementation or another Story consumes the changed contract. Apply required approval-state changes immediately.
