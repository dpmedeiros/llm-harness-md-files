# Skill authoring

Apply these rules when creating or editing an agent skill.

## Progressive disclosure

Keep the purpose, common steps and constraints needed on every invocation in `SKILL.md`. Put substantial detail for a particular mode, provider, format or unusual case in a focused reference, with a precise pointer that says when to read it. Read only the references needed for the current task.

Split by a real task branch: one provider's deployment instructions or one document format's editing procedure can be loaded independently. Keep a short, self-contained skill in one file when an extra routing layer would add no useful choice.

When moving rules, follow [one authoritative home per rule](#one-authoritative-home-per-rule). Inspect consumers that copy, load or fingerprint the instructions, and update them with the moved files so isolated workflows retain the same rules and protections.

## One authoritative home per rule

State each rule fully in its owning file or section. At consuming steps, use a precise pointer that names when to read it. Preserve trigger conditions, required actions, exceptions and completion criteria when moving a rule.

A checklist that paraphrases an existing rule creates another copy. In final verification, name the files or sections to reread. Use checkboxes for requirements stated nowhere else, such as build commands. Compare checklists across the skill's files and replace repeated rules with pointers to their owner.

For a near-identical test variant, give a prose instruction instead of repeating its code block, such as: "Generate a third test: copy X, change Y and assert Z."

## Directives

State the required action directly. Keep conditions and necessary guardrails beside it. Omit commentary that merely announces the directive as the standard or repeats a rejected alternative.

Name the annotation, pattern or command to use. Explain framework mechanics only when the agent needs them to act correctly; explain a directive's reason when it is not obvious.
