---
name: implement
description: Implement a repository-local spec, one task or issue, or a set of tasks using Red–Green TDD and a closing self-review. Use when the developer wants to build work defined by a spec, ticket, or To Tasks breakdown.
license: MIT
disable-model-invocation: true
---

# Implement

This is the closed skill. It owns edits to application code, tests, and configuration that are required by the requested scope.

## Establish scope

1. Resolve the supplied task, spec, task index, or issue reference. Look in `docs/stories/` for a named story. For an issue, use the repository's tracker workflow to read it and identify it by title. For a spec, read `tasks/README.md` in the same story folder if available. For a task, follow its links to the spec, acceptance criteria, and prerequisites. A single task scopes the work to that task. A spec or task index scopes it to the applicable task set.
2. Read the applicable repository instructions, linked architecture decisions and coding standards in `docs/brain/`, existing code, and tests. Capture the requested behavior, constraints, preserved behavior, and planned verification. Reuse the existing verification boundaries named by the spec or task. When choosing a routine boundary, use a supported entry point and the project's established tests.
3. Record the starting revision and inspect the staged and unstaged diffs and relevant untracked files before editing. For any affected files with pre-existing edits, retain enough of their initial contents to identify your own changes in review. Preserve unrelated work. Work through ready tasks in dependency order. Treat a recorded prerequisite as satisfied when its required behavior is present and verified. Carry forward open decisions that block work, and continue independent tasks when possible.

## Check for a required database scaffold

Before editing a task that depends on database objects or persisted data, inspect the relevant schema, constraints, and dependencies through an available SQL MCP connection. Identify the environment and keep the inspection read-only. Compare the relevant database definitions with the checked-out models, mappings, migrations, and SQL. Repeat the check if you encounter another relevant database dependency during implementation. If MCP or the required metadata is unavailable, use repository evidence and report what remains unverified.

If the task needs schema already present in the intended database and the repository's database-first models or mappings need to be regenerated to match it, stop the entire implementation run as soon as you confirm the mismatch. Leave any partial edits in place. Record the database, affected objects and generated files, and the differences that require scaffolding. Give the developer the repository's scaffold instructions if verified, and ask them to run the scaffold before invoking Implement again. Leave scaffold execution to the developer. Pending migrations that introduce schema still to be deployed belong in the database script workflow.

## Stop for a major scope change

If discovery, implementation, or review shows that delivering the agreed outcome would require a material change to product behavior, a public contract, data handling, rollout, or agreed exclusions, stop the entire implementation run before making further code, test, or configuration edits. Leave the worktree as it is, including any incomplete changes. A larger diff or a routine technical choice within the agreed scope can proceed.

## Record a pause

Record the pause in the active task or in the spec if there is no task file. If neither exists locally, use `docs/stories/<spec-name>/implementation-handoff.md` and reuse the story folder if it already exists. If there is no spec title, derive the folder name from the change name in kebab-case. Use the project's status convention or **Paused pending scaffold** or **Paused pending scope decision**, as applicable. Include:

- The spec, task, and acceptance criterion IDs or links, plus the exact prerequisite or decision needed.
- The discrepancy found in the database, code, tests, or review, with evidence and the effect on the task. For a scope decision, note the options and their consequences where known, including deferring or dropping the change.
- The branch or worktree and starting revision if available, known partial edits and affected files, checks run and their results, and remaining work. Mark incomplete work explicitly.

Return the handoff path and a concise summary to the developer, then end the implementation run. For a scope decision, the developer can take the handoff to `$grill-reqs`. For a scaffold pause, the developer can run the scaffold and invoke Implement again with the same task or task index. Ordinary task blockers can still leave independent tasks ready to run.

## Resume a paused implementation

When asked to resume a paused implementation, read the current spec, tasks, and any handoff they contain or link to before editing. After a scaffold pause, compare the current generated files with the schema evidence for the recorded objects. Refresh that evidence through MCP when available. If you cannot verify that the required mappings now match, return the handoff and end the run. For a scope pause, return the handoff and end the run if the decision is still pending. If the revised plan defers or drops the requested task, report that disposition and end the run.

Inspect the actual code and staged, unstaged, and relevant untracked changes. If partial work is present, check it against the current acceptance criteria and generated mappings, reuse applicable changes, and adapt them as needed while preserving the scaffold output and unrelated edits. If the developer undid the partial work or the checkout has none, implement the task from the current code. Treat recorded progress and prior test results as historical evidence and verify the current checkout. Include retained partial edits from the same task in the final review.

