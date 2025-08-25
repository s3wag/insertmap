

## Goal:
Identify weak or missing enforcement of user-level and role-based permissions. These checks target both horizontal and vertical privilege escalation attempts.

---

## User ID & Object Reference Manipulation
- [ ] Directly modify `user_id`, `uid`, `id` in URL
- [ ] Tamper `account_id` or `customer_id` in query
- [ ] Change `order_id`, `invoice_id` in REST calls
- [ ] Manipulate object references in JSON body
- [ ] Replace own ID with sequential/random values
- [ ] Change reference in GraphQL variables
- [ ] IDOR via hidden fields (e.g., `<input type="hidden" name="userId">`)
- [ ] Modify path parameters (e.g., `/users/1` ➝ `/users/2`)
- [ ] Replace UUIDs with other valid-looking ones
- [ ] Guess short/numeric IDs in mobile APIs

---

## Role Escalation & Privilege Misuse
- [ ] Modify `role`, `isAdmin`, `group`, or `permissions` flags
- [ ] Remove or nullify role restrictions (`"role": ""`)
- [ ] Replace `user` with `admin` in API endpoint
- [ ] Abuse UI-exposed endpoints not checked server-side
- [ ] Replay admin-only actions as lower role
- [ ] Fuzz `X-User-Role`, `X-User-Level` headers
- [ ] Test endpoints hidden from the UI but callable directly
- [ ] Check for differences between `GET` and `POST` actions
- [ ] Bypass `readonly` role limits via unsupported methods
- [ ] Attempt internal role switching via GraphQL mutations

---

## Parameter-Based Bypass
- [ ] Add `?admin=true` or similar query strings
- [ ] Use `debug`, `test`, `internal`, `bypass=1` flags
- [ ] Try deprecated or undocumented parameters
- [ ] Replace `access=limited` with `access=full`
- [ ] Remove parameters to trigger default access
- [ ] Append additional hidden parameters
- [ ] Tamper multi-value inputs (e.g., `id[]=1&id[]=2`)
- [ ] Force unexpected values like `access=0/1`, `yes/no`
- [ ] Add conflicting parameters to test precedence
- [ ] Use null/undefined in place of auth-relevant values

---

## Header-Based Manipulation
- [ ] Manipulate `X-User-Id`, `X-Admin`, `X-Role` headers
- [ ] Add `X-Forwarded-User`, `X-Original-User`
- [ ] Test custom internal headers (via proxy detection)
- [ ] Use spoofed IPs in `X-Forwarded-For` header
- [ ] Override auth headers with duplicate values
- [ ] Add `Authorization: Bearer null`
- [ ] Test JWT tokens with altered payload
- [ ] Use expired JWTs and check enforcement
- [ ] Remove or tamper CSRF protection headers
- [ ] Send forged client certs in mutual TLS flows

---

## Logic & Workflow Bypass
- [ ] Replay token from a lower-privilege user
- [ ] Attempt unauthorized state transitions
- [ ] Inject hidden options in forms (e.g., `admin=1`)
- [ ] Abuse "preview" or "draft" endpoints
- [ ] Use OPTIONS method to probe CORS bypass
- [ ] Access endpoints via mobile API that skips checks
- [ ] Cancel → Commit transaction without permission
- [ ] Try “impersonation” endpoints (`/as_user`)
- [ ] Call endpoints in improper sequence (bypass checks)
- [ ] Intercept client validation and bypass using Burp/ZAP

---
