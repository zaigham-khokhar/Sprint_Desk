# 11 · API Documentation
> **Status:** Draft v1.0 · **Source:** MPD §10 · **Depends on:** 08, 09, 12 · **Permissions:** 36 · **Errors:** 31

## 1. Architecture
- Base path `/api/v1`, JSON, versioned. Web UI uses Inertia routes (doc 37); this API serves integrations, tokens and async widgets.
- Auth: Sanctum session (SPA) or bearer token with abilities. Tenant via `X-Workspace: {slug}` header.
- Rate limit: 60 req/min per user (A8), 429 with `Retry-After`.
- Pagination: cursor (`?cursor=&per_page=25`, max 100). Filtering/sorting via query params.

## 2. Request / response structure
```
Success   { "data": {...} | [...], "meta": { "next_cursor": "..." } }
Error     { "message": "...", "code": "VALIDATION_FAILED", "errors": { "field": ["msg"] } }
```
Timestamps ISO-8601 UTC. IDs numeric; issues also addressable by key (`NEX-142`).

## 3. Endpoints
Auth column: **T** = token/session required, **P** = permission required (doc 36).

### Authentication & user
| Method | Path | Purpose | Auth |
|---|---|---|---|
| POST | /auth/login | Login (token issue) | – |
| POST | /auth/logout | Logout | T |
| GET | /me | Current user + memberships | T |
| PATCH | /me | Update profile | T |
| GET/POST/DELETE | /me/tokens | Manage API tokens | T, apitoken.manage |
| GET | /users?q= | Search workspace users | T |

### Workspaces (organizations) & teams
| Method | Path | Purpose | Permission |
|---|---|---|---|
| GET/POST | /workspaces | List/create | T |
| GET/PATCH | /workspaces/{id} | View/update | workspace.view/update |
| GET | /workspaces/{id}/members | List members | workspace.view |
| POST | /workspaces/{id}/invitations | Invite | member.invite |
| PATCH/DELETE | /workspaces/{id}/members/{user} | Change role/remove | member.role_update / member.remove |
| GET/POST | /teams | List/create | team.manage |
| PATCH/DELETE | /teams/{id} | Update/delete | team.manage |
| POST/DELETE | /teams/{id}/members | Add/remove | team.manage |

### Projects
| Method | Path | Permission |
|---|---|---|
| GET/POST | /projects | project.create |
| GET/PATCH/DELETE | /projects/{id} | project.update / delete |
| POST | /projects/{id}/archive | project.archive |
| GET/POST/DELETE | /projects/{id}/members | project.member_manage |
| GET/PUT | /projects/{id}/workflow | workflow.manage |

### Issues
| Method | Path | Purpose | Permission |
|---|---|---|---|
| GET | /projects/{p}/issues | List, filter, sort | issue.view |
| POST | /projects/{p}/issues | Create | issue.create |
| GET | /issues/{key} | Detail | issue.view |
| PATCH | /issues/{key} | Update (requires `version`) | issue.update |
| DELETE | /issues/{key} | Soft delete | issue.delete |
| POST | /issues/{key}/assign | Assign | issue.assign |
| POST | /issues/{key}/transition | Change status | issue.transition |
| POST | /issues/{key}/rank | Reorder | issue.rank |
| GET/POST | /issues/{key}/subtasks | Subtasks | issue.view/create |
| POST/DELETE | /issues/{key}/labels | Labels | issue.update |

### Boards, sprints, epics
| Method | Path | Permission |
|---|---|---|
| GET | /projects/{p}/board | issue.view |
| GET | /projects/{p}/backlog | issue.view |
| GET/POST | /projects/{p}/sprints | sprint.create |
| PATCH | /sprints/{id} | sprint.create |
| POST | /sprints/{id}/start · /complete | sprint.start / complete |
| GET/POST | /projects/{p}/epics | epic.manage |

### Comments & attachments
| Method | Path | Permission |
|---|---|---|
| GET/POST | /issues/{key}/comments | issue.view / comment.create |
| PATCH | /comments/{id} | comment.update_own |
| DELETE | /comments/{id} | own or comment.delete_any |
| POST | /issues/{key}/attachments/presign | attachment.upload |
| POST | /attachments/{id}/confirm | attachment.upload |
| GET | /attachments/{id}/download | issue.view (signed URL) |
| DELETE | /attachments/{id} | attachment.delete |

### Time, search, notifications, reports, audit
| Method | Path | Permission |
|---|---|---|
| POST | /time/start · /time/stop | time.log |
| GET/POST/PATCH/DELETE | /time-entries | time.log (own) / time.view_all |
| GET | /search?q= | issue.view |
| GET/POST/DELETE | /filters | filter.save |
| GET | /notifications | T |
| POST | /notifications/read | T |
| GET/PATCH | /me/notification-preferences | T |
| GET | /projects/{p}/reports/burndown · /velocity · /workload | report.view |
| GET | /workspaces/{id}/audit-logs | audit.view |
| GET | /calendar.ics?token= | per-user token |

## 4. Validation
Server-side via FormRequests (doc 09); failures return 422 with field errors.

## 5. Authorization
Policy check per endpoint; missing tenant membership returns 404; missing permission returns 403.

## 6. Error responses
| Status | Code | Meaning |
|---|---|---|
| 401 | UNAUTHENTICATED | Missing/invalid credentials |
| 403 | FORBIDDEN | Permission denied |
| 404 | NOT_FOUND | Missing or outside tenant |
| 409 | VERSION_CONFLICT / WIP_LIMIT | Concurrency or workflow conflict |
| 422 | VALIDATION_FAILED | Invalid input |
| 429 | RATE_LIMITED | Too many requests |
| 500 | SERVER_ERROR | Unexpected (logged with request ID) |
