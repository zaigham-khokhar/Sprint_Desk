# 26 · Security Requirements
> **Status:** Draft v1.0 · **Source:** MPD §13 · **Depends on:** 07, 12, 25 · **Tests:** 29, 30

| Area | Requirement | Tag |
|---|---|---|
| Authentication | Argon2id/bcrypt, min 12-char password, breach-list check [RC], login throttling, optional/enforced 2FA, session regeneration | R |
| Authorization | Deny-by-default policies on every action; permission resolver; tests for role matrix (doc 36) | R |
| RBAC | Workspace + project roles; last-owner protection | R |
| CSRF | Laravel CSRF tokens on all state-changing web requests; API tokens exempt but ability-scoped | R |
| XSS | Output escaping by default; rich text sanitized server-side (allow-list); CSP header; no `dangerouslySetInnerHTML` without sanitizer | R |
| SQL injection | Eloquent/query builder bindings only; raw SQL reviewed and parameterized | R |
| Mass assignment | Explicit `$fillable`/DTOs; never `$request->all()` into models | R |
| File uploads | See doc 27: type/size validation, random names, private storage, virus scan | R |
| Rate limiting | Login, password reset, invitations, API, search, uploads (A8 values) | R |
| API security | Token abilities, expiry, HTTPS only, versioned, no sensitive data in URLs | R |
| Session security | HttpOnly, Secure, SameSite=Lax, idle timeout, session listing/revocation | R |
| Password security | Hashed, never logged, reset invalidates sessions | R |
| Tenant isolation | Doc 07: global scopes, private channels, prefixed cache, signed file URLs | R |
| Audit logs | Doc 25 | R |
| Sensitive data | Secrets in env/secret manager; 2FA secret and tokens encrypted/hashed; PII minimal in logs; TLS 1.2+ | R |
| Headers | HSTS, X-Content-Type-Options, frame-ancestors, Referrer-Policy | R |
| Dependencies | Automated audit (`composer audit`, `npm audit`, Dependabot) in CI | R |
| Backups | Encrypted, tested restore | RC |
| Data export/erasure | Workspace export and user deletion process | RC |
| WAF / DDoS | At edge/CDN in production | RC |

## Threat model highlights
| Threat | Mitigation |
|---|---|
| Broken object-level authorization (IDOR) | Tenant scope + policies + tests |
| Account takeover | Throttling, 2FA, notifications on new login/2FA change |
| Malicious upload | Scan, isolated storage, no execution, download as attachment |
| Privilege escalation | Role-change requires `member.role_update`; audited |
| Token leakage | Hashed at rest, revocable, scoped |
| WebSocket eavesdropping | Private channel authorization |

## Security review checklist (pre-release)
Policy coverage report · cross-tenant test suite green · headers scan · dependency audit clean · secrets scan (CI) · upload abuse test · rate limit test.
