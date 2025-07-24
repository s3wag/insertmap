# Authentication Bypass

##  Goal:
Identify and test all potential insertion points where authentication mechanisms may be bypassed due to misconfigurations, flawed logic, insecure token handling, or parameter tampering.

---

## Token-Based Authentication
- [ ] `Authorization: Bearer <user-input>` — Replace with random/expired tokens
- [ ] JWT payload tampering: change `alg`, `sub`, `role`, `exp`
- [ ] `access_token` in URL: `?access_token=...`
- [ ] `X-API-Key` header (try null/invalid/old keys)
- [ ] Token reuse across different users or sessions
- [ ] JWT without signature verification (`alg=none`)
- [ ] Changing JWT `kid` to path traversal or pointing to public file
- [ ] Replay of tokens issued to other roles (e.g. `refresh_token`)
- [ ] Leaked token reuse in Authorization or Cookie
- [ ] Access using expired token or invalid `iat`/`exp`

---

## Session-Based Auth Weakness
- [ ] `Set-Cookie: session=...` — reuse or brute force old session tokens
- [ ] Missing `HttpOnly` or `Secure` flags in auth cookies
- [ ] Tampering with `userid`, `username`, or `role` in cookie value
- [ ] Session fixation via predefined `session_id`
- [ ] Cookie used from different user agent/IP
- [ ] Session not invalidated after logout or password change
- [ ] Session cookie guessable or sequential
- [ ] Multiple cookies accepted — test injection (`Cookie: user=admin; user=guest`)
- [ ] Downgrade of session (e.g. from MFA to single factor)
- [ ] Lack of CSRF protection allowing session riding

---

## Bypassing Login Logic
- [ ] `email=admin@example.com&password=admin` — test weak creds
- [ ] Bypass with SQLi: `' OR 1=1--`
- [ ] Logic-based bypass using `username=admin&password[0]=a`
- [ ] Overriding fields like `isAdmin=true` or `role=admin`
- [ ] Brute-force endpoints without rate limiting or lockout
- [ ] Login using `X-Original-URL`, `X-Forwarded-For`, etc.
- [ ] Login using only user ID (no password required)
- [ ] Forgotten password endpoints with insecure token verification
- [ ] Login bypass via API versioning (`/api/v1/login`)
- [ ] POST-to-GET login endpoint confusion

---

## Hidden or Forgotten Endpoints
- [ ] `/admin` or `/admin/login` — hidden login panel
- [ ] `/debug`, `/dev-login`, `/api/dev-auth`
- [ ] `/login-as?user=123` for impersonation
- [ ] `/bypass-auth?token=guest123`
- [ ] Unprotected `/graphql` or `/introspect`
- [ ] `/api/users/me` responds without authentication
- [ ] `/actuator`, `/health`, `/metrics` exposing user data
- [ ] `/reset-password` token not verified
- [ ] `GET /config.json` leaking admin credentials
- [ ] `OPTIONS` method responding with unexpected access

---

## Misc Exploitable Vectors
- [ ] Bypass via `X-Original-URL` header (reverse proxy misconfig)
- [ ] Tampering with `Referer` or `Origin` headers
- [ ] `X-Forwarded-For: 127.0.0.1` for IP-based auth bypass
- [ ] Caching token responses (reusing token of other users)
- [ ] OAuth flow skipping token exchange step
- [ ] Access tokens not scoped or validated (`scope: *`)
- [ ] SSO bypass via unvalidated email domain in ID token
- [ ] Forgotten test user still valid (`test:test`)
- [ ] Pre-auth endpoints calling internal protected APIs
- [ ] Lack of user verification in 2FA or login flows

---
