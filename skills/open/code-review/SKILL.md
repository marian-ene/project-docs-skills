---
name: code-review
description: Review a pull request, branch diff, or local changes against the intended behavior and repository standards. Use for a standalone peer review or an implementation self-review that returns a single prioritized list of actionable findings.
license: MIT
disable-model-invocation: true
---

# Code Review

Review the proposed change in context with application code, tests, and configuration read-only. Return findings to the caller, or write a review document if requested. Keep PR comments and review state read-only. The implementer owns follow-up edits.

## Establish the diff and sources

- For a PR, use its target branch, head, changed files, and description from the repository's hosting workflow. For a branch comparison, use the specified base and head, or the confirmed target branch and its merge base with the head. Respect an explicit diff range. Resolve the refs and report the scope examined.
- For staged changes, use the index diff. For working changes or a self-review, inspect the net change against the starting revision, check the staged and unstaged diffs for differences between the index and working tree, and read relevant untracked files separately. In a self-review, use the initial worktree state supplied by Implement to account for pre-existing edits. With an unspecified local scope, start with pending worktree changes if present. Check the file list against the patch and read changed files and callers as needed.
- Read the supplied or linked spec, tasks, issues, and acceptance criteria. Use the PR description or other explicit requirements where available. If intent is unavailable, review correctness and standards and report the gap. Read the repository instructions that apply to the changed paths, including documented coding standards, architecture decisions, and test conventions.

## Load applicable coding practices

Use the following guides in both standalone reviews and implementation self-reviews. Load both for mixed changes when applicable.

- **Angular UI:** Check `@angular/core` in the affected UI package's manifest and lockfile, when available. If repository evidence confirms Angular 21 or later, load [Angular 21+ UI practices](references/angular-ui-practices.md). Do not apply this guide to unrelated packages, other frameworks, older Angular versions, or when the version cannot be confirmed.
- **C#:** For changes to C# code, load [C# implementation practices](references/csharp-practices.md). Check the owning project's configuration for version-specific syntax or APIs. Apply architecture and integration rules only to the backend patterns and technologies in scope.

## Inspect and substantiate

- **Spec and behavior.** Trace each relevant criterion through the normal entry point. Check missing behavior, regressions for existing callers, unintended scope, and relevant validation, permissions, failure paths, or compatibility.
- **Standards and architecture.** Check changed code against the applicable guides and repository standards. Cite the specific rule or decision and explain the impact of each violation. Follow agreed team standards where they differ from the guides' defaults. Treat an observed pattern as evidence of a convention, not a basis for overriding a documented rule. Treat maintainability and refactoring suggestions as judgment calls unless a documented rule applies. Tie suggestions to concrete costs, such as duplicated business rules that can diverge.
- **Verification.** Check whether tests cover changed behavior and likely regressions at supported boundaries. Examine assertions and the behavior they would catch. Use available CI and caller-supplied test results. Distinguish those results from conclusions based on inspection and identify any targeted checks the implementer should run.

Report findings caused or exposed by the change. Follow the relevant code path and confirm the triggering condition before assigning impact. Ground every finding in a changed location and a requirement, rule, or demonstrated code path. For omitted behavior, anchor to the nearest changed integration point and cite the requirement. Collapse duplicate symptoms into the root cause and omit speculative concerns and formatting already handled by tooling.

## Report findings

Return one numbered list, highest priority first. Within a priority, order by impact and likelihood. Use these levels:

- **P0** Critical release blocker, such as widespread data loss or a system-wide outage.
- **P1** Must fix before merge due to a material regression, broken contract, or core acceptance criterion that fails.
- **P2** Actionable issue with a narrower impact, including a genuine edge-case defect, a meaningful verification gap, or an applicable standards violation of lower impact.
- **P3** Optional improvement with a concrete benefit.

For each finding, give the priority, short title, file and line, triggering scenario or violated rule, consequence, and a focused direction for the fix. Link the criterion or standard when available. If the review finds no actionable issues, say so. Close with material gaps in scope, available requirements, or verification.
