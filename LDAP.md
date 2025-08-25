

> Use this checklist to identify locations where unsanitized user input might be directly used in LDAP queries, leading to data exposure, authentication bypass, privilege escalation, or enumeration.

---

## Common Input Points for LDAP Injection
- [ ] `username` (login forms)
- [ ] `password` (combined filter injection)
- [ ] `email`
- [ ] `uid`
- [ ] `cn` (common name)
- [ ] `ou` (organizational unit)
- [ ] `sn` (surname)
- [ ] `givenName`
- [ ] `displayName`
- [ ] `userPrincipalName`
- [ ] `accountName`
- [ ] `employeeNumber`
- [ ] `mobile`
- [ ] `phone`
- [ ] `location`
- [ ] `address`
- [ ] `department`
- [ ] `group`
- [ ] `search` (directory search bar)
- [ ] `filter` (admin LDAP tools)
- [ ] `q` or `query` parameters
- [ ] Hidden parameters (like `lookupKey`)
- [ ] JSON body fields (`username`, `search`, `targetUser`, etc.)
- [ ] XML/LDAP binding fields
- [ ] Headers like `X-User` or `X-LDAP-Filter`

---

## Bypass Patterns to Try
- [ ] `*)(uid=*))(|(uid=*`
- [ ] `*)(objectClass=*))(|(objectClass=*`
- [ ] `*)(|(password=*))`
- [ ] `*` wildcard for bruteforcing
- [ ] `admin*)(uid=*))(|(uid=*`
- [ ] `*)(cn=*))(|(cn=*`
- [ ] Null byte terminator `%00`
- [ ] URL-encoded wildcards (`%2a`)
- [ ] Use newline/tab characters
- [ ] Filter injection via logic: `)(uid=admin`
- [ ] Escaping attempts like: `\2a`, `\28`, `\29`

---

## Authentication Bypass Cases
- [ ] Login page accepts wildcard username: `*`
- [ ] Filter like: `(&(uid=<input>)(password=<input>))` → test for logic injection
- [ ] Bypass with: `admin)(|(password=*))`
- [ ] Test `anonymous login` with wildcard injection
- [ ] Use base64 injection in encoded filters
- [ ] Username filter override: `*)(uid=admin`
- [ ] Login accepts blank password with injected filter

---

## Enumeration Test Cases
- [ ] Use filters to extract multiple entries
- [ ] Inject to list all usernames via wildcard
- [ ] Test `ou=*`, `objectClass=*` in search endpoints
- [ ] Use time-based enumeration logic if no output shown
- [ ] LDAP injection in error messages (e.g., invalid DN)
- [ ] Bruteforce valid users via filter logic

---

## Application-Level Logic Abuse
- [ ] Admin panel user search filter injection
- [ ] Inject into RBAC filters
- [ ] Modify access filters to elevate privileges
- [ ] Filter bypass in profile editing
- [ ] LDAP injection in HR portals or employee directories
- [ ] Bypass account-locking mechanisms via crafted filters
- [ ] Nested filters: inject inner `(&())` logic

---

## Code & Config Issues
- [ ] App uses string concatenation to build filters
- [ ] No escaping or sanitization of input
- [ ] Reuses the same filter for multiple roles
- [ ] LDAP filter logic visible in logs
- [ ] Hardcoded filters vulnerable to override
- [ ] LDAP filter built from client-controlled data
- [ ] Application uses `searchScope: subtree` allowing deep traversal
- [ ] LDAP attribute injection into non-LDAP fields

---

## Other LDAP Contexts to Test
- [ ] Java’s `InitialDirContext` usage
- [ ] Spring LDAP configurations
- [ ] PHP’s `ldap_search()` and `ldap_bind()`
- [ ] LDAP filters built via XML config
- [ ] REST APIs that call internal LDAP
- [ ] Mobile apps sending LDAP requests over HTTP/SOAP
- [ ] GraphQL-to-LDAP integration (common in enterprise portals)