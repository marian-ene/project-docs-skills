---
name: tdd
description: Plan Red–Green verification for a feature, regression, spec, or task. Use to identify test boundaries, scenarios, expected failures, and verification steps for an implementer.
license: MIT
disable-model-invocation: true
---

# Test-Driven Development Planning

Keep application code, test files, and configuration read-only. Read the acceptance criteria or bug report, applicable project instructions, and nearby code and tests. Prepare one Red–Green cycle per observable behavior for the implementer.

## Choose a test boundary

- Use the boundary documented in the spec or task when it can demonstrate the criterion. A boundary is a supported interface where a caller can observe behavior, such as an API, command, service interface, event, or user flow.
- Otherwise, choose the smallest established boundary that can catch the actual regression. Use a broader test where integration is part of the behavior. Clarify consequential changes to public contracts or testing strategy when the project has left the decision open.
- Describe observable assertions grounded in the requirement, a worked example, or a known input and output. Identify the project's test harness and any existing fixtures worth reusing. Prefer real in-process collaborators and suggest substitutes at external or nondeterministic boundaries where they help control the test. Keep assertions independent of private implementation and duplicated production logic.

## Specify Red and Green

1. **Red.** Describe a focused test with its setup, action, expected assertion, and the failure that would demonstrate the missing behavior or regression. Name the focused test command if known.
2. **Green.** Describe the observable result that should pass after the smallest change through the normal entry point. Name any surrounding tests that should be rerun.

For a change without a meaningful failing test, document the applicable validation or direct acceptance check. Label expected results as planned and leave execution evidence to the implementer.

## Hand off the test plan

When invoked by Implement, return the focused plan to the caller. For a standalone request, use the requested documentation path or add it to the relevant spec or task's verification section. When there is no existing spec or task, default to `docs/specs/<change>/test-plan.md`. Honor a no-write request by returning the plan in the conversation.
