# 36 · API Security & Permission Matrix
> **Status:** Draft v1.0 · **Source:** MPD §5.19, §10 · **Depends on:** 04, 11, 26 · **Used by:** tests (29)

**Legend:** ✔ Allowed · ✖ Denied · ◐ Allowed with condition. Roles: **SA** Super Admin (platform only), **WO** Workspace Owner, **WA** Workspace Admin, **PM** Project Manager, **DEV** Developer, **VW** Viewer. Non-members of the workspace always receive 404. Project-scoped rows require project membership unless project visibility is `workspace` (read only).

| Module | Action | Permission | SA | WO | WA | PM | DEV | VW | Special conditions |
|---|---|---|---|---|---|---|---|---|---|
| Workspace | View | workspace.view | ✖ | ✔ | ✔ | ✔ | ✔ | ✔ | Members only |
| Workspace | Update settings | workspace.update | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | – |
| Workspace | Delete | workspace.delete | ✖ | ✔ | ✖ | ✖ | ✖ | ✖ | Confirmation + 30-day grace |
| Workspace | Billing/plan | workspace.billing | ◐ | ✔ | ✖ | ✖ | ✖ | ✖ | SA changes plan/suspends (platform) |
| Platform | Manage tenants/health | platform.* | ✔ | ✖ | ✖ | ✖ | ✖ | ✖ | No tenant content access; impersonation audited [RC] |
| Members | Invite | member.invite | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | Cannot invite above own role |
| Members | Change role | member.role_update | ✖ | ✔ | ◐ | ✖ | ✖ | ✖ | WA cannot modify Owners; last Owner protected |
| Members | Remove | member.remove | ✖ | ✔ | ◐ | ✖ | ✖ | ✖ | WA cannot remove Owners |
| Teams | Create/edit/delete | team.manage | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | Team Lead may edit own team membership [RC] |
| Project | Create | project.create | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | – |
| Project | Update settings | project.update | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | PM only in own project |
| Project | Archive | project.archive | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | No active sprint |
| Project | Delete | project.delete | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | Must be archived first |
| Project | Manage members | project.member_manage | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | Users must be workspace members |
| Workflow | Configure | workflow.manage | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | Cannot delete status in use |
| Issue | View | issue.view | ✖ | ✔ | ✔ | ✔ | ✔ | ✔ | Project membership or workspace visibility |
| Issue | Create | issue.create | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | Project not archived |
| Issue | Update | issue.update | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | `version` must match |
| Issue | Delete | issue.delete | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | Soft delete |
| Issue | Assign | issue.assign | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | Assignee is project member |
| Issue | Transition | issue.transition | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | Allowed transition, WIP rule |
| Issue | Rank/reorder | issue.rank | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | – |
| Sprint | Create/edit | sprint.create | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | – |
| Sprint | Start | sprint.start | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | Only one active per board |
| Sprint | Complete | sprint.complete | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | Must handle unfinished issues |
| Epic | Manage | epic.manage | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | – |
| Comment | Create | comment.create | ✖ | ✔ | ✔ | ✔ | ✔ | ◐ | VW only if workspace allows |
| Comment | Edit own | comment.update_own | ✖ | ✔ | ✔ | ✔ | ✔ | ◐ | Author only |
| Comment | Delete any | comment.delete_any | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | Audited |
| Attachment | Upload | attachment.upload | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | Type/size/scan rules |
| Attachment | Delete | attachment.delete | ✖ | ✔ | ✔ | ✔ | ◐ | ✖ | DEV only own uploads |
| Time | Log own | time.log | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ | Unlocked period |
| Time | View all | time.view_all | ✖ | ✔ | ✔ | ✔ | ✖ | ✖ | – |
| Reports | View | report.view | ✖ | ✔ | ✔ | ✔ | ◐ | ◐ | DEV/VW: project reports without time data |
| Audit | View/export | audit.view | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | Own security events visible to user |
| Filters | Save | filter.save | ✖ | ✔ | ✔ | ✔ | ✔ | ✔ | Personal; sharing needs PM |
| API tokens | Manage own | apitoken.manage | ✖ | ✔ | ✔ | ✔ | ✔ | ◐ | Abilities limited to role |
| Webhooks | Manage [O] | webhook.manage | ✖ | ✔ | ✔ | ✖ | ✖ | ✖ | – |
| Calendar | iCal feed | (own token) | ✖ | ✔ | ✔ | ✔ | ✔ | ✔ | Policy-filtered items |

## API security rules
1. Bearer token abilities must be a subset of the user's role permissions.
2. Token requests require `X-Workspace`; mismatch → 404.
3. Rate limits (A8): auth 5/min, general API 60/min, uploads 20/min, search 30/min.
4. All endpoints HTTPS only; sensitive actions (role change, token create) write audit events.
5. This matrix is the source for the authorization dataset tests (doc 29).
