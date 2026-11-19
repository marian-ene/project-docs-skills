# Documentation link usage

Both skills use this format. It works with either skill installed by itself.

## Record one entry per invocation

Resolve the local state directory from the target repository root with
`git rev-parse --path-format=absolute --git-path project-docs-usage/v1`.
This keeps the journal in Git's local metadata for the current worktree. Create the directory on the first write. If Git cannot resolve the path or the directory is unavailable for writing, still verify and maintain links within scope. Honor read-only requests by keeping observations in the conversation.

Use one JSON file named with a fresh UUID per invocation. Keep its original UTC timestamp and reuse the same file across pauses, retries, and KT rounds within that invocation. Save before yielding or handing off. Merge new observations into that file so rereading an edge counts once. A later invocation gets its own file. Write using UTF-8 and replace the file atomically where supported. Store timestamps and repository-relative paths only.

~~~json
{
  "startedAt": "2026-01-15T09:00:00Z",
  "seen": [["docs/flows/portfolio.md", "GLOSSARY.md"]],
  "used": [["docs/flows/portfolio.md", "GLOSSARY.md"]]
}
~~~

An edge is directional. Normalize both paths relative to the repository root, use forward slashes, retain the file's actual casing, and keep an explicit destination anchor as part of its identity. Track current local links between Markdown files, including anchored links to other pages. Put an edge in `seen` when it appears on a page you actually review. Add it to `used` only when you follow it to another page and rely on that page for the work. Each list contains unique edges and every used edge is also seen. Opening two pages independently gives no usage credit to their link.

## Review active links

For links in scope, read valid journal entries and count distinct invocation files that record the edge as used in the last 90 days. Each contributes one point. Older uses fall outside the window. Treat a score of zero as a review candidate when the edge was first seen at least 90 days ago and another invocation saw it within the last 90 days. Exclude the current invocation from this activity check. Links with no usable history, newly observed links, and areas without recent recorded activity have insufficient evidence.

Review link validity and meaning independently of score. Repair a broken or moved target when the replacement is verified. If code or documentation changes make the relationship obsolete, update the link when the correct relationship is clear or raise the discrepancy for confirmation. Use low usage to prioritize review. Keep links that serve a documented purpose, including rare procedures or decisions. Remove or merge a link only when evidence shows it is obsolete or redundant, or the developer confirms the change. For an unresolved candidate, report the source, destination, and reason for review.

Story Walkthrough checks the relevant outgoing links on pages it reviews. Project KT can do the same for a broader documentation scope when asked. Existing documentation remains the source of truth about each relationship.
