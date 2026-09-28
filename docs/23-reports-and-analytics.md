# 23 · Reports & Analytics
> **Status:** Draft v1.0 · **Source:** MPD §5.15 · **Depends on:** 08, 17, 21 · **Performance:** 28

## 1. Dashboard analytics
| Widget | Data |
|---|---|
| My open issues | By priority/due |
| Active sprint progress | Points done vs. committed |
| Workload | Open points per assignee |
| Recent activity | From audit feed |
| Overdue issues | Count and list |

## 2. Reports
| Report | Description | Audience | Tag |
|---|---|---|---|
| Project summary | Counts by status/type/priority, created vs. resolved trend | PM | R |
| Issue report | Filterable list with export CSV | PM | R |
| Sprint report | Committed vs. completed, carry-over, scope changes | PM/Team | R |
| Burndown | Ideal vs. actual remaining | Team | R |
| Velocity | Points completed per sprint, average | PM | R |
| Cumulative flow | Issues per status over time | PM | RC |
| Cycle/lead time | In-progress→done, created→done | PM | RC |
| Team/workload | Load per member/team | PM/Admin | R |
| Productivity | Resolved issues per user/period | PM/Admin | R |
| Time reports | Logged vs. estimated by user/project | PM/Admin | R |

## 3. Data & computation
Live queries for small aggregates; nightly `report_snapshots` for burndown/CFD; heavy results cached in Redis (5–15 min TTL). Reports run through `ReportRepository`, always tenant-scoped.

## 4. Filtering
Date range, project(s), sprint, assignee/team, issue type, label, epic. Filters persist in URL and can be saved.

## 5. Export
CSV for tabular reports; PDF **[O]**. Exports over 10 k rows run as queued job with email link.

## 6. Security & edge cases
Requires `report.view`; time data requires `time.view_all`. Edge: sprint with zero points (show empty state), deleted issues (excluded, counted in scope-change log), timezone day boundaries, missing snapshot days (interpolate and mark).
