# 40 · Final Feature Checklist
> **Status:** Draft v1.0 · **Source:** Docs 02, 03, 36 · Use for final QA and client sign-off. Tag: R required · RC recommended · O optional.

## Authentication & profile
- [ ] Register (R) · [ ] Login/logout (R) · [ ] Password reset, link single-use (R)
- [ ] Email verification (RC) · [ ] Login throttling (R) · [ ] TOTP 2FA + recovery codes (R)
- [ ] Profile: name, avatar, timezone (R) · [ ] Session list/revoke (R) · [ ] API tokens (R)
- [ ] Notification preferences (R)

## Workspace, teams, roles
- [ ] Create workspace (R) · [ ] Workspace switcher (R) · [ ] Workspace settings (R)
- [ ] Invite, resend, revoke, expire (R) · [ ] Change role/remove member (R) · [ ] Last owner protected (R)
- [ ] Teams CRUD + membership (R) · [ ] Roles/permissions enforced per matrix (R)
- [ ] Workspace deletion with grace period (R)

## Projects
- [ ] Create with unique key/lead/template (R) · [ ] Settings (R) · [ ] Members + project roles (R)
- [ ] Visibility private/workspace (RC) · [ ] Archive/read-only (R) · [ ] Project dashboard (R) · [ ] Project activity (R)

## Workflow & board
- [ ] Custom statuses/transitions (R) · [ ] Required fields on transition (R)
- [ ] Kanban board display (R) · [ ] Drag-and-drop + keyboard alternative (R) · [ ] Revert on failure (R)
- [ ] WIP limits (R) · [ ] Board filters (R) · [ ] Swimlanes (O)

## Issues
- [ ] Create/edit/delete/restore (R) · [ ] Types Bug/Story/Task/Epic/Subtask (R)
- [ ] Sequential keys (R) · [ ] Priority, assignee, reporter, labels, due date, estimate (R)
- [ ] Subtasks (one level) (R) · [ ] Optimistic locking 409 (R) · [ ] Issue links (RC)
- [ ] Bulk edit (R) · [ ] Issue history (R)

## Backlog, sprints, epics
- [ ] Backlog ranking (R) · [ ] Create/plan sprint (R) · [ ] Start with snapshot (R) · [ ] Scope change logging (R)
- [ ] Complete + move unfinished (R) · [ ] One active sprint per board (R) · [ ] Epics + progress (R)
- [ ] Burndown (R) · [ ] Velocity (R)

## Collaboration
- [ ] Threaded comments (R) · [ ] Edit/delete rules (R) · [ ] Mentions + notifications (R) · [ ] Comment revisions (RC)
- [ ] Attachments: validation, scan, signed download, delete (R)
- [ ] Activity feed (R) · [ ] Presence (R) · [ ] Live updates (R)

## Notifications
- [ ] In-app + bell (R) · [ ] Email (R) · [ ] Preferences (R) · [ ] Dedup (R) · [ ] Digest (RC)
- [ ] Retry/failure handling (R)

## Search, reports, time, calendar
- [ ] Global/project search (R) · [ ] Filters + sorting + pagination (R) · [ ] Saved filters (R)
- [ ] Dashboard widgets (R) · [ ] Project/sprint/team/productivity reports (R) · [ ] CSV export (R) · [ ] CFD, cycle time (RC)
- [ ] Timer, manual entry, timesheet (R) · [ ] Timesheet lock (RC) · [ ] Stale timer auto-stop (R)
- [ ] Calendar month/week/agenda (R) · [ ] iCal feed (R)

## Audit & admin
- [ ] Immutable audit log (R) · [ ] Audit viewer + filters + export (R) · [ ] Security events (R) · [ ] Retention purge (R)
- [ ] REST API v1 (R) · [ ] API docs/OpenAPI (RC)

## UX
- [ ] Responsive 360/768/1024 (R) · [ ] Loading/empty/error states (R) · [ ] Accessibility AA checks (R) · [ ] Dark mode (RC)

## Security & isolation
- [ ] Cross-tenant tests (web, API, channels, files, search) (R) · [ ] CSRF/XSS/SQLi checks (R)
- [ ] Rate limits (R) · [ ] Security headers (R) · [ ] Dependency audit clean (R) · [ ] Secrets scan (R)

## Quality & operations
- [ ] Coverage ≥ 80 % (R) · [ ] Authorization matrix tests (R) · [ ] E2E flows (R) · [ ] Load test budgets (R)
- [ ] Docker one-command setup (R) · [ ] CI gates (R) · [ ] Staging + production deploy (R) · [ ] Rollback tested (R)
- [ ] Monitoring/alerts (R) · [ ] Backups + restore drill (R)

## Sign-off
- [ ] QA lead · [ ] Tech lead · [ ] Client representative
