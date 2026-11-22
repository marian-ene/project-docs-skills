---
name: grill-reqs
description: Interview the developer to clarify requirements for one upcoming change. Use project docs, code, and tests to resolve questions about a requirements brief, story, use case, or acceptance criteria and document settled decisions before implementation.
license: MIT
---

# Grill Reqs

Interview the developer about the requirements for one change until its behavior, boundaries, and key implementation decisions are clear. Use the repository's durable documentation as working context. Keep application code and configuration read-only during the walkthrough.

## Communicate with the developer

Phrase questions, answers, and explanations in plain language for a mid-level developer. Lead with the concrete behavior or decision and explain unfamiliar technical jargon briefly when it matters.

Make each substantive question or request for confirmation understandable on its own, including when it appears in a batch or question picker. Briefly state what you found or what is proposed, where it happens, and what the answer would change. Put that context in the question itself and link to the most relevant source or test, with a line reference when available.

For an API question, name the HTTP method and route, plus the controller action or handler and any service method central to the decision. For other questions, name the relevant screen, workflow step, class, or method. Use verified identifiers and say when a detail is still unknown.

Use the user's language for the conversation. When it is a language other than English, keep project-specific business terms in English. Prefer the English terms used in the project's glossary, docs, or code. Use a clear English equivalent when the project provides no English term, and explain its meaning in the user's language if needed.

## Ground the story

- Start from the requirements, story, or use case supplied by the developer. Use any existing acceptance criteria and constraints to frame the discussion. Identify the affected flow, the user-facing outcome where relevant, and any project workflow it touches.
- Follow the applicable repo instructions and start from its docs entry point. Open the relevant flow pages, glossary entries, coding standards, or ADRs. Follow their links into code and tests to verify current behavior and constraints. Use focused code search to fill gaps where the docs are sparse.
- Surface discrepancies that affect the story, with links to the evidence. Keep current behavior, requested behavior, and open decisions distinct.

## Investigate the database

When the story depends on database behavior, read [database investigation](references/database-investigation.md). Reuse the existing database docs and use read-only MCP to verify the dependencies that affect the story.

## Maintain documentation links

Read [link usage and review](references/link-usage.md) when working with project documentation. On every story, record the links you use, check relevant outgoing links on pages you review, and repair verified broken or obsolete links. Review low-use candidates for those pages and flag anything that needs a decision. This workflow works on its own after initial discovery.

## Record why a page matters

When creating or updating a linked Markdown documentation page, ensure it has a name, a short description of what it covers, and a `why` that states when to consult it and what decision it informs or mistake it helps prevent. Follow the target repo's metadata conventions. By default, use the page title as its name and put `description` and `why` in YAML frontmatter.

Keep `why` to one concrete sentence grounded in verified behavior or confirmed intent. Add it to existing pages as you edit them, and revise it when the page's purpose changes. If the purpose is unclear, flag it as an open question. Use the `why` to judge whether a linked page is relevant to the current task.

## Clarify decisions with the developer

- Check the repo for answerable facts first. Ask questions in dependency order about behavior, edge cases, scope, or trade-offs that affect the story or how acceptance will be verified. Give your recommended answer and the evidence or trade-off behind it. Group independent questions when that helps the discussion.
- As decisions settle, update the owning Markdown page if the result is useful beyond this story. Capture confirmed business vocabulary, user journeys and workflows, observed behavior verified in code or tests, and durable architecture decisions or constraints. Use [documentation guidance](references/documentation.md) when choosing where to record a new note.
- Keep proposed behavior in the story notes or mark it explicitly as an agreed future design. Document it as current behavior once verified in the implementation. Honor requests for a read-only discussion.

When the story is clear enough to hand off, summarize the agreed scope, clarified acceptance criteria, decisions and rationale, suggested verification, and any remaining blockers. Check links in changed Markdown. The handoff can feed a later spec or ticketing step.