## Check for Angular 21+ UI work

Before editing UI code, check whether the affected UI uses Angular and determine its major version from `@angular/core` in the relevant package manifest and lockfile, when available. Check the package that owns the UI, not an unrelated package in the same workspace. If the affected UI uses Angular 21 or later, load [Angular 21+ UI practices](../../open/code-review/references/angular-ui-practices.md) and apply them to the changed code. In a flat installation, load `../code-review/references/angular-ui-practices.md` instead. Skip this guide for non-UI work, other frameworks, and older Angular versions. If the version cannot be confirmed from repository evidence, do not assume the guide applies.

## Check for C# work

Before editing affected C# code, load [C# implementation practices](../../open/code-review/references/csharp-practices.md). In a flat installation, load `../code-review/references/csharp-practices.md` instead. Check the owning project's configuration before using version-specific syntax or APIs. Apply the general C# practices to changed code and the architecture and integration practices only to the backend patterns and technologies in scope. For mixed Angular and C# work, load both guides when applicable.

## Build and verify

1. Before editing behavior, load the [TDD planning skill](../../open/tdd/SKILL.md). In a flat installation, load `../tdd/SKILL.md` instead. Look for a test plan in the task or spec's verification section, a linked file, or `test-plan.md` beside the spec. Use the plan or the TDD planning guidance to identify the next observable behavior and its verification boundary.
2. **Red.** Add or extend one focused test and run it before changing production behavior. Confirm that the failure demonstrates the missing behavior or regression. Diagnose setup failures and unrelated failures. If the test already passes, check whether the behavior already exists or the test misses the criterion.
3. **Green.** Make the smallest production change that satisfies the criterion through the normal entry point. Rerun the same test and the affected surrounding tests. Repeat for the next behavior. Where a meaningful failing test is unavailable, run the applicable validation or direct acceptance check.
4. After each task, verify its acceptance checks and run the relevant project checks. After the task set, run the repository's relevant broader checks to catch interactions. Record commands and outcomes, including the observed Red and Green, verification substitutes, environmental blockers, and pre-existing failures that affect confidence.

## Prepare database changes

Follow the project's migration and deployment conventions. Prepare the final runnable SQL scripts where the project keeps database changes. If the project generates deployment SQL from migrations, use its generator and identify the migration range. Include schema changes and any required backfill or data changes. Check ordering, compatibility with the deployed application, and what happens if execution fails partway or needs to be retried. Include the scripts and their planned order in the self-review. Where feasible, verify them on an authorized disposable database and record the outcome.

## Review and resolve findings

1. Load the [Code Review skill](../../open/code-review/SKILL.md) and run it as a self-review. In a flat installation, load `../code-review/SKILL.md` instead. Provide the implementation scope and starting revision, the final diff including staged, unstaged, and relevant new files, the spec and task IDs, and the verification results. Identify pre-existing edits so the review can focus on the implementation and its interactions. Include each applicable language or framework guide in the review criteria for the affected changes.
2. Verify each finding against the actual diff and its evidence. Fix confirmed in-scope defects, unmet criteria, and applicable standards violations in priority order. For a behavior correction, use Red–Green when possible. For a justified behavior-preserving refactor, establish green, make the smallest relevant change, and rerun the affected tests. Treat heuristic suggestions as optional and apply them when they address a concrete problem within scope.
3. Recheck the fixes and affected code paths against the findings, then rerun the relevant verification. Repeat when a fix introduces a new actionable issue. Finish when the in-scope findings are resolved or a concrete blocker prevents further changes. Report outstanding findings with their impact.

## Hand off database scripts

After implementation and review, give the developer the final runnable script or links to all final scripts in numbered execution order. For each step, state the target database or schema, prerequisites, whether it runs before or after application deployment or another step, and how to verify success before continuing. If a script applies only to a particular environment or starting migration state, state when to use it. Report which scripts were tested and which conditions remain unverified. Leave execution against the target database to the developer unless they separately authorize it.

Summarize completed tasks and acceptance checks, Red–Green evidence or its verification substitute, final checks, and remaining blockers. Update task progress where the project already tracks it locally. Create commits, push, open or update a PR, or change tracker state only with the developer's authorization.
