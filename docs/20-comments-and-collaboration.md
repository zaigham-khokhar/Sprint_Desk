# 20 · Comments & Collaboration
> **Status:** Draft v1.0 · **Source:** MPD §5.9, §5.10, §5.11, §5.13 · **Depends on:** 05, 15, 19, 27

## 1. Comments
Threaded (one reply level), rich text (sanitized), edit with revision history [RC], soft delete. Author edits/deletes own; `comment.delete_any` for moderators (Owner/Admin/PM).

## 2. Mentions
`@username` autocomplete of project members; server parses body, stores `mentions`, notifies (doc 19). Non-members ignored (BR-NTF-04).

## 3. Attachments
Uploaded from issue or comment; rules in doc 27.

## 4. Activity feed
Per issue and per project, built from `activity_logs` (doc 25): field changes, transitions, comments, attachments, assignments; grouped by day; filter "comments only / history only".

## 5. Collaboration workflow
Reporter creates → assignee notified → discussion with mentions → attachment of evidence → transition triggers notification to reporter → resolution comment → closed.

## 6. Real-time collaboration
Presence indicator on issue detail; live comments appear without refresh; typing indicator [O]; edit conflict warning via `version`.

## 7. Permissions
| Action | WO | WA | PM | DEV | VW |
|---|---|---|---|---|---|
| Read comments | ✔ | ✔ | ✔ | ✔ | ✔ |
| Comment | ✔ | ✔ | ✔ | ✔ | ◐ (workspace setting) |
| Edit own | ✔ | ✔ | ✔ | ✔ | ◐ |
| Delete any | ✔ | ✔ | ✔ | ✖ | ✖ |

## 8. Edge cases
Deleted parent comment (thread shows placeholder); mention inside code block (ignored); editing after mention (new mentions only notify once); XSS in body (sanitizer); long threads (paginate).
