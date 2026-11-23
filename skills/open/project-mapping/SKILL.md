---
name: project-mapping
description: Map a repository and build or refresh its linked developer documentation. Use for project discovery, architecture and business-flow mapping, or documentation sync after team changes. Proactively interview the developer to resolve gaps in intent.
license: MIT
---

# Project Mapping

Learn enough about the repository to give a developer or another agent a verified route into the code. Keep application code, tests, and configuration read-only. Write in the repository's documentation locations and honor a read-only request across the whole repo.

## Communicate with the developer

Phrase questions, answers, and explanations in plain language for a mid-level developer. Lead with the concrete behavior or decision and explain unfamiliar technical jargon briefly when it matters.

Make each substantive question or request for confirmation understandable on its own, including when it appears in a batch or question picker. Briefly state what you found or what is proposed, where it happens, and what the answer would change. Put that context in the question itself and link to the most relevant source or test, with a line reference when available.

For an API question, name the HTTP method and route, plus the controller action or handler and any service method central to the decision. For other questions, name the relevant screen, workflow step, class, or method. Use verified identifiers and say when a detail is still unknown.

Use the user's language for the conversation. When it is a language other than English, keep project-specific business terms in English. Prefer the English terms used in the project's glossary, docs, or code. Use a clear English equivalent when the project provides no English term, and explain its meaning in the user's language if needed.

## Choose the scope

A bare invocation or a broad request to map, investigate, or understand the project starts a repository-wide discovery in short sessions. Begin from the repository root and build toward coverage of every major component, including shared modules and external integrations that affect the architecture. A named component or flow narrows the scope. A request to reconcile recent changes uses the sync workflow below.

## Discover and map the project

1. Read the applicable repository instructions and locate the existing docs entry point. Use it to guide discovery. Survey the components and entry points in scope, how they fit together, and the data, contracts, or dependencies they share.
2. Identify the main business flows and user journeys and trace representative ones through the relevant screens, code, tests, or configuration. Record the trigger, rules, handoffs, and outcome. Link consequential claims to files and name the relevant symbols or test scenarios. In a broad review, give each major component a place in the map and identify which flows have been traced in depth.
3. Build or refresh the linked Markdown documentation as you go. Create or update a short entry point and an architecture map with the verified relationships. Add flow pages, glossary entries, coding standards, and decisions as the evidence and discussion warrant. Keep visible which findings describe observed behavior, which reflect confirmed intent, and which questions remain open.

## Investigate the database

When a flow depends on a database, read [database investigation](references/database-investigation.md). Map the relevant objects and code paths in the current round, using read-only MCP evidence when available.

## Work in short, resumable sessions

A session is one useful pass over a bounded topic, such as a component boundary, a business flow, or a cluster of recent changes. Start with an existing mapping continuation note, including a note saved by an earlier KT run, when it matches the request. On a fresh repository-wide pass, build the high-level map and choose one area to trace. Treat whole-repo coverage as a goal across sessions.

1. Investigate the facts you can verify in code, tests, and existing docs. Add or refresh the relevant pages as you learn, including glossary entries, rules, and links. Record verified behavior and keep any unconfirmed intent open. Save this work before handing questions to the developer.
2. Ask one round of up to five material questions, including confirmations in discovery and sync. Prioritize the questions that most affect the docs. Group related findings, show the evidence, and explain what each answer would change. Ask fewer when that covers the remaining material questions.
3. Apply the answers you receive to the owning pages and summarize the round. When work remains, update a short continuation note in or linked from the docs index. Include the scope covered, links to relevant pages or evidence, deferred or unanswered questions, and the next area to investigate. Save the note before yielding control. If the developer asks to stop during a round, save the same handoff and finish.
4. After saving the round, ask in the developer's language whether they want another round or want to stop here. Offer those two choices as a separate check-in, outside the five questions. Wait for an explicit choice to continue before starting another round of up to five. If they stop, finish with the saved handoff. When the requested work is complete, summarize the result and finish.

