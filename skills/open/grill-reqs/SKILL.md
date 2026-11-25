---
name: grill-reqs
description: Interview the developer to clarify requirements for one upcoming change. Use project docs, code, and tests to settle the behavior and acceptance criteria, then agree on the concrete code design before handing off to implementation.
license: MIT
---

# Grill Reqs

Interview the developer about the requirements for one change until its behavior, boundaries, and key implementation decisions are clear. Use the repository's durable documentation as working context. Keep application code, tests, and configuration read-only during the walkthrough.

## Communicate with the developer

Phrase questions, answers, and explanations in plain language for a mid-level developer. Lead with the concrete behavior or decision and explain unfamiliar technical jargon briefly when it matters.

Make each substantive question or request for confirmation understandable on its own, including when it appears in a batch or question picker. Briefly state what you found or what is proposed, where it happens, and what the answer would change. Put that context in the question itself and link to the most relevant source or test, with a line reference when available.

For an API question, name the HTTP method and route, plus the controller action or handler and any service method central to the decision. For other questions, name the relevant screen, workflow step, class, or method. Use verified identifiers and say when a detail is still unknown.

Use the user's language for the conversation. When it is a language other than English, keep project-specific business terms in English. Prefer the English terms used in the project's glossary, docs, or code. Use a clear English equivalent when the project provides no English term, and explain its meaning in the user's language if needed.

## Ground the story

- Start from the requirements, story, or use case supplied by the developer. Use any existing acceptance criteria and constraints to frame the discussion. Identify the affected flow, the user-facing outcome where relevant, and any project workflow it touches.
- When the developer brings a paused implementation handoff, read the task, spec, evidence, and the recorded question. Treat any partial code as work in progress. Clarify whether to retain the agreed scope, revise it, defer part of it, or drop the change. Record the developer's decision and what it changes for To Spec and To Tasks.
- Follow the applicable repo instructions and start from `docs/brain/README.md` or the existing docs entry point if the project has yet to adopt this layout. Open the relevant flow pages, glossary entries, coding standards, or ADRs. Follow their links into code and tests to verify current behavior and constraints. Use focused code search to fill gaps where the docs are sparse.
- If the developer prepared a scaffold to show the intended code structure, inspect the relevant folders and files, including empty files, stubs, and relevant untracked files. Use the scaffold as the starting structure for the code design discussion.
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

## Close the discussion with the code design

Once you and the developer agree on the behavior, scope, and acceptance criteria, make the concrete code design the final part of the discussion. Walk through the proposed changes using the current code and any developer-provided scaffold.

Before proposing the design, read [Load applicable coding practices](../code-review/SKILL.md#load-applicable-coding-practices) and the guides it identifies for the affected code. Use the C# guide for C# changes and the Angular UI guide when the affected package is confirmed to use Angular 21 or later. Load both for mixed changes when applicable. If the sibling `code-review` directory is unavailable, check the other available skill locations. If the guides are still unavailable, tell the developer and proceed using the repository's documented standards.

- Apply the relevant practices when choosing file layout, class responsibilities, and method boundaries. Explain which practices drive consequential design choices. Follow agreed project standards and discuss any consequential conflict with the scaffold or a proposed departure with the developer.
- Give the repo-relative path for each relevant file. Explain which files you would create, which scaffold files you would fill in, and which existing files you would modify or reuse.
- Name the classes or other relevant code elements in each file and explain their responsibilities. Name the methods or functions you would add, change, or call, identify where each belongs, and explain what it does. Walk through how the entry point and those methods work together to implement the agreed behavior.
- Follow the structure the developer provided. Explain any proposed additions or departures from the scaffold and agree on them with the developer. Continue to keep code, tests, and configuration read-only during this discussion.
- Review the proposed design with the developer and settle open code design decisions before handing off. If the design exposes an unresolved behavior or scope decision, settle it first, then return to the code design. Record any blocker that prevents agreement as open.

## Hand off the agreed decisions

Summarize the agreed scope, clarified acceptance criteria, code design with file paths and method responsibilities, decisions and rationale, suggested verification, and any remaining blockers. Include the coding practices that shaped the design and any agreed departures. Check links in changed Markdown. Pass the existing story folder path if there is one. To Spec can use the handoff to write `docs/stories/<spec-name>/spec.md`, and To Tasks can write the breakdown under `tasks/` in the same folder.
