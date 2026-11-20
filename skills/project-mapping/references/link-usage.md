# Documentation link usage

Both skills use this format. It works with either skill installed by itself.

## Choose the journal

Check the active workspace instructions for an explicitly configured documentation link-usage journal. When defined, use that location alone and preserve its existing format and history. Resolve relative paths from the workspace that owns the configuration, even when reviewing a component below it. Verify the resolved destination is in that workspace and outside any sibling or separate child checkout. If the override is unreadable, unwritable, invalid, or outside that boundary, report the limitation and continue link maintenance without writing a journal elsewhere.

When no override is configured, resolve the local state directory from the target repository root with
`git rev-parse --path-format=absolute --git-path project-docs-usage/v1`.
This keeps the journal in Git's local metadata for the current worktree. Create the directory on the first write. If Git cannot resolve the path or the directory is unavailable for writing, still verify and maintain links within scope. Honor read-only requests by keeping observations in the conversation.

## Record one entry per invocation

Read the selected journal at the start of the invocation. Use a fresh UUID and an original UTC timestamp for a new invocation. Reuse both across pauses, resumes, retries, and mapping rounds within that invocation. Save actual observations before yielding or handing off. A later, independent invocation gets a new ID.

- In a configured version 1 JSON journal, preserve its existing container and fields. Add or update one entry by `id` (UUID), with `startedAt`, `seen`, and `used`. Reread before saving and merge observations without replacing other invocations. For a new configured JSON journal with no prescribed structure, use an object with `version: 1` and an `entries` array.
- In the default Git journal, use one JSON file named by UUID per invocation. Keep the following record format.

~~~json
{
  "startedAt": "2026-01-15T09:00:00Z",
  "seen": [["docs/flows/portfolio.md", "GLOSSARY.md"]],
  "used": [["docs/flows/portfolio.md", "GLOSSARY.md"]]
}
~~~

An edge is directional. Normalize both paths relative to the journal-owning workspace root (the target repository root for the default journal), use forward slashes, retain the file's actual casing, and keep an explicit destination anchor as part of its identity. Track current local links between Markdown files, including anchored links to other pages. Put an edge in `seen` when it appears on a page you actually review. Add it to `used` only when you follow it to another page and rely on that page for the work. Each list contains unique edges and every used edge is also seen. Opening two pages independently gives no usage credit to their link. Record only observed or followed links from this invocation. Write UTF-8 and replace files atomically where supported. Store only invocation IDs, timestamps, and relative link paths in new observations.

## Review active links

For links in scope, read valid journal entries and count distinct invocation IDs that record the edge as used in the last 90 days. Use the entry ID in a configured journal or the filename UUID in the default journal. Each contributes one point. Older uses fall outside the window. Derive the score from the journal each time. Leave stored scores and Draw.io diagrams untouched during journal maintenance. Treat a score of zero as a review candidate when the edge was first seen at least 90 days ago and another invocation saw it within the last 90 days. Exclude the current invocation from this activity check. Links with no usable history, newly observed links, and areas without recent recorded activity have insufficient evidence.

Review link validity and meaning independently of score. Repair a broken or moved target when the replacement is verified. If code or documentation changes make the relationship obsolete, update the link when the correct relationship is clear or raise the discrepancy for confirmation. Use low usage to prioritize review. Keep links that serve a documented purpose, including rare procedures or decisions. Remove or merge a link only when evidence shows it is obsolete or redundant, or the developer confirms the change. For an unresolved candidate, report the source, destination, and reason for review.

Grill Reqs checks the relevant outgoing links on pages it reviews. Project Mapping can do the same for a broader documentation scope when asked. Existing documentation remains the source of truth about each relationship.
