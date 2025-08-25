
## Used to mislead scanners, users, and attackers

---

## Fingerprinting Bluffing
- [ ] Spoofing `Server` header to mimic a different tech stack (e.g., `Server: Apache` on nginx)
- [ ] Adding fake `X-Powered-By: PHP/5.6.40` to confuse tech detection tools
- [ ] Faking `X-AspNet-Version`, `X-AspNetMvc-Version` on non-Microsoft stack
- [ ] Returning conflicting headers (`Server: nginx` + `X-Powered-By: Express`)
- [ ] Adding multiple conflicting `Via` headers to obfuscate request chain
- [ ] Responding with common favicon.ico from other platforms (e.g., IIS)
- [ ] Using fake response signatures in error pages (e.g., "Apache Tomcat 9.0.2 - Error 404")
- [ ] Mimicking file extensions in routing (`.aspx`, `.php`, `.jsp`) on non-dynamic pages
- [ ] Custom 404/403 responses to simulate false tech stack messages
- [ ] Adding random or mixed headers (`X-Drupal-Cache`, `X-Joomla-Cache`) to mislead Wappalyzer/BuiltWith

---

## WAF/CDN Bluffing
- [ ] Faking CDN headers like `CF-RAY`, `X-CDN`, or `X-Cache` to simulate protection
- [ ] Adding `X-WAF-Bypassed: false` or `X-WAF-Protection: enabled` (fake flags)
- [ ] Mimicking Cloudflare’s behavior (e.g., 1020 Access Denied or JS challenge redirect)
- [ ] Injecting Akamai-style headers (`Akamai-Origin-Hop`, `X-Akamai-Edgescape`)
- [ ] Returning rate-limited headers (`Retry-After: 60`) even if no limit enforced
- [ ] Faking WAF block page (HTML with CAPTCHA or JS check)
- [ ] Simulating rate limits (`429 Too Many Requests`) randomly
- [ ] Using security-themed headers like `X-Content-Protection: enabled`
- [ ] Obfuscating real origin IPs by always returning CDN-looking headers
- [ ] Mimicking AWS ALB or Azure headers (`x-amzn-trace-id`, `x-msedge-ref`)

---

## Security Header Misdirection
- [ ] Setting `Strict-Transport-Security` with invalid or weak parameters
- [ ] Faking `Content-Security-Policy` (e.g., policy exists but ineffective)
- [ ] Using misleading `Referrer-Policy` (e.g., `unsafe-url` masked as `strict-origin`)
- [ ] Setting `X-Frame-Options: ALLOW-FROM` with fake or unrelated domains
- [ ] Setting `X-Content-Type-Options: nosniff` but misconfiguring MIME
- [ ] Adding `Permissions-Policy` with no actual restrictions enforced
- [ ] Presenting a secure-looking `Feature-Policy` with no backend validation
- [ ] Mimicking real TLS headers but delivering over HTTP
- [ ] Setting up CSP with `report-uri` to fake endpoint
- [ ] Using deprecated or unknown headers (`X-Secure-Protocol: enabled`)

---

## HTTP Response Bluffing
- [ ] Changing status codes (`200 OK` on error pages to confuse scanners)
- [ ] Redirecting on 500 errors to a 200 success page
- [ ] Using `302 Found` for forbidden actions to avoid 403 detection
- [ ] Delivering valid-looking HTML with `204 No Content` status
- [ ] Injecting false `Content-Type: application/json` while sending HTML
- [ ] Returning `Content-Length` headers that don’t match actual body length
- [ ] Simulating directory listing in HTML while backend blocks it
- [ ] Generating fake CORS headers for decoy endpoints
- [ ] Spoofing successful login page on `/admin` but denying real login backend
- [ ] Response padding to throw off fingerprinting tools (add random bytes)

---

## Application-Level Deception
- [ ] Using decoy admin panels that log scanner IPs (`/admin`, `/wp-admin`, `/phpmyadmin`)
- [ ] Deploying honeypot fields (e.g., fake input with `display: none`) in login forms
- [ ] Returning random tech keywords in 404 pages (e.g., "Java Servlet", "Laravel Blade")
- [ ] Giving different response headers based on User-Agent (e.g., `curl` vs `Mozilla`)
- [ ] Disabling specific responses for automated scanners (e.g., ZAP, Nikto)
- [ ] Including non-working API docs (`/swagger`, `/v2/api-docs`) to confuse testers
- [ ] Mimicking backend behavior (e.g., fake GraphQL introspection)
- [ ] Exposing non-functional but valid-looking robots.txt paths
- [ ] Planting decoy HTML comments with fake credentials
- [ ] Serving different responses on IPv6 vs IPv4 to confuse origin detection

---

# Notes:
- These tactics are often used in **WAFs**, **Honeypots**, or **Deceptive Infrastructure**.
- Use with caution: **bluffing should not replace proper security**.
- Test real functionality, not just headers or UI clues.

# 🛠️ Useful Tools:
- `httpx`, `curl -I`, `nmap --script http-*`, `wappalyzer`, `httprint`, `nikto`, `ZAP`

---
