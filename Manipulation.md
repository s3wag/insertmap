
## 🎯 Goal:
Identify places where an attacker can tamper with server responses to:
- Inject/alter client-side behavior
- Influence headers, content, status codes
- Trick frontend logic or users

---

## HTTP Header Manipulation
- [ ] `X-Forwarded-Host` influencing redirects
- [ ] `X-Original-URL` used to rewrite responses
- [ ] `X-Host`, `X-Real-IP` affecting backend logic
- [ ] `Origin`/`Referer` header influencing CORS or redirects
- [ ] `Range` header used for partial content abuse
- [ ] `Accept` or `Accept-Encoding` influencing SSRF or caching
- [ ] `X-Content-Type-Options` missing or misused
- [ ] `Content-Security-Policy` can be disabled/relaxed
- [ ] `Access-Control-Allow-Origin` reflects input
- [ ] `X-Frame-Options` absent or manipulable

---

## Reflected User-Controlled Data
- [ ] User input reflected in response body (e.g. `?message=hello`)
- [ ] Input reflected in JSON responses
- [ ] Reflected URL fragments used in UI
- [ ] Reflected filenames or URLs in download responses
- [ ] `Location:` header includes user input
- [ ] Custom headers like `X-User-Message: {user input}`
- [ ] Reflected error messages exposing stack traces
- [ ] HTML comment injection (`<!--user_input-->`)
- [ ] `Set-Cookie` value influenced by user input
- [ ] Reflecting metadata (e.g., in XML, JSON-LD, headers)

---

## Response Code & Redirection Manipulation
- [ ] Manipulate status code (e.g. 302 instead of 403)
- [ ] Trigger redirect using open redirect logic
- [ ] Abuse 301/302 to cache poisoned locations
- [ ] Switch between 200 OK vs 204 No Content
- [ ] Force upgrade/downgrade responses (e.g., HTTPS ➝ HTTP)
- [ ] Tamper with `Refresh:` header
- [ ] Exploit inconsistent caching headers (`ETag`, `Last-Modified`)
- [ ] Bypass logic based on incorrect HTTP response code
- [ ] Control redirect location by parameter tampering
- [ ] Inject URL in redirection chain via query parameters

---

## Cache Poisoning / CDN Injection
- [ ] Poison response with unkeyed header injection
- [ ] Cache JSON with reflected payload
- [ ] Abuse `Vary:` headers for cache splitting
- [ ] Use `X-Forwarded-*` to split cache entries
- [ ] Force CDN to cache sensitive user data
- [ ] Use internal redirect (e.g., `/internal`) to leak info
- [ ] Force private data to be cached as public
- [ ] Force cache TTL using `Cache-Control: max-age`
- [ ] Tamper `Host:` header to poison absolute URLs in responses
- [ ] Force caching of invalid responses (403, 500)

---

## Functional & Behavioral Manipulation
- [ ] Manipulate API response used by frontend logic
- [ ] Manipulate response metadata to alter client decision
- [ ] Inject `Content-Disposition: inline; filename=evil.html`
- [ ] Force application into maintenance/debug mode
- [ ] Tamper JSON/HTML/XML output fields (`isAdmin`, `auth`)
- [ ] Strip CSP headers for JS injection via proxy
- [ ] Inject alternate MIME types (`Content-Type: application/x-sh`)
- [ ] Cause unexpected behavior using Unicode or null bytes in response
- [ ] Use header injection to break downstream parsing
- [ ] Poison `<meta http-equiv>` via reflected content

---
