---
name: project-kt
description: Study an existing codebase and build or refresh its linked developer documentation. Use for initial architecture and business-flow discovery, or to sync glossary, coding standards, and project docs after team changes.
license: MIT
---

# Project KT

Learn enough about the repository to give a developer or another agent a verified route into the code. Keep application code and configuration read-only. Write in the repository's documentation locations and honor a read-only request across the whole repo.

## Discover

1. Read the applicable repository instructions and find the docs entry point. Use existing maps, glossaries, and ADRs to identify what is known and what needs checking. When starting from scratch, survey the top-level components, entry points, and component boundaries before choosing one meaningful business flow to trace in depth.
2. Follow the requested area or flow through its implementation, tests, and configuration. Record the trigger, business rules, component handoffs, and outcome. Cite the relevant files and name the symbols or test scenarios supporting consequential claims. Keep observed behavior, confirmed business intent, and unresolved assumptions distinct.
3. Verify what you can in the repo before asking the developer. Ask focused questions when intent, vocabulary, rationale, or an apparent inconsistency cannot be resolved from the evidence. Keep productive discovery moving while those questions remain open. Update the relevant page when an answer settles a point.

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
