
## Systematic testing of injection-prone parameters and behaviors

---

## URL & Query Parameters
- [ ] ID parameters (e.g., `/user?id=1`)
- [ ] Numeric values in search queries (`/search?price=100`)
- [ ] String parameters (e.g., `/profile?username=admin`)
- [ ] Category or tag filters (`/products?cat=electronics`)
- [ ] Pagination offsets (`/page?page=2`)
- [ ] Sort parameters (`/sort=asc` / `desc`)
- [ ] Boolean toggles (`?active=true`)
- [ ] Nested or array-like parameters (`user[role]=admin`)
- [ ] JSON key-value strings in GET parameters
- [ ] Language or locale parameters (`lang=en`)

---

## Authentication & Authorization
- [ ] Login username field
- [ ] Login password field
- [ ] Hidden login fields (e.g., token, redirect)
- [ ] Signup form fields (email, username)
- [ ] "Forgot password" email field
- [ ] Password reset token verification
- [ ] MFA/OTP code inputs
- [ ] Session/token revocation endpoints
- [ ] OAuth callback parameters (e.g., `code=`, `state=`)
- [ ] SSO token and email claims (for federated logins)

---

## POST Body Injection Points
- [ ] JSON body values (`{"user":"admin"}`)
- [ ] Nested JSON objects (`{"user":{"id":"1"}}`)
- [ ] Array JSON payloads (`[{"id":"1"}]`)
- [ ] Form-data field values (`application/x-www-form-urlencoded`)
- [ ] Hidden form fields (`<input type="hidden" value="123">`)
- [ ] User profile update fields (first name, last name, bio)
- [ ] File upload metadata (filename, MIME type)
- [ ] Feedback or contact form inputs
- [ ] Mobile API POST data (especially in Flutter/ReactNative apps)
- [ ] GraphQL query variables (`{ id: "1" }`)

---

## HTTP Headers (31–40)
- [ ] `X-User-ID` or custom user headers
- [ ] `X-Forwarded-For` (when used internally)
- [ ] `Referer` (if used in SQL logs/audit)
- [ ] `User-Agent` (in logging/auditing SQL queries)
- [ ] `X-Real-IP` (used in access control logic)
- [ ] `Host` header (if stored or verified in DB)
- [ ] `Authorization` header (JWT or token value)
- [ ] `Cookie` values (auth/session/user IDs)
- [ ] `X-Custom-Token` headers
- [ ] `Origin` or `Client-IP` headers

---

## Navigation, Search, and Filtering
- [ ] Search boxes (text search, site search, product search)
- [ ] Filter inputs (price, rating, location)
- [ ] Autocomplete inputs (AJAX/JS-based)
- [ ] Data export inputs (CSV, Excel)
- [ ] Report generation inputs (e.g., analytics ranges)
- [ ] Tag/label selection
- [ ] Navigation paths like `/product/view/123`
- [ ] Breadcrumbs or breadcrumbs data in DB
- [ ] URL slug fields (`/blog/my-post-title`)
- [ ] Referring user/campaign IDs (`?ref=12345`)

---

## Bonus: Testing Patterns
- [ ] Confirm presence of SQLi via time-based payloads (`SLEEP()`, `pg_sleep()`)
- [ ] Test with `' or 1=1--`, `'||'a'='a`
- [ ] Use logical tests (`' and 1=2 --`, `' and 1=1 --`)
- [ ] Observe errors (DB-specific error messages, stack traces)
- [ ] Blind SQLi techniques via response difference

---

## Notes:
- Always test with multiple payloads across DBMS (MySQL, PostgreSQL, Oracle, MSSQL)
- Combine with automated tools (e.g., `sqlmap`) for validation after manual discovery
- Use Burp Suite's Repeater/Intruder to test headers and JSON bodies
- Record insertion point observations for reuse during recon/automation

---
