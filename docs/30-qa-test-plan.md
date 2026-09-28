# 30 · QA Test Plan
> **Status:** Draft v1.0 · **Source:** MPD §14 · **Depends on:** 29, 36, 40

## 1. Strategy
Risk-based; automated where stable, exploratory manual for UX. Entry: build on staging with seed data. Exit: no open P0/P1 defects, checklist (doc 40) verified.

## 2. Test types
| Type | Scope |
|---|---|
| Functional | Each FR in doc 02 |
| UI | Layout, states, dark mode, accessibility (axe + manual keyboard) |
| API | Doc 11 contract, error codes |
| Security | Doc 26 checklist, OWASP ZAP baseline, IDOR attempts |
| Permission | Doc 36 matrix per role |
| Regression | Automated suite on every release |
| Performance | k6: 500 users, board/backlog/search/API mix |
| Browser | Chrome, Edge, Firefox, Safari (latest 2) |
| Mobile/responsive | 360, 768, 1024 widths; iOS Safari, Android Chrome |

## 3. Scenario catalogue (sample IDs)
| ID | Scenario | Expected |
|---|---|---|
| QA-AUTH-01 | Register, verify email, login | Access granted |
| QA-AUTH-02 | 6 wrong logins | Throttled 429 |
| QA-AUTH-03 | Reset password link reuse | Rejected |
| QA-WS-01 | Invite with expired token | Rejected with message |
| QA-WS-02 | Remove last Owner | Blocked |
| QA-PRJ-01 | Duplicate project key | 422 |
| QA-ISS-01 | Create issue, key NEX-n sequential under concurrent creates | No duplicates |
| QA-ISS-02 | Two users edit same issue | Second gets 409 |
| QA-BRD-01 | Invalid transition drag | Card reverts, message |
| QA-BRD-02 | Exceed WIP limit | Blocked/warned |
| QA-SPR-01 | Start second sprint on same board | Blocked |
| QA-SPR-02 | Complete sprint with unfinished issues | Prompt, moves correctly |
| QA-COM-01 | Mention member/non-member | Notify / ignore |
| QA-ATT-01 | Upload .exe / 30 MB / EICAR | Rejected / rejected / quarantined |
| QA-RT-01 | Move card in browser A | Browser B updates < 1 s |
| QA-TEN-01 | Access other workspace issue by ID | 404 |
| QA-TIM-01 | Start second timer | Prevented/switch prompt |
| QA-RPT-01 | Burndown matches manual calc | Match |
| QA-AUD-01 | Change assignee | Audit entry with diff |
| QA-A11Y-01 | Keyboard-only board move | Possible |

## 4. Defect handling
Severity P0 (data loss/security) … P3 (cosmetic); triage daily; regression test added per fix.

## 5. Sign-off
QA lead confirms: all P0 scenarios pass, matrix verified, performance budgets met, checklist signed.
