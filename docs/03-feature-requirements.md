# 03 · Feature Requirements
> **Status:** Draft v1.0 · **Source:** MPD §3, §5 · **Depends on:** 01, 02 · **Detail:** module docs 14–25

**Priority:** P0 = MVP-critical, P1 = MVP, P2 = advanced, P3 = optional. **Phase** = roadmap phase (doc 34).

| ID | Feature | Description | Depends on | Pri | Set | Phase |
|---|---|---|---|---|---|---|
| F-01 | Registration/Login | Email + password auth | – | P0 | MVP | 1 |
| F-02 | Password reset | Signed link | F-01 | P0 | MVP | 1 |
| F-03 | Two-factor auth | TOTP | F-01 | P1 | MVP | 1 |
| F-04 | Profile & settings | Avatar, timezone, prefs | F-01 | P1 | MVP | 1 |
| F-05 | Workspace creation | Tenant boundary | F-01 | P0 | MVP | 2 |
| F-06 | Invitations | Email token invites | F-05 | P0 | MVP | 2 |
| F-07 | RBAC | Roles, permissions, policies | F-05 | P0 | MVP | 2 |
| F-08 | Teams | Group users | F-05 | P1 | MVP | 2 |
| F-09 | Projects | Key, lead, template | F-05 | P0 | MVP | 3 |
| F-10 | Project members | Project-level roles | F-09, F-07 | P0 | MVP | 3 |
| F-11 | Workflows | Statuses, transitions | F-09 | P0 | MVP | 3 |
| F-12 | Issues | CRUD, keys, fields | F-09, F-11 | P0 | MVP | 3 |
| F-13 | Subtasks | One level | F-12 | P1 | MVP | 3 |
| F-14 | Labels | Tagging | F-12 | P1 | MVP | 3 |
| F-15 | Issue assignment | With notification | F-12 | P0 | MVP | 3 |
| F-16 | Kanban board | Drag-and-drop | F-12, F-11 | P0 | MVP | 4 |
| F-17 | Backlog ranking | Ordered list, bulk edit | F-12 | P0 | MVP | 4 |
| F-18 | WIP limits | Column limits | F-16 | P2 | Adv | 4 |
| F-19 | Comments | Threaded | F-12 | P0 | MVP | 5 |
| F-20 | Mentions | @user notifications | F-19 | P1 | MVP | 5 |
| F-21 | Attachments | Upload + scan | F-12 | P1 | MVP | 5 |
| F-22 | Notifications | In-app + email | F-12 | P0 | MVP | 5 |
| F-23 | Sprints | Lifecycle | F-17 | P0 | MVP | 6 |
| F-24 | Epics | Progress rollup | F-12 | P1 | MVP | 6 |
| F-25 | Burndown/velocity | Snapshots | F-23 | P1 | MVP | 6 |
| F-26 | Real-time | Live boards, presence | F-16, F-22 | P1 | MVP | 7 |
| F-27 | Search | FULLTEXT + filters | F-12 | P0 | MVP | 8 |
| F-28 | Saved filters | Per user | F-27 | P2 | Adv | 8 |
| F-29 | Dashboards | Widgets | F-12 | P1 | MVP | 8 |
| F-30 | Reports | Sprint, team, time | F-23 | P1 | MVP | 8 |
| F-31 | Time tracking | Timers, manual | F-12 | P1 | MVP | 8 |
| F-32 | Calendar | Due dates, iCal | F-12, F-23 | P2 | Adv | 8 |
| F-33 | Audit logs | Immutable log | F-07 | P0 | MVP | 9 |
| F-34 | API tokens | Sanctum | F-01 | P2 | Adv | 9 |
| F-35 | Issue links [RC] | Blocks/relates | F-12 | P2 | Adv | 9 |
| F-36 | Dark mode [RC] | Theme | – | P2 | Adv | 8 |
| F-37 | Data export [RC] | Workspace export | F-05 | P3 | Adv | 10 |
| F-38 | Swimlanes | By assignee/epic | F-16 | P3 | Opt | – |
| F-39 | Webhooks | Outbound events | F-33 | P3 | Opt | – |
| F-40 | Meilisearch | Search upgrade | F-27 | P3 | Opt | – |

## MVP vs Advanced
- **MVP (P0–P1):** F-01–F-17, F-19–F-27, F-29–F-31, F-33.
- **Advanced (P2):** F-18, F-28, F-32, F-34–F-36.
- **Optional (P3):** F-37–F-40.
