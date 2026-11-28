# Project Docs Skills

Portable agent skills and instructions for building and maintaining developer documentation as you work. Install the same skills in any code repository. Each repository grows its own developer knowledge base, covering architecture, code, business vocabulary, user journeys, and project workflows. Code, tests, and confirmed team decisions provide the evidence.

## Open skills

Skills in `skills/open/` keep application code, tests, and configuration read-only. They work in the conversation or write documentation and planning artifacts.

- [Project Mapping](skills/open/project-mapping/SKILL.md) explores an existing codebase and builds or refreshes its linked documentation. Run it to learn the architecture and business flows, or rerun it after team changes to compare the docs with current behavior. It asks for confirmation before treating a significant change as an accepted rule or decision.
- [Grill Reqs](skills/open/grill-reqs/SKILL.md) works through the requirements for one upcoming change with a developer. It uses the relevant docs, code, and tests to clarify scope and acceptance criteria, writes durable findings into the relevant pages, and leaves a handoff for later implementation.
- [To Spec](skills/open/to-spec/SKILL.md) turns agreed requirements into a local spec with acceptance criteria, decisions, and verification.
- [To Tasks](skills/open/to-tasks/SKILL.md) breaks a spec or settled plan into verifiable tasks with explicit dependencies.
- [TDD](skills/open/tdd/SKILL.md) prepares a Red–Green test plan that describes the test boundary, expected failure, and acceptance checks for each behavior.
- [Code Review](skills/open/code-review/SKILL.md) checks a PR, branch diff, or local changes against requirements, repository standards, and regressions, then reports findings in priority order.

## Closed skill

[Implement](skills/closed/implement/SKILL.md) is the only skill that edits application code, tests, and configuration. It builds a spec, task, or task set, executes Red–Green, and resolves actionable findings from its self-review.

The `open` and `closed` folders describe skill behavior. The execution environment controls filesystem permissions.

## Install in any repository

1. Clone or download this repository.
2. Copy each complete skill directory from `skills/open/` or `skills/closed/` directly into `.agents/skills/` at the target repository root. For example, copy `skills/open/tdd/` to `.agents/skills/tdd/`.
3. Open a new agent session from that repository root. In Codex, invoke the skill by name with a `$` prefix, such as `$to-spec`. In GitHub Copilot CLI, use a `/` prefix, such as `/to-spec`. An existing Copilot CLI session can reload skills with `/skills reload`.

Install `implement`, `tdd`, and `code-review` together to use the implementation workflow. TDD and Code Review can also be installed individually.

The `code-review` directory includes the shared Angular 21+ UI and C# guides. Install `code-review` alongside `grill-reqs` to apply the same guides when planning the code design.

See the [Codex installation docs](https://developers.openai.com/api/reference/cli) and [GitHub Copilot CLI skill docs](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills).

## Use the skills

### Start or resume a short mapping session

> `$project-mapping` Map the project.

A bare `$project-mapping` builds the map in short passes. Each round documents what it verifies and asks up to five important questions. After applying your answers and saving where to resume, it asks whether you want another round or want to stop. Choose to continue for another round in the same chat, or resume later. Name a component or flow to focus the review.

> `$project-mapping` Continue from the last mapping session.

### Refresh the docs after changes

> `$project-mapping` Compare the relevant docs with the current code. Use the last reviewed revision if it is available. Show me material differences and confirm intended behavior before updating the docs.

### Clarify requirements

> `$grill-reqs` Review the requirements below and any constraints or acceptance criteria I have included. Use the existing docs and code to resolve what you can. Ask me about the remaining decisions and update the project docs as we settle them.

### Capture a spec and split it into tasks

> `$to-spec` Turn the requirements and the decisions we just agreed on into a spec.

> `$to-tasks` Split the spec at `docs/stories/<spec-name>/spec.md` into verifiable tasks with dependencies.

The spec and its tasks share a story folder in the target repository. Reuse that folder when revising the same story.

### Implement a task or spec

> `$implement` Implement the tasks listed in `docs/stories/<spec-name>/tasks/README.md`.

Pass a single task file to work on that task. Implement uses the TDD plan or guidance, executes Red–Green itself, and calls Code Review on the resulting diff, including uncommitted changes. It handles justified refactoring in response to findings and reruns the affected checks.

> `$tdd` Add a Red–Green test plan to the task's verification section for the reported behavior at the API boundary.

### Pause for a major scope change

If implementation reveals a decision that would materially change the agreed scope, `$implement` stops the whole run, leaves partial edits in place, and records a handoff in the task or spec. You can take that handoff to `$grill-reqs`. If you decide to proceed, use `$to-spec` and `$to-tasks` to update the plan, then invoke `$implement` again with the revised task or task index. A new session can pick up from the same files.

On resume, Implement checks the actual worktree. It verifies and reuses partial work that fits the revised scope. If you undid those edits, it starts from the current code.

### Review a pull request or local changes

> `$code-review` Review PR #123 and give me the findings in priority order.

> `$code-review` Review my staged and unstaged changes against `docs/stories/<spec-name>/spec.md`.

Code Review checks the applicable Angular 21+ UI and C# practices in standalone reviews as well as implementation self-reviews.

## How the documentation grows

```text
docs/
  brain/
    README.md
    flows/
    adr/
  stories/
    <spec-name>/
      spec.md
      tasks/
        README.md
        <task-id>.md
  diagrams/
    <diagram-name>.drawio
```

- `docs/brain/` holds the linked project documentation. Project Mapping builds it from a short index and adds architecture, flows, glossary terms, coding standards, and decisions as evidence warrants. Grill Reqs updates the pages that own durable findings.
- `docs/stories/` holds planning and implementation artifacts for individual changes. To Spec uses the spec title to choose a stable kebab-case folder name. To Tasks writes the task index and task files under `tasks/` in that folder.
- `docs/diagrams/` holds requested Draw.io diagrams, including diagrams linked from a project page, spec, or task.

Create folders as needed. Use relative links between project pages, story artifacts, diagrams, and supporting code and tests. When reorganizing existing docs, update incoming and outgoing links to the moved files.

## How links are maintained

Project Mapping and Grill Reqs share a journal of the Markdown links they see and actually use. The journal groups each link by source and destination. A followed link earns one point per invocation when it helps with the work. The score counts usage over the last 90 days. An older link with no recent use becomes a review candidate only when there is evidence that the area is still being worked on. Link repairs and cleanup depend on evidence from the current docs and code.

Grill Reqs handles this maintenance during regular story work. Project Mapping can review a wider area. Both skills use `docs/brain/link-usage.json` by default and keep new journals untracked. When creating or migrating this journal, they import valid history from prior journal locations.
