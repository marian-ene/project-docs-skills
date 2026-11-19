# Project Docs Skills

Portable agent skills and instructions for building and maintaining developer documentation as you work. Install the same skills in any code repository. Each repository grows its own documentation from its code, tests, and decisions confirmed by its developers.

## Available skills

- [Project KT](skills/project-kt/SKILL.md) explores an existing codebase and builds or refreshes its linked documentation. Run it to learn the architecture and business flows, or rerun it after team changes to compare the docs with current behavior. It asks for confirmation before treating a significant change as an accepted rule or decision.
- [Story Walkthrough](skills/story-walkthrough/SKILL.md) works through one upcoming story with a developer. It uses the relevant docs, code, and tests to clarify scope and acceptance criteria, writes durable findings into the relevant pages, and leaves a handoff for later implementation.

Both skills can update documentation. They read application code and configuration to verify their findings.

## Install in any repository

1. Clone or download this repository.
2. Copy the complete `skills/project-kt` and `skills/story-walkthrough` directories into `.agents/skills/` at the root of the repository where you want to use them.
3. Open a new agent session from that repository root. In Codex, invoke `$project-kt` or `$story-walkthrough`. In GitHub Copilot CLI, use `/project-kt` or `/story-walkthrough`. An existing Copilot CLI session can reload skills with `/skills reload`.

See the [Codex installation docs](https://developers.openai.com/api/reference/cli) and [GitHub Copilot CLI skill docs](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills).

## Use the skills

### Build an initial map

> `$project-kt` Map the main components and trace one business flow from its entry point. Verify your findings in code and tests, document what you can establish, and ask me where intent is unclear.

### Refresh the docs after changes

> `$project-kt` Compare the relevant docs with the current code. Use the last reviewed revision if it is available. Show me material differences and confirm intended behavior before updating the docs.

### Walk through a story

> `$story-walkthrough` Review the story, constraints, and acceptance criteria below. Use the existing docs and code to resolve what you can. Ask me about the remaining decisions and update the project docs as we settle them.

## How the documentation grows

The skills follow the target repository's documentation conventions. A repository can start with a short index and a single flow page, then add glossary terms, architecture decisions, and coding standards when there is enough evidence to record them. Relative links connect related pages to each other and to supporting code and tests. Later sessions start from the relevant pages and refresh them as the project evolves.

This release focuses on testing Project KT and Story Walkthrough. Future implementation skills can use the same linked documentation to find project conventions, business rules, and the parts of the code affected by a change.
