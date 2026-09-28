# 24 · Search & Filtering
> **Status:** Draft v1.0 · **Source:** MPD §5.14 · **Depends on:** 08, 15 · **Performance:** 28

## 1. Search scopes
| Scope | Fields |
|---|---|
| Global | Issues, projects, users (quick switcher) |
| Project | Issues in project |
| Issue | Title, description, key, comments (RC) |
| User | Name, email within workspace |
| Team | Name |

## 2. Implementation phases
Phase 1: MySQL FULLTEXT on issues + indexed filters. Later **[O]**: Meilisearch behind the `SearchEngine` interface, index updated by queued `IndexIssue` listener, filtered by `workspace_id`.

## 3. Filters
Status, type, priority, assignee (incl. "me", unassigned), reporter, label, epic, sprint, due date range, created/updated range, has attachment [RC]. Advanced query syntax: `assignee = me AND status != Done` **[R for MVP subset: AND only; OR/parentheses O]**.

## 4. Sorting & pagination
Sort by rank, created, updated, priority, due date; stable secondary sort on id. Cursor pagination, 25 default, 100 max.

## 5. Saved filters
Stored as JSON per user (optionally shared with project); appear in sidebar and dashboard widgets.

## 6. Security & edge cases
Results policy-filtered by project membership; user search limited to workspace. Edge: FULLTEXT minimum word length (fallback to LIKE for short terms), special characters escaped, deleted issues excluded, very large result sets (require additional filter), stale index (reindex command).
