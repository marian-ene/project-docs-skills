# Documentation link usage

Both skills use this format. It works with either skill installed by itself.

## Choose the journal

Use `docs/brain/link-usage.json` relative to the target repository root. If the active workspace instructions specify a journal inside that workspace's `docs/` directory, use the configured file and preserve its format and history. Resolve a relative override from the workspace that owns the configuration. Check that the resolved journal path stays inside `docs/` and outside any separate child checkout.

Create the parent directory and journal on the first write. Keep the journal local and untracked. If an override is outside `docs/`, or the selected journal cannot be read or written safely, report the limitation and continue verifying links within scope. Honor read-only requests by keeping observations in the conversation.

When initializing the default journal, import valid version 1 entries from `docs/link-usage.json` if it exists. Also check for older records using `git rev-parse --path-format=absolute --git-path project-docs-usage/v1` from the target repository root. Import valid UUID-named JSON records using the filename stem as `id` and retaining `startedAt`, `seen`, and `used`. Merge by ID, preserving unique observed edges and their timestamps. Treat both legacy locations as read-only. Continue with available history if either source is missing.

## Record one entry per invocation

Read the selected journal at the start of the invocation. Use a fresh UUID and an original UTC timestamp for a new invocation. Reuse both across pauses, resumes, retries, and mapping rounds within that invocation. Save actual observations before yielding or handing off. A later, independent invocation gets a new ID.

Use a version 1 JSON object with an `entries` array by default. Add or update one entry by `id` (UUID), with `startedAt`, `seen`, and `used`. Preserve the existing container and fields in a configured journal. Reread before saving and merge observations without replacing other invocations. Serialize the read, merge, and write when invocations can save concurrently.

~~~json
{
  "version": 1,
  "entries": [
    {
      "id": "a3c4b8e2-7d11-4f26-8a9d-13b715d11e62",
      "startedAt": "2026-01-15T09:00:00Z",
      "seen": [["docs/brain/flows/portfolio.md", "docs/brain/GLOSSARY.md"]],
      "used": [["docs/brain/flows/portfolio.md", "docs/brain/GLOSSARY.md"]]
    }
  ]
}
~~~

An edge is directional. Normalize both paths relative to the journal-owning workspace root (the target repository root for the default journal), use forward slashes, retain the file's actual casing, and keep an explicit destination anchor as part of its identity. Track current local links between Markdown files, including anchored links to other pages. Put an edge in `seen` when it appears on a page you actually review. Add it to `used` only when you follow it to another page and rely on that page for the work. Each list contains unique edges and every used edge is also seen. Opening two pages independently gives no usage credit to their link. Record only observed or followed links from this invocation. Write UTF-8 and replace files atomically where supported. Store only invocation IDs, timestamps, and relative link paths in new observations.

## Review active links

For links in scope, read valid journal entries and count distinct invocation IDs that record the edge as used in the last 90 days. Each contributes one point. Older uses fall outside the window. Derive the score from the journal each time. Leave stored scores and Draw.io diagrams untouched during journal maintenance. Treat a score of zero as a review candidate when the edge was first seen at least 90 days ago and another invocation saw it within the last 90 days. Exclude the current invocation from this activity check. Links with no usable history, newly observed links, and areas without recent recorded activity have insufficient evidence.

Review link validity and meaning independently of score. Repair a broken or moved target when the replacement is verified. If code or documentation changes make the relationship obsolete, update the link when the correct relationship is clear or raise the discrepancy for confirmation. Use low usage to prioritize review. Keep links that serve a documented purpose, including rare procedures or decisions. Remove or merge a link only when evidence shows it is obsolete or redundant, or the developer confirms the change. For an unresolved candidate, report the source, destination, and reason for review.

Grill Reqs checks the relevant outgoing links on pages it reviews. Project Mapping can do the same for a broader documentation scope when asked. Existing documentation remains the source of truth about each relationship.
