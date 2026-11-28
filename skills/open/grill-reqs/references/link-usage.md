# Documentation link usage

Project Mapping and Grill Reqs share this journal. Either skill can maintain it on its own.

## Choose the journal

Use `docs/brain/link-usage.json` relative to the target repository root. Honor a path override in the active workspace instructions. Resolve it from the workspace that owns it and check that it stays inside that workspace's `docs/` directory and outside separate child checkouts. Preserve a configured format when the workspace explicitly requires it.

Create the parent directory on the first write. Keep new journals local and untracked. If the selected journal cannot be read or written safely, report the limitation and continue verifying links within scope. For read-only work, keep observations in the conversation.

## Record link usage

An edge is directional. Normalize source and destination paths relative to the journal-owning workspace root, use forward slashes and actual file casing, and keep any explicit destination anchor in the key. Track local Markdown links. Record an edge as seen when it appears on a page you review, and as used when you follow it and rely on the destination. Every used edge is also seen. Opening two pages independently earns no usage credit.

Use a fresh UUID and a UTC start timestamp for each independent invocation. Reuse both across pauses, resumes, retries, and mapping rounds. Read the journal at the start and save actual observations before yielding or handing off. Reread under a lock before merging and hold the lock through atomic replacement when invocations can write concurrently. Use UTF-8.

Version 2 groups edges by source and then by destination. Each date map uses invocation IDs as keys. Keep source and destination keys sorted and each destination record on one line for easy scanning.

~~~json
{
  "version": 2,
  "links": {
    "docs/brain/flows/portfolio.md": {
      "docs/brain/GLOSSARY.md": {"firstSeenAt":"2026-01-15T09:00:00Z","lastUsedAt":"2026-01-15T09:00:00Z","recentSeen":{"a3c4b8e2-7d11-4f26-8a9d-13b715d11e62":"2026-01-15T09:00:00Z"},"recentUsed":{"a3c4b8e2-7d11-4f26-8a9d-13b715d11e62":"2026-01-15T09:00:00Z"}}
    }
  }
}
~~~

- `firstSeenAt` is the earliest start timestamp of an invocation that saw the edge.
- `lastUsedAt` is the latest start timestamp of an invocation that used the edge, or `null` if the edge has never been used.
- `recentSeen` keeps the two latest distinct invocations that saw the edge. Keep them even as they age. Break timestamp ties by invocation ID.
- `recentUsed` keeps each distinct invocation that used the edge within the last 90 days. On each write, remove uses at or before the cutoff. Keep `lastUsedAt` after older uses expire.

Merge observations by invocation ID for each edge. Use the invocation start time for all its observations so replaying a save adds no points. Compare dates as UTC instants. Use the same cutoff rule for scoring and pruning.

## Migrate earlier journals

On the first write to a version 2 journal, merge history from the selected file if it is version 1. Its `entries` contain `id`, `startedAt`, `seen`, and `used`. Each edge is a two-item array ordered source then destination.

When initializing or migrating the default journal, also check `docs/link-usage.json` for version 1 entries and locate older records with `git rev-parse --path-format=absolute --git-path project-docs-usage/v1` from the target repository root. Read valid UUID-named JSON records there using the filename stem as the ID and retaining `startedAt`, `seen`, and `used`. Leave both legacy locations read-only. Merge valid observations from all available sources by edge and invocation ID before retaining the latest two sightings and pruning uses. If the workspace explicitly requires version 1, continue merging `entries` by invocation ID and use the same review rules directly over those entries.

## Review active links

For links in scope, score one point per distinct invocation in `recentUsed` with a start time later than the UTC cutoff 90 days ago. Calculate this at review time so scores expire even if the file has not been written recently. A zero-score edge is a review candidate if `firstSeenAt` is at or before the cutoff and at least one `recentSeen` invocation other than the current one is later than the cutoff. Links with missing history, new links, and areas without recent recorded activity have insufficient evidence. Leave stored diagram scores and Draw.io files untouched during journal maintenance.

Review whether links still work and whether the relationship still makes sense. Repair a broken or moved target when the replacement is verified. Update obsolete relationships when the correct replacement is clear. Keep links with a documented purpose, including rare procedures or decisions. Remove or merge a link when evidence shows it is obsolete or redundant, or the developer confirms the change. For unresolved candidates, report the source, destination, and reason for review.

Grill Reqs checks outgoing links on pages it reviews. Project Mapping can cover a broader scope when asked. The documentation remains the source of truth about each relationship.
