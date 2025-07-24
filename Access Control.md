
##  Goal:
Test insertion points where an attacker may access unauthorized resources or perform actions beyond their privileges due to flawed authorization logic or weak enforcement.

---

##  Role/Privilege Manipulation
- [ ] Modify `role=admin` in cookies, headers, or body
- [ ] Change `isAdmin=false` ➝ `isAdmin=true` in request
- [ ] Manipulate `group=user` ➝ `group=superadmin`
- [ ] Insert `access_level=99` in JSON/XML
- [ ] Replay request from higher-privileged user
- [ ] Downgrade or upgrade privileges via `PUT` or `PATCH`
- [ ] Send `X-User-Role: admin` or similar custom headers
- [ ] Modify JWT payload to elevate role
- [ ] Override ACLs using predictable numeric values (`access=1`)
- [ ] Test various `user_type`, `account_type`, `profile_type` variations

---

## IDOR (Insecure Direct Object Reference)
- [ ] Replace `user_id=123` with another user ID
- [ ] Access `/users/1234/profile` as an unauthorized user
- [ ] Guess and access `/invoices/2022-04-01.pdf`
- [ ] Access `/admin/config.json` or `/user/0/settings`
- [ ] Tamper with file download paths using ID values
- [ ] API-based IDOR via `/api/v1/user/123/details`
- [ ] Change `email=attacker@example.com` ➝ victim's email
- [ ] Refer another user's reference code or account number
- [ ] Mobile app APIs referencing user ID in plain text
- [ ] Access S3/cloud bucket URLs with guessable filenames

---

## API Endpoint Access Control Gaps
- [ ] Access `/admin/` or `/internal/` endpoints unauthenticated
- [ ] Call `DELETE /users/123` as a normal user
- [ ] Access `PUT /order/123/approve` as a guest
- [ ] Test legacy APIs like `/v1/` or `/beta/` with weak auth
- [ ] Access management APIs from different roles
- [ ] Use HTTP verbs (`OPTIONS`, `PUT`, `PATCH`) not blocked by WAF
- [ ] Tamper GraphQL queries to access other users’ data
- [ ] Perform `bulkUpdate` operations meant for admins
- [ ] Trigger backend-only actions from frontend context
- [ ] Access private API keys via misconfigured endpoints

---

## File, Functionality, and Method Access
- [ ] Access `/.git/config`, `/env`, `/config.yaml`
- [ ] Try static JS files for hidden admin endpoints
- [ ] Trigger `export`, `report`, or `sync` actions from UI
- [ ] Call internal-only HTTP methods (e.g., `MOVE`, `COPY`)
- [ ] Use HTTP method override headers (`X-HTTP-Method-Override`)
- [ ] Call hidden API routes not exposed in frontend
- [ ] Check service workers for offline cached protected data
- [ ] Try functionality toggles via `?admin=true`
- [ ] Upload arbitrary file and call the download URL directly
- [ ] Run webhooks meant for internal usage

---

## Misc Authorization Bypass Techniques
- [ ] Bypass using `X-Original-URL`, `X-Forwarded-Host`
- [ ] Modify `Referer` or `Origin` headers to internal hosts
- [ ] Test using lower-privileged OAuth scopes
- [ ] Spoof source IP headers (`X-Forwarded-For: 127.0.0.1`)
- [ ] Switch HTTP protocol versions (e.g., HTTP/1.1 vs 2.0)
- [ ] Replay `Authorization` token from other user
- [ ] Switch between `mobile`, `admin`, and `internal` subdomains
- [ ] Invoke shadow/internal GraphQL mutations
- [ ] Reuse URLs or links shared in emails (forgot password, invite)
- [ ] Race condition between state change and access control
