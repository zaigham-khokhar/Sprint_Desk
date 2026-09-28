# 29 · Testing Strategy
> **Status:** Draft v1.0 · **Source:** MPD §14 · **Depends on:** 02, 09, 10 · **QA plan:** 30

## 1. Pyramid & tooling
| Level | Tool | Focus | Target |
|---|---|---|---|
| Unit | Pest/PHPUnit | Services, ranking, workflow transitions, permission resolver | Fast, no DB where possible |
| Feature | Pest | HTTP flows, validation, policies, events/queues faked | Every endpoint |
| API | Pest JSON assertions + OpenAPI contract check | Status codes, shapes, errors, pagination | All `/api/v1` |
| Authentication | Pest | Register, login, throttle, reset, 2FA, sessions | 100 % of flows |
| Authorization | Pest datasets | Role × action matrix from doc 36 | Full matrix |
| Multi-tenant | Pest | Cross-tenant read/write/delete attempts via web, API, broadcast, files, search | Every tenant model |
| Integration | Pest + real MySQL/Redis in CI | Events → listeners → jobs → notifications; file upload with fake storage | Key workflows |
| Frontend | Vitest + Testing Library | Components, hooks, forms | Critical components |
| E2E | Playwright | Register → create issue → drag on board; two-browser real-time; sprint flow | Top workflows |

## 2. Rules
- Factories for every model; seeded demo workspace (Nexora) for E2E.
- Backend coverage ≥ 80 %; changed lines ≥ 90 % (CI check).
- Tests run in parallel; database refreshed per test (transactions).
- Flaky tests quarantined within one day.
- Every bug fix adds a regression test.

## 3. Test data
Workspaces: Nexora Logistics, Orbit Studio (isolation tests). Users per role in each. Project `NEX` with 200 issues, 3 sprints.

## 4. CI gates
Lint → static analysis → unit/feature → frontend tests → E2E (on main/PR label). Merge blocked on failure (doc 33).
