

> Use this checklist to identify weak JWT configurations, insecure token handling, and logic abuse vectors across headers, payloads, and signature validations.

##  Where to Look for JWTs
- [ ] `Authorization: Bearer <JWT>` (header)
- [ ] `Cookie: jwt=<token>`
- [ ] `access_token`, `id_token`, `auth_token` in JSON response
- [ ] In query parameters: `?token=`, `?jwt=`, `?auth=`
- [ ] Web storage: `localStorage`, `sessionStorage`
- [ ] JavaScript variables: exposed in frontend apps
- [ ] Mobile apps (hardcoded or stored in shared prefs)

##  Payload Injection Points
- [ ] `sub` – test for IDOR (`"sub": "1"` to `"sub": "2"`)
- [ ] `role` – escalate privileges (`"role": "admin"`)
- [ ] `isAdmin`, `isSuperuser` → Boolean tampering
- [ ] `user_id`, `email`, `username`
- [ ] `exp`, `nbf`, `iat` – time manipulation
- [ ] `aud`, `iss` – bypass audience validation
- [ ] `scope`, `permissions` – broaden access
- [ ] `alg`, `typ` header parameters
- [ ] Extra fields – test if server parses them (`debug=true`)

##  Header Manipulation
- [ ] `alg: none` attack (if server skips validation)
- [ ] `alg: HS256` + public key as HMAC key
- [ ] Swap `RS256` ↔ `HS256`
- [ ] Tamper `kid` field to use arbitrary keys
- [ ] `typ: jwt` → test other types (e.g., `application/xml`)
- [ ] Add duplicate headers → test parsing logic

## 🔁 Token Handling Logic
- [ ] Replay old tokens (expired reuse)
- [ ] JWT rotation failures
- [ ] Refresh token logic
- [ ] Static JWT with no expiry (`"exp"` missing)
- [ ] Same JWT reused across roles or users

## Weak Signature Testing
- [ ] No signature (unsigned JWT)
- [ ] Using public/private key as HMAC secret
- [ ] Empty signature (`a.b.`)
- [ ] Brute force HS256 using rockyou.txt (hashcat mode 16500)
- [ ] `kid` injection to load local/public files

## Cryptographic Abuse
- [ ] Weak key length (e.g., 32-bit secret)
- [ ] Known/default secrets (`admin`, `1234`, `secret`)
- [ ] Predictable `iat` or `jti` for brute-forcing tokens
- [ ] Algorithm confusion attacks (RS/HS swap)
- [ ] JWT encrypted with JWE (leak possibility)

## Client-Side Token Logic
- [ ] JWT stored in `localStorage` (XSS risk)
- [ ] JWT passed in URL (leak in referrer logs)
- [ ] JWT in browser memory → check JS variables
- [ ] Forced logout doesn’t invalidate token
- [ ] JWT regeneration on every request

## Authentication & Authorization Abuse
- [ ] Use JWT from another user → IDOR
- [ ] Modify JWT claims to escalate privilege
- [ ] Misconfigured token verification (e.g., no `aud` check)
- [ ] JWT accepted by multiple services (shared keys)
- [ ] Inconsistent JWT parsing libraries (server vs gateway)

## Miscellaneous Attack Surfaces
- [ ] Log injection (`\n` in token leaks logs)
- [ ] JWT used in CORS preflight responses
- [ ] JWT reflected in error/debug messages
- [ ] Tokens not revoked on password change
- [ ] Malformed JWTs not rejected
- [ ] Mix of signed and unsigned tokens accepted