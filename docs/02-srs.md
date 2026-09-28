# 02 · Software Requirements Specification (SRS)
> **Status:** Draft v1.0 · **Source:** MPD §1–30 · **Depends on:** 01 · **Feature detail:** 03 · **Rules:** 05

## 1. Business requirements
| ID | Requirement | Priority |
|---|---|---|
| BRQ-01 | Provide one place to plan, track and report on work | [R] |
| BRQ-02 | Support several companies on one platform with strict data separation | [R] |
| BRQ-03 | Provide audit evidence for compliance | [R] |
| BRQ-04 | Reduce status-meeting time through live boards and reports | [R] |

## 2. User requirements
| ID | As a… | I want to… |
|---|---|---|
| UR-01 | Owner | create a workspace, invite people, assign roles |
| UR-02 | Project Manager | plan sprints, manage epics, view velocity |
| UR-03 | Developer | create, update and move issues, log time, comment |
| UR-04 | Viewer/Client | see project progress without editing |
| UR-05 | Super Admin | manage tenants and system health |

## 3. Functional requirements
| ID | Requirement | Tag |
|---|---|---|
| FR-AUTH-01 | Register, login, logout | R |
| FR-AUTH-02 | Password reset via signed expiring link | R |
| FR-AUTH-03 | TOTP two-factor authentication | R |
| FR-AUTH-04 | Email verification | RC |
| FR-WS-01 | Create workspace; owner assigned automatically | R |
| FR-WS-02 | Invite by email with role; expiring token | R |
| FR-WS-03 | Teams group users | R |
| FR-PRJ-01 | Create project with unique key, lead, template (Scrum/Kanban) | R |
| FR-PRJ-02 | Custom workflow statuses and transitions | R |
| FR-PRJ-03 | Archive project | R |
| FR-ISS-01 | Create/edit/delete issues (Bug, Story, Task, Epic, Subtask) | R |
| FR-ISS-02 | Auto issue key `KEY-n` | R |
| FR-ISS-03 | Assign, prioritize, label, estimate, set due date | R |
| FR-ISS-04 | Subtasks (one level) | R |
| FR-ISS-05 | Issue links/dependencies | RC |
| FR-BRD-01 | Kanban board with drag-and-drop transitions | R |
| FR-BRD-02 | WIP limits | R |
| FR-BRD-03 | Swimlanes | O |
| FR-SPR-01 | Sprint create/start/complete | R |
| FR-SPR-02 | Backlog ordering and bulk edit | R |
| FR-SPR-03 | Burndown and velocity | R |
| FR-EPC-01 | Epics with progress | R |
| FR-COM-01 | Threaded comments, @mentions | R |
| FR-ATT-01 | Attachments with validation and virus scan | R |
| FR-NTF-01 | In-app, email notifications with preferences | R |
| FR-RT-01 | Real-time board/issue updates, presence | R |
| FR-SRC-01 | Search and filters; saved filters | R |
| FR-RPT-01 | Dashboard and reports | R |
| FR-TIM-01 | Timers and manual time entries | R |
| FR-CAL-01 | Calendar and iCal feed | R |
| FR-AUD-01 | Immutable audit log | R |
| FR-PRF-01 | Profile, timezone, API tokens, sessions | R |
| FR-UI-01 | Dark mode | RC |
| FR-DAT-01 | Workspace data export | RC |

## 4. Non-functional requirements
| ID | Category | Requirement |
|---|---|---|
| NFR-01 | Performance | p95 page response < 500 ms; API p95 < 300 ms at 500 concurrent users |
| NFR-02 | Real-time | Event-to-screen latency < 1 s |
| NFR-03 | Availability | 99.5 % (MVP), 99.9 % target |
| NFR-04 | Security | OWASP Top 10 mitigated; tenant isolation verified by tests (doc 26) |
| NFR-05 | Scalability | Stateless app tier; horizontal workers (doc 28) |
| NFR-06 | Maintainability | ≥ 80 % backend coverage; lint and static analysis in CI |
| NFR-07 | Accessibility | WCAG 2.1 AA target |
| NFR-08 | Compatibility | Latest 2 versions of Chrome, Edge, Firefox, Safari; responsive ≥ 360 px |
| NFR-09 | Recoverability | Daily backups, PITR, RPO ≤ 15 min, RTO ≤ 4 h (A8) |
| NFR-10 | Auditability | All state changes logged with actor and diff |

## 5. System requirements
| Item | Requirement |
|---|---|
| Server | PHP 8.3+, MySQL 8, Redis 7, Node 20+ for builds |
| Runtime | Docker containers (doc 32) |
| Storage | S3-compatible object storage |
| Client | Modern browser with WebSocket support |

## 6. Acceptance criteria (system level)
1. All [R] requirements above have passing feature tests (doc 29).
2. Cross-tenant access tests all return 404/403 (doc 07).
3. Authorization matrix (doc 36) verified for every role.
4. Two-browser real-time test passes.
5. Final checklist (doc 40) fully verified.
