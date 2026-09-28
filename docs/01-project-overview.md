# 01 · Project Overview
> **Status:** Draft v1.0 · **Source:** Master Project Document · **Depends on:** none · **Read next:** 02, 03

## 1. Conventions used in every document
| Tag | Meaning |
|---|---|
| **[R]** Required | Stated in the Master Project Document (MPD) |
| **[RC]** Recommended Supporting Requirement | Not in the MPD, but technically necessary or strongly advisable |
| **[O]** Optional | Nice to have; deferred |

**Assumptions** (referenced as A1…A8 across the set):
| ID | Assumption |
|---|---|
| A1 | The MPD is the published document *"Enterprise Project Management & Collaboration Platform: System Design"*. If your MPD differs, the MPD wins and these docs must be updated. |
| A2 | "Organization" in the request equals **Workspace** in the MPD. This set uses **Workspace** everywhere (the tenant). |
| A3 | "Feature" is not a base issue type in the MPD (Bug, Story, Task, Epic, Subtask). It is treated as a *Story* or an optional custom type **[O]**. |
| A4 | Billing/plans exist as a `workspaces.plan` field only; payment processing is out of MVP scope. |
| A5 | Dark mode is delivered as **[RC]**. |
| A6 | Audit log retention default is 24 months, configurable. |
| A7 | Single-region deployment initially. |
| A8 | Numeric limits (rate limits, page sizes) are starting values, tunable after load testing. |

## 2. Purpose & vision
**Purpose.** A multi-tenant SaaS where organizations plan, track and ship work through Projects, Issues, Sprints, Kanban boards and real-time collaboration.
**Vision.** A maintainable, fast, enterprise-ready Jira alternative that teams can adopt without weeks of configuration, built as a Laravel modular monolith with a React (Inertia) frontend.

## 3. Problem statement
Example company **Nexora Logistics** (120 staff) tracks work in spreadsheets, chat and email: no single source of truth, lost requests, unclear ownership, no sprint visibility, no audit trail. See MPD §1–3.

## 4. Target users & companies
- **Users:** software teams, agencies, IT departments, PMOs, QA teams, external clients (read-only).
- **Companies:** 10–500 staff, software or IT-service oriented, needing role control and auditability without Jira's admin overhead.

## 5. Objectives
| Objective | Measure |
|---|---|
| Single source of truth for work | Every task is an issue with owner, status, history |
| Real-time visibility | Board updates reach viewers in < 1 s |
| Enterprise readiness | RBAC, audit logs, tenant isolation |
| Engineering quality | ≥ 80 % backend coverage, CI-gated merges |
| Scalability | 500 concurrent users per workspace, 1 M+ issues |

## 6. Scope
| In scope [R] | Out of scope (initially) |
|---|---|
| Auth, workspaces, teams, projects, issues, boards, backlog, sprints, epics | Payment processing (A4) |
| Comments, mentions, attachments, notifications, real-time | Native mobile apps [O] |
| Search, dashboards, reports, time tracking, calendar, audit logs | Automation rules, GitHub/Slack integrations [O] |
| REST API, API tokens, Docker, CI/CD | SSO SAML/OIDC [O], multi-region [O] |

## 7. Technology stack
Laravel · React · Inertia.js · Tailwind CSS · MySQL · Redis · Laravel Queues/Horizon · Events & Listeners · Laravel Reverb (WebSockets) · Docker · Git/GitHub Actions · Meilisearch (later phase). Details: doc 06.

## 8. Major modules
| # | Module | Doc |
|---|---|---|
| 1 | Auth & Access | 12 |
| 2 | Workspace & Team Management | 18 |
| 3 | Project Management | 14 |
| 4 | Issue Management | 15 |
| 5 | Kanban & Workflow | 16 |
| 6 | Sprint, Backlog & Epics | 17 |
| 7 | Comments & Collaboration | 20 |
| 8 | Notifications | 19 |
| 9 | Search & Filtering | 24 |
| 10 | Reports & Analytics | 23 |
| 11 | Time Tracking | 21 |
| 12 | Calendar | 22 |
| 13 | Audit Logging | 25 |
| 14 | Files & Storage | 27 |
