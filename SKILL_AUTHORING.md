# Skill Authoring

Rules for writing and editing Claude Code skill files. Apply them when creating or updating any skill.

## Checklists point to sources

A checklist item that restates a rule from the same skill is a second copy that will drift. In the final verification step, name the files or sections to re-read instead of paraphrasing them. Use real checkboxes only for items stated nowhere else in the skill, such as build commands. Before finalizing, compare every checklist across the skill's sub-files and replace items in the less authoritative file with a pointer to the authoritative one.

## State the directive alone

Write the directive and stop. Leave out "do not use X" and "only fall back to Y when..." asides about the rejected alternative, since naming it keeps it in the agent's context and makes it more likely to be used.

## State what to do, not how the framework works

Name the annotation, pattern or command to use, and leave out the mechanism behind it (Spring binding, serialization, auto-resolution). This covers mechanics only. When the reason for a directive isn't obvious, state the reason.

## One authoritative home per rule

When a rule is needed in several files, state it fully in the most authoritative one and replace every other occurrence with a one-line reference. For a test method that is a near-identical variant of another, give a prose instruction instead of repeating the code block, e.g. "GENERATE a third test: copy X verbatim, but change Y and assert Z."

## State the standard without commenting on it

Delete lines like "This is the go-forward standard. Do not rearrange X without explicit request." The directive is the standard, and a line announcing it adds nothing.