On a later invocation, read the note and linked pages, skip settled questions, and verify evidence again where the code may have changed. If the developer requests read-only work, give the same continuation details in the session summary.

## Confirm important findings

During an initial map as well as later reviews, bring newly discovered or materially changed architectural choices, business rules, and coding conventions to the developer for confirmation. Do this even when their current behavior is clear in code. Group related findings and show how the approach works today, the evidence for it, and why it matters. Ask whether to keep it as an intended direction, revisit it later, or leave the decision open.

Record the verified current behavior where it helps readers understand the code. Record it as an agreed direction only after confirmation. If the developer wants to revisit it, add a follow-up to the repo's existing documentation or to a short follow-up section in the owning page. Capture what should be revisited, why, and a link to the evidence. Mark undecided findings as open and leave implementation for a separate task.

## Sync after team changes

Use this workflow when rerunning KT on a newer checkout or when the developer names changes that may have made the docs stale.

1. Identify the checked-out revision and the review scope. Compare it with a Git ref supplied by the developer or a documented last-reviewed commit for that scope, if available and valid. Use the diff to locate changes in behavior, contracts, ownership, architecture, and enforcement, including moved or deleted code. If there is no usable baseline, compare the relevant docs and their links with the current code and tests. Recent commits can help prioritize that review. State the range or areas actually reviewed and any coverage limits.
2. Trace consequential differences back to source and tests. For each, show what the docs say, what the current implementation does, and why the difference matters. Ask the developer whether the change is intended, a deviation to fix, or still undecided. Ask even when the docs are silent if the finding would establish a new business rule, architectural decision, or coding standard.
3. Update the owning pages and links for confirmed decisions. Keep rejected or undecided behavior out of accepted architecture, rules, and standards. Report it as a discrepancy with evidence, or record it as a known deviation if requested. Mechanical link and path repairs verified against the repository can be made independently. Leave fixes to application code for a separate task.

If tracking a last-reviewed commit helps repeat this review, record it with the scope in the existing docs index. Advance it for that scope after review only when material findings have been resolved or explicitly tracked as open. An initial comparison against current code establishes coverage only for the areas actually reviewed.

## Maintain documentation links

Read [link usage and review](references/link-usage.md) when working with project documentation. Record links you use and review the relevant links in the areas you explore. Use the same local journal as Grill Reqs. If a link requires a decision from the developer, include it within the five-question round or carry it to the continuation note.

## Build and maintain the documentation

Use the repo's established structure. When there is none, start with a short `docs/README.md` linking to the first useful page. Add pages as evidence and scope warrant:

- An architecture overview and pages under `docs/flows/` for system behavior, user journeys, and project workflows. Link to the screens, code, tests, or project instructions that support the account.
- `GLOSSARY.md` for verified or developer-confirmed domain terms.
- `CODING_STANDARDS.md` for established team conventions for the codebase that require judgment. Treat repeated patterns in code as candidates until a documented rule or the developer confirms them. Link to automated checks for existing mechanical rules.
- `docs/adr/` for confirmed consequential decisions and their rationale. Preserve the distinction between an observed design and a decision whose rationale is known.

Update the page that already owns a topic. Use descriptive relative links between related pages and to relevant source files. On repeat runs, recheck the pages touched by the exploration, repair broken links, and consolidate duplicates when the surviving path preserves useful context. Use low relevance as a reason to review a page and evidence of redundancy or supersession to decide what to retire.

### Record why a page matters

When creating or updating a linked Markdown documentation page, ensure it has a name, a short description of what it covers, and a `why` that states when to consult it and what decision it informs or mistake it helps prevent. Follow the target repo's metadata conventions. By default, use the page title as its name and put `description` and `why` in YAML frontmatter.

Keep `why` to one concrete sentence grounded in verified behavior or confirmed intent. Add it to existing pages as you edit them, and revise it when the page's purpose changes. If the purpose is unclear, flag it as an open question. Use the `why` to judge whether a linked page is relevant to the current task.

Check changed links and report the areas covered, documentation updated, and questions still open. State where a later mapping session can continue if the requested scope is broader than the area verified.
