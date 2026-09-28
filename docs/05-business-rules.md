# 05 · Business Rules
> **Status:** Draft v1.0 · **Source:** MPD §5 · **Depends on:** 02, 04 · Rules are referenced as `BR-…` elsewhere.

## Organization (Workspace) rules
| ID | Rule |
|---|---|
| BR-ORG-01 | Workspace slug is globally unique. |
| BR-ORG-02 | Creator becomes Owner; a workspace always has ≥ 1 Owner. |
| BR-ORG-03 | Invitations expire (default 7 days, A8), are single-use, and bound to the invited email. |
| BR-ORG-04 | Removing a member unassigns nothing automatically; their open issues are flagged "unassigned owner" for the PM. |
| BR-ORG-05 | Users may belong to multiple workspaces with independent roles. |

## Project rules
| ID | Rule |
|---|---|
| BR-PRJ-01 | Project key is 2–10 uppercase letters, unique per workspace, immutable after first issue. |
| BR-PRJ-02 | Every project has a lead who must be a project member. |
| BR-PRJ-03 | Creating a project seeds a default workflow and issue types. |
| BR-PRJ-04 | Archived projects are read-only; issues cannot be created or moved. |
| BR-PRJ-05 | Archiving with an active sprint requires completing the sprint first. |

## Issue rules
| ID | Rule |
|---|---|
| BR-ISS-01 | Issue number is sequential per project, allocated in a transaction with row lock; never reused. |
| BR-ISS-02 | Title required (≤ 255 chars); description sanitized. |
| BR-ISS-03 | Assignee must be a project member. |
| BR-ISS-04 | Subtasks are one level deep; a subtask cannot have subtasks. |
| BR-ISS-05 | A parent cannot move to a *done* status while subtasks are open (configurable per project). |
| BR-ISS-06 | Epics cannot be nested; deleting an epic un-parents its children. |
| BR-ISS-07 | Concurrent edits use `version`; stale writes return 409. |
| BR-ISS-08 | Deletion is soft; restore is possible by Admin within 30 days [RC]. |

## Workflow rules
| ID | Rule |
|---|---|
| BR-WFL-01 | Status changes must follow an allowed transition. |
| BR-WFL-02 | A transition may require a field (e.g. resolution). |
| BR-WFL-03 | A status cannot be deleted while issues use it; issues must be migrated first. |
| BR-WFL-04 | A column with a WIP limit blocks moves that exceed it unless the user has `workflow.manage` (soft warning configurable). |

## Sprint rules
| ID | Rule |
|---|---|
| BR-SPR-01 | States: planned → active → completed; no reverse. |
| BR-SPR-02 | One active sprint per board. |
| BR-SPR-03 | Start requires start/end dates, end > start, and ≥ 1 issue (warning if empty). |
| BR-SPR-04 | Starting snapshots committed points. |
| BR-SPR-05 | Scope changes after start are allowed and logged. |
| BR-SPR-06 | Completing prompts to move unfinished issues to backlog or next sprint. |
| BR-SPR-07 | Sprint dates of the same board cannot overlap. |

## Notification rules
| ID | Rule |
|---|---|
| BR-NTF-01 | Users never notify themselves about their own actions. |
| BR-NTF-02 | Duplicate notifications of the same type/subject within 60 s are merged. |
| BR-NTF-03 | User preferences are respected per event type and channel; security emails cannot be disabled. |
| BR-NTF-04 | Mentions of non-members are ignored. |

## Permission, time, file rules
| ID | Rule |
|---|---|
| BR-PRM-01 | Every action passes a policy check; deny by default. |
| BR-PRM-02 | Project role overrides workspace role only within that project. |
| BR-TIM-01 | One running timer per user; auto-stopped after 12 h. |
| BR-TIM-02 | Entries cannot overlap for one user [RC]. |
| BR-FIL-01 | Max attachment size 25 MB; allowed types whitelisted (doc 27). |
| BR-FIL-02 | Files are unavailable until virus scan passes. |
| BR-AUD-01 | Audit records are immutable. |

## Validation rules (summary)
Email valid and unique per user; password ≥ 12 chars, checked against breach list [RC]; due date cannot precede creation date; estimates non-negative; label ≤ 30 chars. See doc 31 for messages.
