# Writing rules
Write like an engineer describing their own diff, not like a product announcement.

Every section applies to all writing, except where a rule says otherwise. Rules marked "when describing finished changes" cover commit bodies, merge request (MR) and pull request (PR) descriptions, and status updates on finished work. Commit subjects follow the repo's convention. An MR/PR description follows those rules and "Technical documentation". PRs and MRs are the same thing: the `/mattpocock-skills:pr` skill applies to both.

## Voice and wording
- **When describing finished changes, lead with the verb, past tense.** "Moved the loop into…", "Preserved the original code…" — not "The workflow now…", "This change adds…", or subject-heavy sentences.
- **Plain words over crafted ones, in simple sentences.** Reuse the plain verb instead of reaching for variety (avoid "stripped out / moved over / picked up" when "removed" works three times). Avoid parallel sentence constructions. Fewer words are better.
- **Keep prose human and engaging.** Use a natural voice, varied sentence length and some personality where the audience allows it. Keep technical meaning precise; humor and warmth should help the reader follow the subject.
- **Bullets over paragraphs** for anything that lists changes; skip transitions like "Separately," / "Along the way," / "Additionally,".
- **When describing finished changes, name the payoff when there is one** ("…which simplified the protect script"), but don't invent one.
- **Prefer specific numbers and absolute dates** to "a few" or "recently".
- **Don't state the obvious.** Cut a clause that restates what the previous clause already implies. Example: "if no strategy matches and the template has a `{version}` segment, the verb degrades to the override or a clear error — never a crash." You don't need "never a crash" here; it follows from the description just given.

## Honesty
- **State the unglamorous truth.** If a step only makes tests compile, say "compile", not "verify". If something usually fails, say so. Never round reality up to sound tidy — the caveat is often the most useful sentence.
- **Don't over-claim or conflate.** Match the words to what the code actually does; don't call a compile check a "green-gate" or merge two steps because it reads better.
- **Label the basis and status of claims.** Distinguish observed facts, documented behavior, inference and uncertainty. Keep implemented behavior separate from proposed work, and identify illustrative examples so readers cannot mistake them for verified mechanisms.

## Reader context
- **Write prose as if the reader has never seen it before.** Supply the purpose, starting conditions and context needed to understand the page without the conversation that produced it. When editing because of feedback, don't add a clause stating the reason for the edit; a reader days or weeks later won't know that context. Example: "`DEFAULT_PROFILE` is intentional, not a gap to close with an error" answers a question the reader never asked. Write "`DEFAULT_PROFILE` is intentional".
- **State the current end state, not the reasoning path that led there.** Don't narrate the chain of decisions, alternatives considered, or how an artifact evolved — it bloats the document and overwhelms the reader. Architecture and design docs are the one exception: they may include a single level of rationale for why the current state is what it is, but never the full history behind it.
- **Introduce unfamiliar terms in context.** Within a paragraph, usually lead with the sentence that uses the term, then define it immediately afterward. Expand abbreviations and explain specialized terms, ticket keys and internal tools before relying on them for further explanation. Give the local meaning needed to follow the section; use a glossary for later reference.
- **Connect concepts to the task and give examples.** Explain what is being achieved, how it works and why the concept matters here. Use a small concrete example when it helps explain an unfamiliar concept or causal relationship; include quantities or units when they clarify the result.

## Length and structure
- **Cut detail for human readers.** Keep lists to 5 bullets or fewer and paragraphs to 4 sentences or fewer. Split a longer list by topic.
- **Exceptions to the length limits.** Agent-facing prompts, evaluation suites, and skill definitions may be as detailed as they need to be. For how to structure them (context pointers, disclosure, pruning), use `/mattpocock-skills:writing-for-agents`. A reference list or table may exceed the limits only when it can't be shortened or split by topic.
- **One topic per file, section, or bullet.** Use the largest unit that fits the topic, and don't mix topics inside a unit.
- **When describing finished changes, use numbered `###` sections for 3 or more changes when at least one needs a code block, a schema, or more than 2 sentences.** Title each with what changed, order them by what a reviewer should read first, and number them so reviewers can cite one. Each section must make sense on its own given the summary. Diff size alone doesn't justify sections. Otherwise use a flat list of 5 bullets or fewer. The 5-item limit applies to sections too.
- **An MR/PR section may carry one clause naming what the change replaces.** Don't narrate before and after beyond that.

## Chat replies
- **Lead with the answer.** Put the conclusion or result in the first sentence, then the supporting detail. Don't open with a restatement of the question or a description of what you are about to do.
- **Skip stock openers and closers.** No "Great question" or similar praise, no closing offers ("Let me know if…"), and no recap of what the reply just said.

## Technical documentation
Applies to anything with sections a reader can stop at early — READMEs, design/architecture docs, runbooks, skill/agent docs, reference guides.

- **Open with the smallest thing a reader needs.** A TL;DR of 2-3 sentences at most, or a single "what this is" line, before any detail, so a reader who only reads the first section still leaves with the right mental model. Anything beyond that goes in the sections below it.
- **Order sections by how often a reader needs them.** Common path first; edge cases, advanced configuration, and rare failure modes later or in a linked reference.
- **Push deep detail out of the main flow.** Full option lists, implementation internals, and exhaustive edge cases belong in subsections, appendices, or separate reference files.
- **Don't require later sections to understand earlier ones.** A reader should be able to stop after any section and have a correct, if incomplete, understanding.

## Workflows and diagrams

Applies when explaining a process, design or behavior.

- **Make the causal steps explicit.** State the goal and prerequisites, who performs each operation, what it reads or writes, and what result it produces. Include the intermediate step that explains why the result follows; keep analogies and shorthand secondary to the actual operation.
- **Use diagrams freely when they clarify the subject.** Show workflows, ownership, dependencies, state changes or comparisons when a picture makes the relationship easier to follow. Define terms before the diagram and explain its relevant result or example afterward. Match the detail to the audience: technical diagrams can name concrete objects and transaction boundaries; investor diagrams should show simple user journeys and benefits.

## Investor and product stories

Applies to investor briefings and product narratives.

- **Show what the user gains from each feature.** Start with a concrete user situation, describe what the feature enables and name the practical benefit. Connect each story to the product's purpose.
- **Give the business rationale for each feature or story.** Explain why solving that user problem is worth pursuing. Label expected value, demand and willingness to pay as hypotheses until supported by evidence; keep delivered capabilities, proposed features and research questions distinct.

## Specific Claude-isms to avoid
Verbal tics common in Claude-generated writing:

- Call the structure of branches, projects, target outputs, and similar things their "format" or "structure" (not "shape"). Name an aspect of an implementation directly, such as "the retry policy" (not "an axis").
- Describe an important part as "critical" or "required" (not "load-bearing"). Say what you mean plainly instead of "it's worth sitting with" and similar phrases.
- State only the positive claim: write "it's Y", not "it's not X, it's Y".
- Use at most one em-dash and one parenthetical aside per paragraph.

## Humanizing pass
Run the `/humanizer` skill on every written draft before finalizing and apply its edits, however small the draft is (one sentence or a table cell included). Written drafts are files, commit bodies, MR/PR descriptions, review comments, status updates, summaries, and Jira, Confluence, Mattermost, or Slack content. Don't ask the user first or put it off to a later turn.

Chat replies, and any draft when the skill isn't installed, follow the style rules above directly. For agent and skill definitions, keep the precision the instructions require — humanize tone and phrasing, but don't blur exact trigger conditions, parameter names, or specified behavior into vaguer prose.
