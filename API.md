
##  Goal:
Identify common API endpoints and data points where attacker-controlled input can lead to vulnerabilities such as auth bypass, BOLA, mass assignment, IDOR, SSRF, injection, and misconfigurations.

---

## Authentication / Authorization Issues
- [ ] `Authorization: Bearer <user-controlled>` header
- [ ] `X-API-Key` header from public/front-end client
- [ ] Token included in query string: `?token=abc123`
- [ ] OTP or 2FA code submission endpoints
- [ ] Device registration endpoints: `/api/device/register`
- [ ] Login endpoints accepting only user ID (no password)
- [ ] Publicly exposed introspection endpoints (`/me`, `/validate-token`)
- [ ] Password reset token validation endpoint
- [ ] Access-control bypass via method spoofing (`X-HTTP-Method-Override`)
- [ ] Missing `scope` validation in OAuth token exchange

---

## BOLA / IDOR (Broken Object Level Auth)
- [ ] Path parameter injection: `/api/users/{userId}`
- [ ] Resource-based access: `/orders/{orderId}`, `/invoices/{invoiceId}`
- [ ] Changing `account_id` or `user_id` in body or query
- [ ] Replacing object references in PATCH/PUT/DELETE requests
- [ ] Accessing `GET /files/{filename}` or `/documents/{docId}`
- [ ] GraphQL: Querying objects by ID directly `{ user(id: 5) }`
- [ ] Bypassing RBAC with elevated `role=admin` in body
- [ ] Modifying nested objects in JSON (e.g., `"owner":{"id":2}`)
- [ ] Using predictable sequential resource IDs
- [ ] Caching leaks due to resource-based URLs

---

## Mass Assignment / Overposting
- [ ] Extra fields in POST/PUT/PATCH JSON body
- [ ] Sending `is_admin`, `role`, `access_level` in user registration
- [ ] Modifying server-controlled flags: `"verified": true`
- [ ] `user_id`, `tenant_id`, `company_id` fields in nested JSON
- [ ] GraphQL mutation abusing nested input: `{ updateUser(input: { admin: true }) }`
- [ ] Bypassing frontend-restricted fields with direct API call
- [ ] Ignored field names reused for privilege escalation
- [ ] Modifying soft-deleted records via undeclared fields
- [ ] Input fields not whitelisted by backend serializer
- [ ] Supplying foreign keys not authorized to user

---

## Injection Points (SQLi, NoSQLi, CMDi)
- [ ] Filter/search parameters: `?filter=name`, `?search=query`
- [ ] POST body fields passed directly to queries
- [ ] Sort/order fields (`?sort=id`, `?order=asc`)
- [ ] GraphQL filter injection: `{ users(where: {name_contains: "..."}) }`
- [ ] gRPC Protobuf fields deserialized insecurely
- [ ] Query builders taking raw user input (like Sequelize or Mongoose)
- [ ] Headers processed dynamically: `X-User-ID`, `X-Forwarded-For`
- [ ] Unescaped input used in dynamic routing
- [ ] Fields that control database queries like `column`, `table`, etc.
- [ ] API gateway parsing input for backend SQL query strings

---

## SSRF / External Interaction Vectors
- [ ] `url=` parameter in query or body for import/upload
- [ ] File fetchers or renderers accepting external URLs
- [ ] GraphQL with URL input: `{ fetch(url: "http://...") }`
- [ ] Image preview/render endpoints (`/api/preview?src=http...`)
- [ ] PDF or file generation services with external input

---

## Miscellaneous API-Specific Vectors
- [ ] API versioning path: `/v1/`, `/v2/` — unauthenticated legacy endpoints
- [ ] Rate limit testing: brute-forcing through `/api/login`
- [ ] Content-Type abuse: `Content-Type: text/xml`, `multipart/form-data`
- [ ] Method confusion via CORS preflight bypass (`OPTIONS`, `PUT`, etc.)
- [ ] Unfiltered object expansion (`include=comments.user.profile`)

---

## Payload Examples
- [ ] `/api/users/1337` → modify to test IDOR
- [ ] `{"admin":true,"role":"superadmin"}` → mass assignment
- [ ] `?filter=1'--` → SQLi
- [ ] `url=http://127.0.0.1:8080` → SSRF
- [ ] `Authorization: Bearer malformed.jwt.token` → token parsing issues

---
