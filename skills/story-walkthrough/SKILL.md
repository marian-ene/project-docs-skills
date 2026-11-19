---
name: story-walkthrough
description: Clarify one upcoming story or use case with the developer using existing project docs, code, and tests. Use when given a story, requirements, or acceptance criteria to discuss implementation and capture settled decisions before planning or coding.
license: MIT
---

# Story Walkthrough

Work through one story with the developer until its behavior, boundaries, and key implementation decisions are clear. Use the repository's durable documentation as working context. Keep application code and configuration read-only during the walkthrough.

## Ground the story

- Read the story, acceptance criteria, and constraints supplied by the developer. Identify the affected flow and the outcome the story is meant to achieve.
- Follow the applicable repo instructions and start from its docs entry point. Open the relevant flow pages, glossary entries, coding standards, or ADRs. Follow their links into code and tests to verify current behavior and constraints. Use focused code search to fill gaps where the docs are sparse.
- Surface discrepancies that affect the story, with links to the evidence. Keep current behavior, requested behavior, and open decisions distinct.

## Clarify decisions with the developer

- Check the repo for answerable facts first. Ask questions in dependency order about behavior, edge cases, scope, or trade-offs that affect the story or how acceptance will be verified. Give your recommended answer and the evidence or trade-off behind it. Group independent questions when that helps the discussion.
- As decisions settle, update the owning Markdown page if the result is useful beyond this story. Capture confirmed vocabulary, existing behavior verified in code, and durable rationale or constraints. Use [documentation guidance](references/documentation.md) when choosing where to record a new note.
- Keep proposed behavior in the story notes or mark it explicitly as an agreed future design. Document it as current behavior once verified in the implementation. Honor requests for a read-only discussion.

When the story is clear enough to hand off, summarize the agreed scope, clarified acceptance criteria, decisions and rationale, suggested verification, and any remaining blockers. Check links in changed Markdown. The handoff can feed a later spec or ticketing step.
