# Skill authoring

Apply these rules when creating or editing an agent skill.

## One authoritative home per rule

State each rule fully in its owning file or section. At consuming steps, use a precise pointer that names when to read it. Preserve trigger conditions, required actions, exceptions and completion criteria when moving a rule.

A checklist that paraphrases an existing rule creates another copy. In final verification, name the files or sections to reread. Use checkboxes for requirements stated nowhere else, such as build commands. Compare checklists across the skill's files and replace repeated rules with pointers to their owner.

For a near-identical test variant, give a prose instruction instead of repeating its code block, such as: "Generate a third test: copy X, change Y and assert Z."

## Directives

State the required action directly. Keep conditions and necessary guardrails beside it. Omit commentary that merely announces the directive as the standard or repeats a rejected alternative.

Name the annotation, pattern or command to use. Explain framework mechanics only when the agent needs them to act correctly; explain a directive's reason when it is not obvious.
