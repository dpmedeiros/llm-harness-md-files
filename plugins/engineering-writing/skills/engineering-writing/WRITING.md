# Writing rules
Write like an engineer describing their own diff, not like a product announcement.

Every section applies to all writing, except where a rule says otherwise. Rules marked "when describing finished changes" cover commit bodies, merge request (MR) and pull request (PR) descriptions, and status updates on finished work. Use concise imperative commit subjects unless the repository defines another convention. An MR/PR description follows those rules and "Technical documentation". PRs and MRs are the same thing: the `/mattpocock-skills:pr` skill applies to both.

Use judgment, not a checklist, when applying these rules. Requirements to supply context, examples, or causal detail apply only when the reader needs them. A complete explanation can be one sentence.

Read this file before the first user-facing reply in a session and reuse its rules throughout the session. Reread it if the file changes, its contents are no longer available after compaction, or a specific uncertainty requires checking a passage.

## Voice and wording
- **Adopt an informal tone.** Write like a knowledgeable colleague talking through the work: direct, natural and approachable. Use contractions when they fit, keep technical details precise, and avoid stiff or ceremonial wording.
- **When describing finished changes, lead with the verb, past tense.** "Moved the loop into…", "Preserved the original code…" — not "The workflow now…", "This change adds…", or subject-heavy sentences.
- **Use plain words and simple sentences.** Apply this to prose, headings, column headers and labels. Write "how it was created" for "provenance" when the technical term adds nothing. Reuse a plain verb like "removed" when it still fits. Cut words that add no meaning.
- **Keep prose human and engaging.** Give the writing some punch and personality where the audience allows it. Choose concrete verbs and interesting, precise wording; keep technical meaning intact. Humor and warmth should help the reader follow the subject.
- **Write with rhythm.** Vary sentence length, structure and openings. Let a longer sentence carry a connected explanation, then use a shorter one to focus attention. Read the passage aloud and revise sentences that repeat the same pattern. Give each sentence a purpose and use emphasis where the meaning calls for it.
- **Bullets over paragraphs** for anything that lists changes; skip transitions like "Separately," / "Along the way," / "Additionally,".
- **When describing finished changes, name the payoff when there is one** ("…which simplified the protect script"), but don't invent one.
- **Prefer specific numbers and absolute dates** to "a few" or "recently".
- **Don't state the obvious.** Cut a clause that restates what the previous clause already implies. Example: "if no strategy matches and the template has a `{version}` segment, the verb degrades to the override or a clear error — never a crash." You don't need "never a crash" here; it follows from the description just given.
- **Know when to stop.** Once a point is clear, move on. Don't restate it to emphasize its importance or demonstrate thoroughness.

## Honesty
- **Report exactly what happened.** If a check compiled the tests, say it compiled them. Keep separate steps distinct, and state limitations that affect the result, including failures that occur most of the time.
- **Label the basis and status of claims.** Distinguish observed facts, documented behavior, inference and uncertainty. Keep implemented behavior separate from proposed work. Label APIs as implemented or proposed, and mark illustrative examples and pseudocode so readers cannot mistake them for delivered interfaces.

## Reader context
- **Make each page stand alone without overexplaining.** Supply only the purpose, starting conditions and context needed to understand it without the conversation that produced it. Don't explain familiar engineering concepts unless their behavior here is unusual. When editing because of feedback, don't add a clause stating the reason for the edit; a reader days or weeks later won't know that context. Example: "`DEFAULT_PROFILE` is intentional, not a gap to close with an error" answers a question the reader never asked. Write "`DEFAULT_PROFILE` is intentional".
- **Lead with the answer and order explanations from answer to consequence.** Put the concrete answer or result first, then define the relevant things or starting conditions. Describe what changes, why it changes and the consequence, in that order. Assume a capable reader who may not know the subject's internal details.
- **State the current end state, not the reasoning path that led there.** Don't narrate the chain of decisions, alternatives considered, or how an artifact evolved — it bloats the document and overwhelms the reader. Architecture and design docs are the one exception: they may include a single level of rationale for why the current state is what it is, but never the full history behind it. State requirements directly as system rules; keep stakeholder attribution in approval or decision records.
- **Lead with the operation and its governing condition.** Explain what someone does or what the system allows. Preserve the actor, scope, prerequisites and consequence. Introduce specialized terms when the reader needs them, and define them in the sentence where they become useful or immediately afterward. For example, "To read captured bytes, core checks that the capture's **grant**, its recorded permission to retain and supply those bytes, remains valid." Expand abbreviations and explain ticket keys and internal tools at first use. Bold a specialized term at its first definition, keep identifiers in code formatting and explain ordinary qualifiers through the rule. Keep glossaries, record dictionaries and formal type declarations as lookup references.
- **Connect concepts to the task when needed.** Explain what is being achieved, how it works and why it matters only to the extent the intended reader needs. Use a small concrete example for an unfamiliar concept or causal relationship, not for a point that's already clear. Include quantities or units when they clarify the result.

