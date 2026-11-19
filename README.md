# Project Docs Skills

Portable agent skills for learning a codebase and turning a story into an implementation-ready plan.

- [Project KT](skills/project-kt/SKILL.md) studies the repository, builds a map of its architecture and business flows, and maintains the linked documentation as it learns.
- [Story Walkthrough](skills/story-walkthrough/SKILL.md) uses that documentation and the code to work through one story with the developer. It clarifies acceptance criteria and records settled decisions as they emerge.

Both skills use the target repository's documentation conventions and keep application code read-only.

## Install in a project

Copy both folders under `skills/` into `.agents/skills/` at the target repository root. This layout is supported by [Codex](https://developers.openai.com/api/reference/cli) and [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills).

For a local checkout alongside Bullish Beans, run this in PowerShell:

~~~powershell
$source = 'C:\AzDo\project-docs-skills\skills'
$destination = 'C:\AzDo\bb-monorepo\.agents\skills'
New-Item -ItemType Directory -Path $destination -Force | Out-Null
Copy-Item -LiteralPath (Join-Path $source 'project-kt'), (Join-Path $source 'story-walkthrough') -Destination $destination -Recurse -Force
~~~

Open a new agent session from the target repo root. In Codex, invoke `$project-kt` or `$story-walkthrough`. In Copilot CLI, include `/project-kt` or `/story-walkthrough` in your prompt. To refresh Copilot CLI in an existing session, use `/skills reload`.

## Try the workflow in Bullish Beans

Start by building context for one part of the monorepo:

> $project-kt Fă o hartă scurtă a componentelor și urmărește cum împart bb-api și bb-stocks schema SQL. Verifică dovezile și documentează ce ai aflat. Întreabă-mă unde lipsește contextul de business.

### Sync after the team ships changes

Run Project KT again from the updated checkout. Give it the previous reviewed commit, tag, or a list of changes if you have one. Otherwise, it compares the relevant documentation with current code and tests and reports the areas it checked.

> $project-kt Am ultima versiune din Bullish Beans. Compară documentația despre datele de piață cu implementarea curentă. Arată-mi diferențele și dovezile din cod. Întreabă-mă ce reguli de business sau decizii de arhitectură confirmăm înainte să actualizezi paginile.

When a change is a deviation, keep the intended architecture in the docs and report the implementation difference separately.

### Walk through a story

When you have a story, give it to Story Walkthrough:

> $story-walkthrough Parcurge story-ul de mai jos cu mine. Folosește documentația proiectului, verifică în cod ce poți afla și clarifică pe rând deciziile care afectează criteriile de acceptare.
>
> Story: [paste story, constraints, and acceptance criteria here]

The first skill adds useful project knowledge as it discovers it. The second starts from that knowledge, captures durable clarifications in the relevant pages, and leaves a short handoff for a future spec or implementation session.
