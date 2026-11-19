---
name: project-kt
description: Map a repository and build or refresh its linked developer documentation. Use for project discovery, architecture and business-flow mapping, or documentation sync after team changes. Proactively interview the developer to resolve gaps in intent.
license: MIT
---

# Project KT

Learn enough about the repository to give a developer or another agent a verified route into the code. Keep application code and configuration read-only. Write in the repository's documentation locations and honor a read-only request across the whole repo.

## Choose the scope

A bare invocation or a broad request to map, investigate, or understand the project starts a repository-wide discovery. Begin from the repository root and cover every major component, including shared modules and external integrations that affect the architecture. A named component or flow narrows the scope. A request to reconcile recent changes uses the sync workflow below.

## Discover and map the project

1. Read the applicable repository instructions and locate the existing docs entry point. Use it to guide discovery. Survey the components and entry points in scope, how they fit together, and the data, contracts, or dependencies they share.
2. Identify the main business flows and trace representative ones through code, tests, and configuration. Record the trigger, rules, handoffs, and outcome. Link consequential claims to files and name the relevant symbols or test scenarios. In a broad review, give each major component a place in the map and identify which flows have been traced in depth.
3. Build or refresh the linked Markdown documentation as you go. Create or update a short entry point and an architecture map with the verified relationships. Add flow pages, glossary entries, coding standards, and decisions as the evidence and discussion warrant. Keep visible which findings describe observed behavior, which reflect confirmed intent, and which questions remain open.

## Interview the developer as you go

Initiate the interview yourself. Investigate facts you can verify from repository evidence first. Once you have evidence, ask focused questions about unresolved business rules, vocabulary, ownership, architecture rationale, or behavior that may conflict with the intended design. Show what you found and explain what the answer would change. Offer an interpretation or recommendation when the evidence supports one.

Ask the questions that can be answered now together. Use each answer to update the relevant page and ask any follow-ups it unlocks. Continue independent discovery while questions are open. Keep going until the material questions in scope are resolved or the developer defers them. If you need an answer to establish intent, ask it during the walkthrough and leave the point open in the meantime.

## Confirm important findings

During an initial map as well as later reviews, bring newly discovered or materially changed architectural choices, business rules, and coding conventions to the developer for confirmation. Do this even when their current behavior is clear in code. Group related findings and show how the approach works today, the evidence for it, and why it matters. Ask whether to keep it as an intended direction, revisit it later, or leave the decision open.

Record the verified current behavior where it helps readers understand the code. Record it as an agreed direction only after confirmation. If the developer wants to revisit it, add a follow-up to the repo's existing documentation or to a short follow-up section in the owning page. Capture what should be revisited, why, and a link to the evidence. Mark undecided findings as open and leave implementation for a separate task.

## Sync after team changes

Use this workflow when rerunning KT on a newer checkout or when the developer names changes that may have made the docs stale.

1. Identify the checked-out revision and the review scope. Compare it with a Git ref supplied by the developer or a documented last-reviewed commit for that scope, if available and valid. Use the diff to locate changes in behavior, contracts, ownership, architecture, and enforcement, including moved or deleted code. If there is no usable baseline, compare the relevant docs and their links with the current code and tests. Recent commits can help prioritize that review. State the range or areas actually reviewed and any coverage limits.
2. Trace consequential differences back to source and tests. For each, show what the docs say, what the current implementation does, and why the difference matters. Ask the developer whether the change is intended, a deviation to fix, or still undecided. Ask even when the docs are silent if the finding would establish a new business rule, architectural decision, or coding standard.
3. Update the owning pages and links for confirmed decisions. Keep rejected or undecided behavior out of accepted architecture, rules, and standards. Report it as a discrepancy with evidence, or record it as a known deviation if requested. Mechanical link and path repairs verified against the repository can be made independently. Leave fixes to application code for a separate task.

If tracking a last-reviewed commit helps repeat this review, record it with the scope in the existing docs index. Advance it for that scope after review only when material findings have been resolved or explicitly tracked as open. An initial comparison against current code establishes coverage only for the areas actually reviewed.

## Build and maintain the documentation

Use the repo's established structure. When there is none, start with a short `docs/README.md` linking to the first useful page. Add pages as evidence and scope warrant:

- An architecture overview and pages under `docs/flows/` for what the system does and where to trace it.
- `GLOSSARY.md` for verified or developer-confirmed domain terms.
- `CODING_STANDARDS.md` for established conventions or confirmed preferences that require judgment. Treat repeated patterns in code as candidates until a documented rule or the developer confirms them. Link to automated checks for existing mechanical rules.
- `docs/adr/` for confirmed consequential decisions and their rationale. Preserve the distinction between an observed design and a decision whose rationale is known.

Update the page that already owns a topic. Use descriptive relative links between related pages and to relevant source files. On repeat runs, recheck the pages touched by the exploration, repair broken links, and consolidate duplicates when the surviving path preserves useful context. Use low relevance as a reason to review a page and evidence of redundancy or supersession to decide what to retire.

Check changed links and report the areas covered, documentation updated, and questions still open. State where a later KT session can continue if the requested scope is broader than the area verified.
