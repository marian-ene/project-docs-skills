# Documentation during requirements clarification

Keep durable project documentation in `docs/brain/`. Update the page that owns a durable clarification and use meaningful relative links to related notes and source files.

- Put confirmed domain language in the glossary.
- Put verified behavior and important code paths on the relevant architecture or flow page.
- Record a consequential design decision and its rationale in an ADR if the repo uses them. Mark agreed future work as planned.
- Record a confirmed team convention that requires judgment in the project's coding standards. Link to an existing automated check where one enforces the rule.

Use the story handoff for acceptance criteria, options still being discussed, and decisions that only matter to the current change. If the developer requests a handoff file, use the existing story folder or derive `docs/stories/<spec-name>/` from the agreed change name in kebab-case. Reuse that folder for the spec and tasks. Save requested Draw.io files in `docs/diagrams/` and link to them from the relevant pages. Check incoming pointers when replacing or merging material and preserve any rationale future readers need.
