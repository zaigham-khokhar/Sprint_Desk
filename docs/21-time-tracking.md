# 21 · Time Tracking
> **Status:** Draft v1.0 · **Source:** MPD §5.16 · **Depends on:** 05, 15 · **Reports:** 23

## 1. Features
| Feature | Requirement | Tag |
|---|---|---|
| Timer | Start/stop on an issue; one running timer per user (BR-TIM-01) | R |
| Manual entry | Date, duration or start/end, note | R |
| Estimated time | `estimate_minutes` (and/or points) on issue | R |
| Logged time | Sum of entries; shown vs. estimate | R |
| Timesheets | Weekly per-user grid, editable until locked | R |
| Timesheet lock | PM/Admin locks a period | RC |
| Time reports | By user, issue, project, sprint, label | R |

## 2. Backend logic
Start: reject if a timer is running (or offer to switch). Stop: compute minutes, create entry. Scheduled `StopStaleTimers` closes timers older than 12 h and notifies the user. Entries cannot overlap for a user (BR-TIM-02).

## 3. Frontend
Global timer widget in header; issue "Log time" panel; weekly timesheet grid with inline edit.

## 4. Data / API / Security
Table: time_entries. Endpoints: `/time/start`, `/time/stop`, `/time-entries`. Permissions: `time.log` (own entries), `time.view_all` (PM and above). Viewers see no time data.

## 5. Edge cases
Timezone changes (store UTC, display in user tz); issue moved/deleted (entries kept, reassigned with issue); user removed (entries retained for reporting); DST boundaries; edits to locked period (denied, audited).
