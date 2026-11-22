---
name: to-spec
description: Turn agreed requirements, a Grill Reqs handoff, or a decision record into a repository-local specification for one change. Use when the developer wants to capture the scope, acceptance criteria, decisions, and verification before splitting or implementing the work.
license: MIT
---

# To Spec

Synthesize the decisions already made into a spec another developer or agent can use in a fresh session. Keep application code and configuration read-only.

## Gather the decisions

- Use the supplied requirements, conversation, Grill Reqs handoff, or linked artifact. Read the relevant project docs, glossary, ADRs, code, and tests to verify the current behavior and constraints.
- Preserve the project's business terms and the developer's confirmed choices. Keep current behavior, intended behavior, and proposed options distinct. Capture unresolved decisions as open questions and say which work they block. If essential source material is unavailable, ask for that input and label any partial spec as a draft.
- Reuse an existing verification point where it can demonstrate the outcome, such as an API contract, service boundary, or user flow. Cite the evidence and mark new verification ideas as proposed.

## Write the spec

Use the project's established location or the path the developer supplies. Otherwise use `docs/specs/<change>/spec.md`. Update the existing spec when rerunning against the same change.

Write for a developer or model that has the repository and this document, with no access to the conversation. Replace conversational references such as "as discussed" with the actual decision and its source.

- Give the spec a name, a short description of the change, and a one-sentence `why` that states why the change matters. Base it on the agreed problem, outcome, or risk. Link to the relevant project page or ADR when it records the rationale. Follow the target repo's metadata conventions. By default, use the spec title as its name and put `description` and `why` in YAML frontmatter.
- State the problem, desired outcome, scope, exclusions, and behavior that must be preserved. Identify the affected components, code entry points, and related project decisions with repository links.
- Describe the required behavior in concrete terms. Where relevant, specify actors, triggers, preconditions, inputs, outputs, permissions, state transitions, failure handling, and edge cases. For contract, schema, or rollout changes, identify affected consumers and compatibility requirements.
- Give each acceptance criterion a stable ID such as `AC-01`. Describe the setup or input, action, and expected observable result. Link existing tests and name verified test commands or manual verification steps when available.
- Mark confirmed decisions, proposals, and open questions explicitly. Where a decision is missing, state exactly what needs confirmation and which criteria or areas it blocks. Leave affected work marked as blocked. State any decisions the developer explicitly delegated to the implementer.

Before handing off, read the spec as if you had just opened the repository. Resolve vague references and check that each required behavior has a verification path. A reader should be able to tell what to build, how to check it, and when to stop for a decision.

Report the spec path and any questions that still block planning. Keep the spec local unless the developer explicitly requests publication to a named destination. Honor a read-only request by drafting in the conversation.
