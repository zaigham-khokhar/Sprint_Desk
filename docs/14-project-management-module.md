# 14 · Project Management Module
> **Status:** Draft v1.0 · **Source:** MPD §5.1 · **Depends on:** 04, 05, 08 · **Related:** 15, 16, 18

## 1. Purpose
Scope work into projects with an owner, workflow and team.

## 2. Requirements
| Area | Requirement | Tag |
|---|---|---|
| Creation | Name, key, description, lead, template (Scrum/Kanban), visibility | R (visibility RC) |
| Settings | Name, description, lead, workflow, issue types, labels, archive | R |
| Members | Add/remove users with project role | R |
| Project roles | Project Manager, Developer, Viewer; overrides workspace role in project | R |
| Workflows | Statuses + transitions (doc 16) | R |
| Status | Active, Archived (read-only) | R |
| Visibility | `private` (members only) or `workspace` (all members read) | RC |
| Dashboard | Active sprint, issue counts by status/type, recent activity, my issues | R |
| Activity | Project-level feed from activity logs | R |

## 3. Backend logic
`ProjectService::create` → validate unique key → create project → seed workflow/statuses/transitions → add creator + lead as members → dispatch `ProjectCreated` (audit).

## 4. Frontend
Project list with search/filter, create modal (key auto-suggested from name), settings tabs, member picker.

## 5. Data / API / Security
Tables: projects, project_members, workflows (doc 08). Endpoints: doc 11 Projects. Permissions: `project.*`, `workflow.manage`, `project.member_manage`.

## 6. Edge cases
Duplicate key; changing lead to non-member (auto-add prompt); removing a member with assigned issues (reassign prompt); archiving with active sprint (blocked, BR-PRJ-05); key change after issues exist (blocked, BR-PRJ-01).
