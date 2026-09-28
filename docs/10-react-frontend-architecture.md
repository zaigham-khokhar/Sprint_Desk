# 10 · React Frontend Architecture
> **Status:** Draft v1.0 · **Source:** MPD §11 · **Depends on:** 06, 11 · **UI rules:** 13

## 1. Folder structure
```
resources/js/
├── app.tsx  ssr.tsx
├── Pages/{Auth,Dashboard,Projects,Board,Backlog,Sprints,Issues,Reports,Calendar,Search,Settings,Admin}
├── Layouts/{AppLayout,AuthLayout,ProjectLayout,SettingsLayout}
├── Components/
│   ├── ui/         Button, Input, Modal, Dropdown, Table, Toast, Avatar, Badge, Tabs
│   ├── forms/      FormField, RichTextEditor, UserSelect, LabelSelect, DatePicker
│   ├── board/      BoardColumn, IssueCard, WipBadge
│   ├── issue/      IssueDrawer, IssueForm, CommentThread, AttachmentList, TimeLogger
│   ├── sprint/     SprintPlanner, BurndownChart
│   └── shared/     EmptyState, ErrorBoundary, Skeleton, ConfirmDialog
├── Hooks/          useChannel, useDebounce, usePermission, useOptimistic, useTheme
├── Stores/         boardStore (Zustand), uiStore
├── Lib/            api client, echo setup, formatters
└── Types/          models mirroring API Resources
```

## 2. Pages
| Page | Route | Notes |
|---|---|---|
| Dashboard | `/w/{ws}/dashboard` | Widgets |
| Projects list | `/w/{ws}/projects` | Filter/search |
| Board | `/w/{ws}/p/{key}/board` | Drag-and-drop |
| Backlog | `.../backlog` | Ranking, sprint planning |
| Sprints | `.../sprints` | Lifecycle |
| Issue detail | `/w/{ws}/issues/{key}` | Drawer or full page |
| Reports, Calendar, Search | – | – |
| Settings | Profile, security, notifications, workspace, members, roles | – |

## 3. State management
| State | Where |
|---|---|
| Server data | Inertia props (source of truth) |
| Board drag state, optimistic moves | Zustand `boardStore` |
| UI (modals, theme) | `uiStore` / context |
| Form state | Inertia `useForm` (server-side errors mapped to fields) |

## 4. API communication
Inertia visits for navigation and mutations; a small typed fetch client for REST widgets (`/api/v1`) with CSRF/session or token handling; Echo for real-time.

## 5. Real-time integration
`useChannel('project.{id}')` subscribes to events; events merge into `boardStore`; own events ignored via socket id; on reconnect, board reloads via partial Inertia reload to resync.

## 6. Forms
Inertia `useForm`, server validation errors displayed inline, disabled submit while processing, unsaved-change guard, rich text sanitized on server.

## 7. Reusable components (rules)
Presentational and stateless where possible; accessible by default (labels, focus, keyboard); no business logic in `ui/`.

## 8. Error, loading and empty states
| State | Pattern |
|---|---|
| Loading | Skeletons for lists/board; button spinners |
| Empty | `EmptyState` with explanation + primary action |
| Error | Error boundary per page section; toast for mutations; retry action |
| 403/404/409/422 | Dedicated handling (doc 31) |

## 9. Responsive architecture
Mobile-first Tailwind breakpoints; sidebar collapses to drawer; board scrolls horizontally with snap; tables become cards below `md`.

## 10. Performance
Route-level code splitting, virtualized long lists, memoized cards, debounced search, deferred props for heavy widgets (doc 28).
