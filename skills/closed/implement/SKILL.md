---
name: implement
description: Implement a repository-local spec, one task or issue, or a set of tasks using Red–Green TDD and a closing self-review. Use when the developer wants to build work defined by a spec, ticket, or To Tasks breakdown.
license: MIT
disable-model-invocation: true
---

# Implement

This is the closed skill. It owns edits to application code, tests, and configuration that are required by the requested scope.

## Establish scope

1. Resolve the supplied task, spec, task index, or issue reference. For an issue, use the repository's tracker workflow to read it and identify it by title. For a spec, read its task index if available. For a task, follow its links to the spec, acceptance criteria, and prerequisites. A single task scopes the work to that task. A spec or task index scopes it to the applicable task set.
2. Read the applicable repository instructions, linked architecture decisions, coding standards, existing code, and tests. Capture the requested behavior, constraints, preserved behavior, and planned verification. Reuse the existing verification boundaries named by the spec or task. When choosing a routine boundary, use a supported entry point and the project's established tests.
3. Record the starting revision and inspect the staged and unstaged diffs and relevant untracked files before editing. For any affected files with pre-existing edits, retain enough of their initial contents to identify your own changes in review. Preserve unrelated work. Work through ready tasks in dependency order. Treat a recorded prerequisite as satisfied when its required behavior is present and verified. Carry forward open decisions that block work, and continue independent tasks when possible.

## Stop for a major scope change

If discovery, implementation, or review shows that delivering the agreed outcome would require a material change to product behavior, a public contract, data handling, rollout, or agreed exclusions, stop the entire implementation run before making further code, test, or configuration edits. Leave the worktree as it is, including any incomplete changes. A larger diff or a routine technical choice within the agreed scope can proceed.

Record the pause in the active task or in the spec if there is no task file. If neither exists locally, use the project's handoff location or `docs/specs/<change>/implementation-handoff.md`. Use the project's status convention or **Paused pending scope decision**. Include:

- The spec, task, and acceptance criterion IDs or links, and the exact decision needed.
- The discrepancy found in code, tests, or review, with evidence and the effect on scope. Note the options and their consequences where known, including deferring or dropping the change.
- The branch or worktree and starting revision if available, known partial edits and affected files, checks run and their results, and remaining work. Mark incomplete work explicitly.

Return the handoff path and a concise summary to the developer. End the implementation run so the developer can choose whether to take the handoff to `$grill-reqs`. Ordinary task blockers can still leave independent tasks ready to run.

## Resume after clarification

When asked to resume a paused implementation, read the updated spec, tasks, and any handoff they contain or link to before editing. If the scope decision is still pending, return the handoff and end the run. If the revised plan defers or drops the requested task, report that disposition and end the run.

Inspect the actual code and staged, unstaged, and relevant untracked changes. If partial work is present, check it against the revised acceptance criteria, reuse applicable changes, and rework what the new scope requires while preserving unrelated edits. If the developer undid the partial work or the checkout has none, implement the revised task from the current code. Treat recorded progress and prior test results as historical evidence and verify the current checkout. Include retained partial edits from the same task in the final review.

## Build and verify

1. Before editing behavior, load the [TDD planning skill](../../open/tdd/SKILL.md). In a flat installation, load `../tdd/SKILL.md` instead. Look for a test plan in the task or spec's verification section, a linked file, or `test-plan.md` beside the spec. Use the plan or the TDD planning guidance to identify the next observable behavior and its verification boundary.
2. **Red.** Add or extend one focused test and run it before changing production behavior. Confirm that the failure demonstrates the missing behavior or regression. Diagnose setup failures and unrelated failures. If the test already passes, check whether the behavior already exists or the test misses the criterion.
3. **Green.** Make the smallest production change that satisfies the criterion through the normal entry point. Rerun the same test and the affected surrounding tests. Repeat for the next behavior. Where a meaningful failing test is unavailable, run the applicable validation or direct acceptance check.
4. After each task, verify its acceptance checks and run the relevant project checks. After the task set, run the repository's relevant broader checks to catch interactions. Record commands and outcomes, including the observed Red and Green, verification substitutes, environmental blockers, and pre-existing failures that affect confidence.

## Review and resolve findings

1. Load the [Code Review skill](../../open/code-review/SKILL.md) and run it as a self-review. In a flat installation, load `../code-review/SKILL.md` instead. Provide the implementation scope and starting revision, the final diff including staged, unstaged, and relevant new files, the spec and task IDs, and the verification results. Identify pre-existing edits so the review can focus on the implementation and its interactions.
2. Verify each finding against the actual diff and its evidence. Fix confirmed in-scope defects, unmet criteria, and applicable standards violations in priority order. For a behavior correction, use Red–Green when possible. For a justified behavior-preserving refactor, establish green, make the smallest relevant change, and rerun the affected tests. Treat heuristic suggestions as optional and apply them when they address a concrete problem within scope.
3. Recheck the fixes and affected code paths against the findings, then rerun the relevant verification. Repeat when a fix introduces a new actionable issue. Finish when the in-scope findings are resolved or a concrete blocker prevents further changes. Report outstanding findings with their impact.

Summarize completed tasks and acceptance checks, Red–Green evidence or its verification substitute, final checks, and remaining blockers. Update task progress where the project already tracks it locally. Create commits, push, open or update a PR, or change tracker state only with the developer's authorization.
