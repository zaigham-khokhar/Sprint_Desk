# 25 · Audit Logging
> **Status:** Draft v1.0 · **Source:** MPD §5.11 · **Depends on:** 05, 08 · **Security:** 26

## 1. Principles
Immutable, append-only, written by listeners (never controllers), workspace-scoped, includes actor, subject, action, before/after diff, IP and user agent. Table: `activity_logs` (doc 08).

## 2. Trackable actions
| Category | Actions |
|---|---|
| Issues | created, updated (per field), transitioned, assigned, ranked, moved sprint, deleted, restored |
| Collaboration | comment added/edited/deleted, attachment added/removed |
| Projects | created, updated, archived, member added/removed, workflow changed |
| Sprints | created, started, completed, scope changed |
| Time | entry created/edited/deleted, timesheet locked |
| Administrative | member invited/removed/role changed, team changes, workspace settings, API token created/revoked |
| Security | login success/failure, 2FA enabled/disabled, password changed/reset, session revoked, permission denied (sampled) |

## 3. User activity vs. audit
Issue/project feeds are filtered views of the same log. Security events also stored with `subject_type = user`.

## 4. Access
`audit.view` (Owner, Admin). Filter by actor, action, date, subject; CSV export. Users can see their own security events in profile.

## 5. Retention & storage
Default 24 months (A6), then archived/purged by scheduled job; monthly partitions make purge cheap. Sensitive values (passwords, tokens) never logged; PII minimized.

## 6. Edge cases
Bulk operations (one log per issue, plus one summary); deleted actor (keep actor_id, show "Deleted user"); very large diffs (truncate with hash); log-write failure must not fail user action but is retried and alerted.
