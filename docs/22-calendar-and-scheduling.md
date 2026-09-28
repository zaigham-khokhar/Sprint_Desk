# 22 · Calendar & Scheduling
> **Status:** Draft v1.0 · **Source:** MPD §5.17 · **Depends on:** 15, 17

## 1. Calendar items
| Item | Source | Tag |
|---|---|---|
| Due dates | `issues.due_date` | R |
| Deadlines/milestones | Epic or sprint end dates | R |
| Sprint dates | `sprints.start_date/end_date` | R |
| Project schedule | Project start/target end [RC fields] | RC |
| Events (custom) | User-created events | O |

## 2. Views
Month, week, agenda; filter by project, assignee, type; color by project; click item opens issue/sprint. Overdue items highlighted.

## 3. iCal feed
`/calendar.ics?token=` per-user random token (revocable). Read-only. Contains assigned issues with due dates and sprint dates for user's projects.

## 4. Rules
Workspace timezone for sprint boundaries, user timezone for display; only issues the user can view appear (policy-filtered).

## 5. Edge cases
Issue without due date (not shown); due date changes (feed updates on next poll); revoked token (404); large ranges (paginate/limit to ±90 days).
