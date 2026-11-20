# Project Docs Skills

Portable agent skills and instructions for building and maintaining developer documentation as you work. Install the same skills in any code repository. Each repository grows its own developer knowledge base, covering architecture, code, business vocabulary, user journeys, and project workflows. Code, tests, and confirmed team decisions provide the evidence.

## Available skills

- [Project Mapping](skills/project-mapping/SKILL.md) explores an existing codebase and builds or refreshes its linked documentation. Run it to learn the architecture and business flows, or rerun it after team changes to compare the docs with current behavior. It asks for confirmation before treating a significant change as an accepted rule or decision.
- [Grill Reqs](skills/grill-reqs/SKILL.md) works through the requirements for one upcoming change with a developer. It uses the relevant docs, code, and tests to clarify scope and acceptance criteria, writes durable findings into the relevant pages, and leaves a handoff for later implementation.

- [To Spec](skills/to-spec/SKILL.md) turns agreed requirements into a local spec with acceptance criteria, decisions, and verification.
- [To Tasks](skills/to-tasks/SKILL.md) breaks a spec or settled plan into verifiable tasks with explicit dependencies.

The skills write documentation and planning artifacts. They read application code and configuration to verify their findings.

## Install in any repository

1. Clone or download this repository.
2. Copy the complete directories for the skills you want from `skills/` into `.agents/skills/` at the root of the repository where you want to use them.
3. Open a new agent session from that repository root. In Codex, invoke the skill by name with a `$` prefix, such as `$to-spec`. In GitHub Copilot CLI, use a `/` prefix, such as `/to-spec`. An existing Copilot CLI session can reload skills with `/skills reload`.

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

> `$to-tasks` Split the spec at `docs/specs/<change>/spec.md` into verifiable tasks with dependencies.

By default, the spec and task files live in the target repository. Follow the project's existing conventions where available.

## How the documentation grows

The skills follow the target repository's documentation conventions. A repository can start with a short index and a single flow page, then add glossary terms, architecture decisions, and coding standards when there is enough evidence to record them. Relative links connect related pages to each other and to supporting code and tests. Later sessions start from the relevant pages and refresh them as the project evolves.

## How links are maintained

Both skills keep a local per-worktree journal of the Markdown links they see and actually use. A followed link earns one point per invocation when it helps with the work. The score counts usage over the last 90 days. An older link with no recent use becomes a review candidate only when there is evidence that the area is still being worked on. Link repairs and cleanup depend on evidence from the current docs and code.

Grill Reqs handles this maintenance during regular story work. Project Mapping can review a wider area. The journal lives in local Git metadata, while Markdown changes can be committed with the rest of the project documentation.

Future implementation skills can use the same linked documentation and task files to find project conventions, business rules, and affected code.
