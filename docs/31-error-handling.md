# 31 · Error Handling
> **Status:** Draft v1.0 · **Source:** MPD §13 · **Depends on:** 09, 11 · **Logging:** 32

## 1. Error matrix
| Category | HTTP | Handling | User-facing message |
|---|---|---|---|
| Validation | 422 | Field errors returned; Inertia maps to fields | "Please fix the highlighted fields." |
| Authentication | 401 | Redirect to login (web) / JSON (API); session expiry preserves return URL | "Please sign in to continue." |
| Authorization | 403 | Forbidden page/toast | "You don't have permission to do this." |
| Not found / cross-tenant | 404 | Generic not-found page | "We couldn't find that." |
| Conflict | 409 | Version conflict, WIP limit, invalid transition; UI offers refresh/revert | "This item was changed by someone else." |
| Rate limit | 429 | `Retry-After` header | "Too many attempts. Try again in a minute." |
| Server | 500 | Logged with request ID; generic page | "Something went wrong. Reference: {id}" |
| Database | 500/503 | Deadlock retried (max 3) inside services; connection failure → 503 | Same as server |
| File | 422/415/413 | Type, size, scan failures; infected quarantined | "This file type/size isn't allowed." |
| Real-time | – | Reconnect with backoff; banner; resync on reconnect | "Reconnecting…" |
| Queue | – | Retries with backoff; `failed_jobs`; alert | (not shown) |

## 2. Rules
1. Domain exceptions (doc 09) map centrally in the exception handler; no try/catch swallowing.
2. Never expose stack traces, SQL or internal IDs in production.
3. API errors use the envelope in doc 11 with stable `code`.
4. Every error response carries `X-Request-ID`.
5. Transactions roll back on exception; events dispatched after commit.
6. Frontend: error boundaries per section; mutation errors as toasts; forms show inline.

## 3. Logging strategy
| Level | Use |
|---|---|
| debug | Local only |
| info | Business events (sprint started) |
| warning | Recoverable (retry, throttled) |
| error | Failed requests/jobs → Sentry |
| critical | Data integrity, security → alert |
Structured JSON with request ID, user ID, workspace ID; no secrets/PII bodies. Retention 30 days hot, 12 months cold [A8].
