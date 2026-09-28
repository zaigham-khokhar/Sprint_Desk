# 34 · Development Roadmap
> **Status:** Draft v1.0 · **Source:** MPD "Development Roadmap" · **Depends on:** 03 · **Tasks:** 35

## 1. Phases
| Phase | Scope | Depends on | Milestone |
|---|---|---|---|
| 1 Foundation | Docker env, repo, CI skeleton, auth, 2FA, profile | – | M1 Login works in CI |
| 2 Tenancy & RBAC | Workspaces, invitations, roles, policies, tenant scope | 1 | M2 Isolation tests green |
| 3 Projects & Issues | Projects, workflows, issues, subtasks, labels | 2 | M3 Create/track issues |
| 4 Boards & Backlog | Kanban, ranking, backlog | 3 | M4 Drag-and-drop live |
| 5 Collaboration | Comments, mentions, attachments, notifications | 3 | M5 Team collaboration |
| 6 Agile | Sprints, epics, snapshots | 4 | M6 Full sprint cycle |
| 7 Real-time | Reverb, channels, presence | 4, 5 | M7 Two-browser sync |
| 8 Insight | Search, filters, dashboards, reports, time, calendar | 6 | M8 Reporting complete |
| 9 Hardening | Audit UI, caching, performance, security review, full test suite | 1–8 | M9 Release candidate |
| 10 Production | Staging, CD, monitoring, backups, load test, launch | 9 | M10 v1.0 live |
Phases 4 and 5 can run in parallel; 7 requires both.

## 2. Work per phase
| Phase | Backend | Frontend | Database | Testing | Deployment |
|---|---|---|---|---|---|
| 1 | Fortify, sessions, 2FA | Auth pages, layout | users, sessions | Auth tests | Docker, CI |
| 2 | Tenancy scope, RBAC, invites | Workspace, members UI | workspaces, roles, members, invitations | Tenant + authz suites | – |
| 3 | Project/Issue services | Project list, issue form/drawer | projects, workflows, issues, labels | Feature tests | – |
| 4 | Transitions, ranking | Board, backlog DnD | rank, indexes | E2E board | – |
| 5 | Comments, uploads, notifications | Threads, uploader, bell | comments, attachments, notifications | Upload/notify tests | Workers |
| 6 | Sprint/Epic services, snapshots | Planner, burndown | sprints, snapshots | Sprint tests | Scheduler |
| 7 | Broadcast events, channel auth | Echo hooks, presence | – | Real-time E2E | Reverb service |
| 8 | Search, reports, time | Filters, dashboard, timesheet, calendar | time_entries, filters | Report accuracy | – |
| 9 | Caching, audit UI, throttles | Polish, a11y, dark mode | Indexes, partitions | Coverage, security | – |
| 10 | – | – | – | Load, smoke | Staging/prod, monitoring |

## 3. Implementation order
Follows phase numbers; within a phase: database → backend service/policy → API/routes → frontend → tests → docs.
