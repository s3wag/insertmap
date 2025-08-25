
## Missing or Misconfigured Security Headers
- [ ] Missing `X-Content-Type-Options: nosniff`
- [ ] Missing or weak `Content-Security-Policy`
- [ ] Missing `Strict-Transport-Security` (HSTS)
- [ ] Missing or insecure `X-Frame-Options`
- [ ] Missing or weak `Referrer-Policy`
- [ ] Missing `Permissions-Policy` (e.g., to restrict camera/mic access)
- [ ] Missing `Cache-Control` or `Pragma: no-cache` for sensitive pages
- [ ] Insecure or overly permissive `Access-Control-Allow-Origin`
- [ ] Missing `X-XSS-Protection` (for older browsers)
- [ ] Missing or inconsistent `Expect-CT` / `NEL` / `Report-To`

##  Header Injection & Response Splitting
- [ ] `Host` header injection (poisoning, cache poisoning)
- [ ] `X-Forwarded-Host` injection for SSRF or URL spoofing
- [ ] `X-Original-URL` / `X-Rewrite-URL` header injection
- [ ] HTTP response splitting via CRLF (`\r\n`) injection
- [ ] Tampering `Location` header in redirects
- [ ] Injecting malicious headers in upstream requests
- [ ] WAF bypass by using non-standard header casing (e.g., `x-Forwarded-host`)
- [ ] Header injection leading to reflected output in error pages or logs
- [ ] Injecting headers to bypass CSP/XSS filters
- [ ] Tampering with `Via`, `Forwarded`, or proxy-specific headers

## Logic & Authentication Abuse
- [ ] Manipulating `Authorization` header (e.g., Basic/AuthZ bypass)
- [ ] Reusing stolen tokens in `Authorization: Bearer <token>`
- [ ] Header-based role escalation (`X-User-Role: admin`)
- [ ] Injecting headers to skip MFA checks (`X-MFA-Verified: true`)
- [ ] Tampering with custom auth headers (e.g., `X-API-Key`)
- [ ] Abusing internal headers for SSO/SSRF (`X-Remote-User`, `X-User-Id`)
- [ ] Sending spoofed `Origin`/`Referer` headers to bypass CSRF protections
- [ ] Using outdated or unsupported headers to cause fallback/insecure behavior
- [ ] App trusting user-controlled `X-Forwarded-For` for logging/IP logic
- [ ] Abuse of `Range` header for partial content DoS (Slow HTTP attacks)

## Information Disclosure
- [ ] Application leaking debug headers (`X-Powered-By`, `X-Backend`, etc.)
- [ ] Disclosing server software/version via `Server:`, `X-AspNet-Version`
- [ ] Headers leaking CDN/Proxy info (`Via`, `X-CDN`)
- [ ] Revealing internal IPs via misconfigured proxy headers
- [ ] Revealing internal routes via `Location` or redirect headers
- [ ] Sensitive info in headers (`X-User-Email`, `X-Session-Token`)
- [ ] Verbose CORS headers exposing methods or credentials
- [ ] Verbose `Accept`, `Accept-Encoding`, etc. in error messages
- [ ] `ETag` values leaking sensitive resource versions
- [ ] `Set-Cookie` used insecurely in cross-domain responses

##  Abuse of Caching and Proxy Behavior
- [ ] Insecure caching of authenticated pages (no `Cache-Control: private`)
- [ ] Cache poisoning via user-controlled `Host`, `X-Forwarded-Host`
- [ ] `Vary` header missing, allowing cache key collision
- [ ] `Content-Encoding` or `Content-Length` tampering (proxy smuggling)
- [ ] Multiple conflicting headers (`Host`, `X-Host`, etc.) for cache/key confusion
- [ ] Content sniffing attacks due to `Content-Type` mismatch
- [ ] Misuse of `Transfer-Encoding` header (smuggling or desync attacks)
- [ ] Forwarding hop-by-hop headers incorrectly (`Connection`, `Keep-Alive`)
- [ ] Tampering with `Accept` or `Accept-Language` to trigger logic flaws
- [ ] Exploiting `X-Accel-Redirect` or `X-Sendfile` headers to read arbitrary files

#  Tips for Testing:
- Use **Burp Suite**, **Hoppscotch**, or **curl** to send custom headers
- Always check responses with **Logger++**, **Proxy History**, and **Repeater**
- Target headers used in **auth, redirection, caching, SSRF, and IP logic**
---
