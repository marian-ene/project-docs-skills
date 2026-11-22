---
name: to-tasks
description: Split agreed requirements, a spec, or an implementation plan into independently verifiable repository-local tasks. Use when the developer wants small delivery slices with acceptance criteria, dependencies, and a clear order of work.
license: MIT
---

# To Tasks

Turn one agreed change into a task plan that a fresh implementation session can pick up. Keep application code and configuration read-only.

## Shape the work

- Start from the supplied spec, plan, or settled conversation. Follow the relevant project docs and ADRs and inspect code or tests where they inform scope, sequencing, or verification. Carry forward unresolved decisions and identify which tasks they block.
- Prefer small, independently verifiable delivery slices. For a feature, each slice should deliver one observable behavior across the layers it needs. Keep small changes together when splitting them adds handoffs without creating useful milestones.
- For a broad migration or refactor, use compatibility steps when they let each task land safely. For example, add a compatible interface, migrate consumers in verifiable batches, and remove the old interface once its consumers are migrated. Give each step a clear outcome and verification.
- Give each task a stable ID, outcome, scope, acceptance checks, and links to source decisions and spec criteria where available. Record only real prerequisites under `Blocked by`. Verify every referenced task ID exists, the dependency graph has no cycles, and every in-scope criterion is covered by a task or explicitly deferred.

## Make each task usable in a fresh session

Treat each task file as the implementer's entry point. Include the concrete outcome, scope boundaries, expected behavior, and requirements from the spec that apply to this task. Link directly to the relevant spec criteria, project docs, and code or tests. Name verified components, symbols, or test locations that help the implementer start.

Give each task a name and a short description of its outcome. Link to the source spec when one exists so the implementer can find the change's `why`. Add a one-sentence `why` to a task only when it explains a task-specific constraint, dependency, or trade-off that affects implementation. Ground it in the agreed requirements or verified evidence.

Write checks with the relevant setup or input, action, and expected result. Name existing test commands or reproducible manual steps when available. State behavior that must be preserved and prerequisite changes or decisions that matter. If work depends on an unresolved decision, mark the task blocked and name the exact decision needed. An implementer should be able to pick up the file with the repository open and use its links without reading the planning conversation.

## Save and hand off the breakdown

Use the project's task conventions or a path the developer supplied. By default, create `tasks/` beside a spec in its own change directory. For a flat spec or a conversation without a file, use `docs/specs/<change>/tasks/`. Write one Markdown file per task and a short `tasks/README.md` linking the source and tasks in dependency order. When revising an existing breakdown, preserve stable IDs and recorded progress.

Give the task index a name, a short description, and a one-sentence `why` that explains when to consult the breakdown and what it helps coordinate. Follow the target repo's metadata conventions for the index and task files. By default, use page titles as names and put `description` and any `why` in YAML frontmatter.

Show the developer the proposed breakdown, the work that can start, and the decisions or dependencies that still block work. Invite feedback on scope and sequencing. Keep artifacts local unless the developer explicitly requests publication to a named tracker. Honor a read-only request by presenting the breakdown in the conversation.