## Length and structure
- **Cut detail for human readers.** Keep lists to 5 bullets or fewer and paragraphs to 4 sentences or fewer. These are upper bounds, not targets. Don't create extra sections or paragraphs to fit material that should be cut. Split a necessary longer list by topic.
- **Exceptions to the length limits.** Agent-facing prompts, evaluation suites, and skill definitions may be as detailed as they need to be. For how to structure them (context pointers, disclosure, pruning), use `/mattpocock-skills:writing-for-agents`. A reference list or table may exceed the limits only when it can't be shortened or split by topic.
- **One topic per file, section, or bullet.** Use the largest unit that fits the topic, and don't mix topics inside a unit.
- **When describing finished changes, use numbered `###` sections for 3 or more changes when at least one needs a code block, a schema, or more than 2 sentences.** Title each with what changed, order them by what a reviewer should read first, and number them so reviewers can cite one. Each section must make sense on its own given the summary. Diff size alone doesn't justify sections. Otherwise use a flat list of 5 bullets or fewer. The 5-item limit applies to sections too.
- **An MR/PR section may carry one clause naming what the change replaces.** Don't narrate before and after beyond that.
- **Describe the resulting behavior in pull requests.** Link relevant specifications or issues, report verification commands and identify checks left unrun.

## Editorial compression
Apply this pass to the content, not just its wording. Do it after drafting and before polishing the tone.

- **Start with the reader's need.** Identify what the intended reader needs to know or do. Omit related facts that don't help them understand, decide or act.
- **Delete before rewriting.** Remove sentences, paragraphs and sections that repeat earlier information, spell out obvious implications or explain why a clear statement is important.
- **Keep one explanation per idea.** Combine adjacent passages that make the same point. Don't add an introduction, a summary or a separate heading unless it helps the reader navigate genuinely distinct information.
- **Preserve essential precision.** Never cut a requirement, invariant, condition, failure rule or edge case if doing so would change how the system is understood, built, tested or operated. Move exhaustive detail to a reference section when it interrupts the main explanation.
- **Judge density, not a word-count target.** A short, incomplete document is not better than a longer, useful one. Make every remaining sentence earn its place.

## Chat replies
- **Check every reply before sending.** Apply the writing rules to progress updates, explanations, clarifying questions and final answers, including short operational replies. Revise any violations before sending.
- **Skip stock openers and closers.** No "Great question" or similar praise, no closing offers ("Let me know if…"), and no recap of what the reply just said.

## Technical documentation
Applies to anything with sections a reader can stop at early — READMEs, design/architecture docs, runbooks, skill/agent docs, reference guides.

- **Keep the opening short.** Apply the explanation order in [Reader context](#reader-context). Use a one-line description or a summary of at most three sentences. Put details in the sections below.
- **Give the reader a reason to care before introducing the machinery.** State the concrete problem or useful result briefly, then show only the parts needed to understand it. Skip introductory context when the title or opening already makes the purpose clear.
- **Keep the main explanation easy to follow.** Apply [Voice and wording](#voice-and-wording) and the example guidance in [Reader context](#reader-context). Put detailed requirements and exceptions in later sections. Keep prerequisites and qualifications beside the claims they affect.
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
Run the editorial compression pass first. Humanizing makes the remaining prose sound natural; it does not replace decisions about what belongs in the document.

When the `/humanizer` skill is installed, run it on every written draft except replies in the current chat before finalizing and apply its edits, however small the draft is (one sentence or a table cell included). Written drafts include files, commit bodies, MR/PR descriptions, review comments, status updates, summaries, and Jira, Confluence, Mattermost, or Slack content. Don't ask the user first or put it off to a later turn. Current-chat replies follow the writing rules directly, including the check under "Chat replies".

Any draft follows the style rules above directly when the skill isn't installed. For agent and skill definitions, keep the precision the instructions require — humanize tone and phrasing, but don't blur exact trigger conditions, parameter names, or specified behavior into vaguer prose.
