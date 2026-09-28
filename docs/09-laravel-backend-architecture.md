# 09 · Laravel Backend Architecture
> **Status:** Draft v1.0 · **Source:** MPD §7, §11, §12 · **Depends on:** 06, 07, 08 · **See also:** 11, 12, 19

## 1. Folder structure
```
app/
├── Actions/            single-purpose operations (StartSprint, MoveIssue)
├── DTOs/               typed input objects (CreateIssueData)
├── Enums/              IssueType, Priority, SprintState, Role
├── Events/  Listeners/ Jobs/  Notifications/
├── Exceptions/         domain exceptions
├── Http/
│   ├── Controllers/{Web,Api/V1}
│   ├── Middleware/     ResolveWorkspace, EnsureProjectAccess
│   ├── Requests/       FormRequests
│   └── Resources/      API Resources
├── Models/  Policies/  Scopes/  Traits/
├── Providers/
├── Repositories/       Contracts + Eloquent/Search implementations
└── Services/           domain services
```

## 2. Layer responsibilities
| Layer | Rule |
|---|---|
| Controller | Thin: authorize, call service, return response |
| FormRequest | Validation and input normalization |
| Policy | Authorization decisions only |
| Service | Business rules, transactions, event dispatch |
| Repository | Only for search and reporting (RC) |
| Model | Relations, scopes, casts; no business workflows |
| Resource | Output shape for API |

## 3. Models
User, Workspace, WorkspaceMember, Role, Permission, Team, Invitation, Project, ProjectMember, Workflow, WorkflowStatus, WorkflowTransition, Issue, IssueLink, Label, Sprint, Comment, Mention, Attachment, TimeEntry, ActivityLog, SavedFilter, ReportSnapshot.

## 4. Controllers (representative)
WorkspaceController, InvitationController, TeamController, ProjectController, WorkflowController, IssueController, IssueTransitionController, IssueRankController, BoardController, BacklogController, SprintController, EpicController, CommentController, AttachmentController, TimeEntryController, SearchController, ReportController, NotificationController, AuditLogController, ProfileController.

## 5. Form Requests
One per write operation, e.g. `StoreIssueRequest`, `TransitionIssueRequest`, `StartSprintRequest`, `InviteMemberRequest`. Custom rules: `ValidTransition`, `ProjectMember`, `UniqueProjectKey`.

## 6. Policies
WorkspacePolicy, ProjectPolicy, IssuePolicy, SprintPolicy, CommentPolicy, AttachmentPolicy, TimeEntryPolicy, AuditLogPolicy. Policies read permissions from a cached `PermissionResolver`.

## 7. Middleware
`ResolveWorkspace` (tenant), `EnsureWorkspaceMember`, `EnsureProjectAccess`, `ThrottleByUser`, `SecurityHeaders`, `HandleInertiaRequests` (shares auth user, workspace, permissions, flash).

## 8. Services
WorkspaceService, InvitationService, ProjectService, WorkflowService, IssueService, RankingService, SprintService, EpicService, CommentService (mention parsing), AttachmentService, TimeTrackingService, NotificationService, ReportService, AuditService, PermissionResolver.

## 9. Repositories & DTOs
- Repositories: `IssueSearchRepository` (MySQL FULLTEXT, later Meilisearch behind the same interface), `ReportRepository`. Simple CRUD uses Eloquent directly.
- DTOs for multi-field creates/updates passed FormRequest → Service.

## 10. API Resources
IssueResource, IssueCollection, ProjectResource, SprintResource, CommentResource, UserResource (minimal fields), NotificationResource.

## 11. Events, listeners, jobs, notifications
| Event | Listeners (queued) |
|---|---|
| IssueCreated | WriteAuditLog, NotifyAssignee, BroadcastIssueChange, IndexIssue |
| IssueUpdated | WriteAuditLog, BroadcastIssueChange, IndexIssue |
| IssueTransitioned | WriteAuditLog, NotifyWatchers, BroadcastBoardChange |
| CommentAdded | WriteAuditLog, NotifyMentioned, BroadcastIssueChange |
| SprintStarted / Completed | WriteAuditLog, SnapshotSprint, NotifyMembers |
| MemberInvited | SendInvitationMail, WriteAuditLog |
Jobs: ScanAttachment, GenerateSprintSnapshot (scheduled), SendDigestEmail, StopStaleTimers, PurgeExpiredInvitations, PurgeDeletedWorkspaces. Details in doc 19.

## 12. Exceptions
`InvalidTransitionException`, `WipLimitExceededException`, `VersionConflictException`, `SprintStateException`, `TenantMismatchException`. Mapped centrally (doc 31).

## 13. Service providers, DI, container
- `AppServiceProvider`: bind repositories/interfaces, `preventLazyLoading` in non-production.
- `TenancyServiceProvider`: tenant context singleton.
- `AuthServiceProvider`: policy map, Gate::before for Super Admin platform abilities only.
- Services receive dependencies by constructor injection; interfaces bound in providers.

## 14. SOLID application
| Principle | Where |
|---|---|
| S | One service per domain, one Action per complex operation |
| O | New notification channels/report generators added without editing core services |
| L | `SearchEngine` implementations interchangeable |
| I | Small contracts (`Rankable`, `Auditable`) |
| D | Services depend on interfaces and are bound in providers |
