# 35 · Project Task Breakdown
> **Status:** Draft v1.0 · **Source:** MPD roadmap · **Depends on:** 03, 34 · **Class:** BE Backend · FE Frontend · DB Database · DO DevOps · QA

| ID | Module | Task | Description | Depends | Pri | Class | Acceptance criteria |
|---|---|---|---|---|---|---|---|
| T-001 | Foundation | Docker environment | Compose with app, nginx, mysql, redis, mailpit | – | P0 | DO | `docker compose up` runs app locally |
| T-002 | Foundation | CI skeleton | Lint + test workflow | T-001 | P0 | DO | PR blocked on failure |
| T-003 | Auth | Auth backend | Register/login/logout/reset, throttling | T-001 | P0 | BE | Feature tests pass |
| T-004 | Auth | Auth pages | Login, register, reset UI | T-003 | P0 | FE | Errors shown inline |
| T-005 | Auth | Two-factor | TOTP setup/challenge/recovery | T-003 | P1 | BE/FE | Login requires code when enabled |
| T-006 | Profile | Profile & sessions | Avatar, timezone, session list | T-003 | P1 | BE/FE | Revoke session works |
| T-007 | Workspace | Workspace schema | workspaces, members, roles, permissions | T-003 | P0 | DB | Migrations + seeders |
| T-008 | Tenancy | Tenant scope | Middleware + global scope trait | T-007 | P0 | BE | Cross-tenant tests 404 |
| T-009 | RBAC | Permission resolver & policies | Cached resolver, base policies | T-007 | P0 | BE | Matrix (36) tests pass |
| T-010 | Workspace | Invitations | Signed tokens, accept flow | T-007 | P0 | BE/FE | Expired token rejected |
| T-011 | Workspace | Member/role management UI | List, change role, remove | T-009 | P1 | FE | Last owner protected |
| T-012 | Teams | Teams CRUD | Backend + UI | T-007 | P1 | BE/FE | Members add/remove |
| T-013 | Project | Project schema & service | Key, lead, template, seed workflow | T-008 | P0 | DB/BE | Unique key enforced |
| T-014 | Project | Project UI | List, create, settings, members | T-013 | P0 | FE | Archive works |
| T-015 | Workflow | Workflow engine | Statuses, transitions, validation | T-013 | P0 | BE | Invalid transition 409 |
| T-016 | Issue | Issue schema + indexes | Per doc 08 | T-013 | P0 | DB | FULLTEXT + unique key |
| T-017 | Issue | Issue service | Create with sequence lock, update with version | T-015, T-016 | P0 | BE | Concurrent create no duplicates |
| T-018 | Issue | Issue UI | Create modal, detail drawer, inline edit | T-017 | P0 | FE | Optimistic update reverts on error |
| T-019 | Issue | Subtasks & labels | One-level subtasks | T-017 | P1 | BE/FE | BR-ISS-04 enforced |
| T-020 | Issue | Assignment | Assign + policy + notify hook | T-017 | P0 | BE/FE | Non-member rejected |
| T-021 | Board | Ranking service | Fractional rank + rebalance job | T-017 | P0 | BE | Order stable |
| T-022 | Board | Kanban board | Columns, DnD, filters, WIP | T-021 | P0 | BE/FE | Move persists, revert on error |
| T-023 | Backlog | Backlog page | Ranking, bulk edit | T-021 | P0 | FE/BE | Bulk update works |
| T-024 | Comments | Comments + mentions | Threads, parsing, sanitization | T-017 | P0 | BE/FE | Mention notifies |
| T-025 | Files | Attachments | Presign, confirm, scan, download | T-017 | P1 | BE/FE | Infected file quarantined |
| T-026 | Notifications | Notification pipeline | Events, listeners, prefs, mail | T-017 | P0 | BE | Dedup within 60 s |
| T-027 | Notifications | Notification UI | Bell, list, preferences | T-026 | P1 | FE | Mark read works |
| T-028 | Sprint | Sprint service | Lifecycle rules | T-021 | P0 | BE | BR-SPR tests pass |
| T-029 | Sprint | Sprint planning UI | Planner, complete dialog | T-028 | P0 | FE | Unfinished moved correctly |
| T-030 | Epic | Epics | CRUD + progress | T-017 | P1 | BE/FE | Progress accurate |
| T-031 | Reports | Snapshot job | Nightly remaining points | T-028 | P1 | BE | Snapshots per active sprint |
| T-032 | Real-time | Reverb + channels | Auth channels, broadcast events | T-022, T-026 | P1 | BE/DO | Private auth enforced |
| T-033 | Real-time | Echo hooks + presence | Board/issue live updates | T-032 | P1 | FE | Two-browser test passes |
| T-034 | Search | Search + filters | FULLTEXT, filter bar, saved filters | T-016 | P0 | BE/FE | Policy-filtered results |
| T-035 | Dashboard | Dashboard widgets | Per doc 23 | T-031 | P1 | BE/FE | Loads < 1 s cached |
| T-036 | Reports | Reports | Sprint, velocity, workload | T-031 | P1 | BE/FE | Values match manual calc |
| T-037 | Time | Time tracking | Timers, entries, timesheet | T-017 | P1 | BE/FE | One timer rule |
| T-038 | Calendar | Calendar + iCal | Views + feed | T-017, T-028 | P2 | BE/FE | Feed valid |
| T-039 | Audit | Audit logging | Listeners + admin UI + export | T-009 | P0 | BE/FE | Immutable, filterable |
| T-040 | API | REST API v1 + tokens | Resources, docs | T-017 | P2 | BE | Contract tests pass |
| T-041 | UX | Dark mode, a11y pass | Tokens, axe checks | T-018 | P2 | FE | No critical axe issues |
| T-042 | Performance | Caching + index review | Redis caches, EXPLAIN review | T-036 | P1 | BE/DB | Budgets met |
| T-043 | Security | Security hardening | Headers, throttles, dependency audit | T-039 | P0 | BE/DO | Checklist (26) green |
| T-044 | Testing | Test suites completion | Tenant, authz, E2E | All | P0 | QA | Coverage ≥ 80 % |
| T-045 | DevOps | CD + staging | Deploy pipeline | T-002 | P0 | DO | Auto staging deploy |
| T-046 | DevOps | Monitoring & backups | Sentry, alerts, backups | T-045 | P0 | DO | Restore drill passed |
| T-047 | QA | Load test | k6 at 500 users | T-045 | P1 | QA | Budgets met |
| T-048 | Release | Production launch | Runbook, approval, release | T-046, T-047 | P0 | DO | v1.0 live |
