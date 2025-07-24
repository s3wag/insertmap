
##  Purpose: Identify locations vulnerable to CL.TE / TE.CL / Transfer-Encoding quirks in HTTP parsing inconsistencies

---

## Entry Points – General Endpoints
- [ ] `/` – Check homepage parsing behaviors
- [ ] `/login` – Smuggle a second request inside login
- [ ] `/register` – Delayed request bodies or malformed headers
- [ ] `/forgot-password` – Inject follow-up reset requests
- [ ] `/upload` – Multipart body injection
- [ ] `/profile` – Modify or smuggle requests behind auth
- [ ] `/cart`, `/checkout` – Queue poisoning via smuggled requests
- [ ] `/order` – Duplicate order creation via smuggling
- [ ] `/api/*` – API endpoints that parse headers differently
- [ ] `/oauth/*` – Smuggle inside OAuth callback or token request

---

## HTTP Headers to Target
- [ ] `Content-Length` – Test for duplication / override
- [ ] `Transfer-Encoding` – Chunked + dual header behaviors
- [ ] `TE:` – TE:trailers variant
- [ ] `Expect:` – Expect: 100-continue smuggle trigger
- [ ] `Host:` – Multiple Host headers
- [ ] `X-Forwarded-*` – Proxies manipulating request parsing
- [ ] `Connection:` – Unexpected header handling
- [ ] `Via:` – Proxy chains
- [ ] `Upgrade-Insecure-Requests:` – Appending malicious headers
- [ ] Custom headers triggering WAF or CDN inconsistencies

---

## CDN / Load Balancer Insertion Points
- [ ] Behind Cloudflare/Akamai/Fastly/CDN – see parsing difference
- [ ] Multiple backends with inconsistent parsing (e.g. Apache+Nginx)
- [ ] Proxy that strips or rewrites `Transfer-Encoding`
- [ ] Proxy that ignores conflicting `Content-Length`
- [ ] Backend accepting non-standard TE values (e.g., `TE: gzip`)
- [ ] Reverse proxies (Envoy, Traefik, HAProxy) — CL/TE smuggling
- [ ] Load balancers stripping headers (e.g. AWS ALB)
- [ ] Cache servers misinterpreting split requests
- [ ] CORS preflights triggering smuggled second request
- [ ] WAF modifying or normalizing headers inconsistently

---

## Business Logic / Application Actions
- [ ] Password reset flow → delayed smuggled request
- [ ] Promo or referral links → smuggle registration
- [ ] Admin-only functionality — smuggle with admin path
- [ ] Hidden endpoints behind auth — accessible via smuggled request
- [ ] Scheduled actions (cron APIs) → queued via smuggle
- [ ] Email confirmation / token validation endpoints
- [ ] File upload + file download endpoint interaction
- [ ] Multi-part forms smuggling payloads inside boundaries
- [ ] Checkout process allowing delayed POST
- [ ] Partner API integrations with different parsing expectations

---

## Chained or Queued Requests
- [ ] POST followed by GET smuggling (CL.TE)
- [ ] POST with delayed body, second request prepended
- [ ] Request splitting with `0\r\n\r\nPOST /malicious...`
- [ ] Desyncing the queue on proxy — leaking other users' requests
- [ ] DoS via queued unparsed smuggled requests
- [ ] Poisoning cache headers via smuggled requests
- [ ] Smuggled second request using `Transfer-Encoding: chunked`
- [ ] Multipart chunked body smuggling (nested)
- [ ] Sending partial headers in first request, completing in second
- [ ] Triggering internal request confusion between proxy/backend

---

## Fuzzing Payload Examples
- [ ] `Transfer-Encoding: chunked\r\n\r\n0\r\n\r\nGET /admin HTTP/1.1`
- [ ] `Content-Length: 4\r\n\r\nPOST /evil HTTP/1.1`
- [ ] Dual TE/CL headers → backend mismatch
- [ ] `Transfer-Encoding: cow\r\nTransfer-Encoding: chunked`
- [ ] `Content-Length: 10\nTransfer-Encoding: chunked\n\n0\r\n\r\n`

---

## Testing Notes
- [ ] Try different line breaks (`\n`, `\r`, `\r\n`)
- [ ] Use both HTTP/1.1 and HTTP/2 if supported
- [ ] Log and inspect response times, codes, and leaks
- [ ] Try both GET and POST method smuggling
- [ ] Observe shared resources (queue logs, logs, cache keys)

---

## 🧪 Tools
- [ ] Burp Suite + HTTP Request Smuggler Plugin
- [ ] Smuggler.py
- [ ] curl (low-level request crafting)
- [ ] mitmproxy or custom socket scripts
- [ ] Race-the-Web for timing-based desync

---
