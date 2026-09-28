# 13 · UI/UX Requirements
> **Status:** Draft v1.0 · **Source:** MPD §5, §11 · **Depends on:** 03, 10 · **Accessibility target:** WCAG 2.1 AA

## 1. Design system
| Element | Specification |
|---|---|
| Framework | Tailwind CSS with design tokens as CSS variables |
| Typography | One sans-serif family; 14 px base; scale 12/14/16/20/24/32 |
| Colors | Neutral gray scale, one primary, semantic success/warning/danger; priority and status colors also carry icon/text (not color alone) |
| Spacing | 4 px grid |
| Components | Doc 10 `ui/` library |
| Dark mode [RC] | Token-based theme, follows OS, user override |

## 2. Layout & navigation
- **Header:** workspace switcher, global search (`/`), quick create (`c`), notifications bell, profile menu.
- **Sidebar:** Dashboard, Projects (with favorites), My Work, Calendar, Reports, Settings. Project sub-nav: Board, Backlog, Sprints, Epics, Issues, Reports, Settings.
- **Breadcrumbs** on nested pages.

## 3. Key screens
| Screen | Requirements |
|---|---|
| Dashboard | My open issues, active sprint progress, recent activity, workload |
| Project pages | Summary, members, activity, settings tabs |
| Issue page/drawer | Title inline-edit, fields sidebar, description, subtasks, comments, attachments, time, history tabs |
| Kanban board | Columns with counts and WIP badge, card shows key, title, assignee avatar, priority, labels, due-date warning; drag with keyboard alternative |
| Backlog | Two-pane: backlog + sprints, drag between, bulk select |
| Forms | Labels above fields, inline validation, required marker, submit disabled while processing |
| Tables | Sortable headers, sticky header, column visibility, pagination, row actions menu |
| Modals | Focus trap, ESC closes, destructive actions need confirm |
| Filters/search | Filter bar with chips, saved filters, debounced search, clear-all |

## 4. States
| State | Requirement |
|---|---|
| Loading | Skeleton matching final layout |
| Empty | Icon, one-line explanation, primary action |
| Error | Human message, retry, request ID for support |
| Offline/reconnecting | Banner when WebSocket drops |

## 5. Responsive
Breakpoints 360 / 768 / 1024 / 1440. Mobile: bottom-sheet modals, board scrolls horizontally, issue detail full-screen.

## 6. Accessibility
Keyboard operability everywhere (including board moves via menu), visible focus, ARIA roles for dialogs/menus/live regions (announce real-time changes politely), contrast ≥ 4.5:1, respects reduced-motion.

## 7. Keyboard shortcuts [O]
`/` search · `c` create issue · `g b` go to board · `?` shortcut help.
