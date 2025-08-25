
## Targets: Apache, Nginx, Varnish, Node.js, Express, Flask, Laravel, Django, etc.

---

## Authentication / Session Management
- [ ] `/login` → check for absolute links in response (Location: header)
- [ ] `/register` → confirmation email includes `Host:` or full URL
- [ ] `/forgot-password` → password reset links use host header
- [ ] `/verify-email` → confirmation token link poisoned via Host
- [ ] `/resend-confirmation` → check link in body/header
- [ ] Email headers containing injected host (X-Forwarded-Host reflected)
- [ ] 2FA QR codes or OTP pages referencing Host
- [ ] Cookies scoped based on host manipulation
- [ ] Redirect after login (`Location:` header injection via host)
- [ ] Subdomain login flows (`Host:` used for routing)

---

## Email / Notification Systems
- [ ] Email confirmation link uses unsanitized `Host:` in email body
- [ ] Password reset or welcome email link vulnerable to injection
- [ ] `/send-invite` or `/refer` → target URL contains Host
- [ ] Admin or user alerts contain poisoned URLs
- [ ] Email previews that render absolute links based on Host
- [ ] `/email/test` or `/debug` reflects Host in preview
- [ ] Notification messages that link to the application
- [ ] `unsubscribe` links generated using Host
- [ ] Email footers or logos pulled from `Host`-based URL
- [ ] Support email content includes affected URL

---

## API & Microservices
- [ ] Internal API routing based on `Host:`
- [ ] `/api/gateway` → Host header affects backend resolution
- [ ] API key validation fails open when Host is manipulated
- [ ] Reverse proxy trusts `Host` or `X-Forwarded-Host` unsafely
- [ ] Misconfigured backends using Host header for target selection
- [ ] Header-based SSRF protection bypass using Host
- [ ] `/api/redirect` → redirects to external domain via Host
- [ ] Host affects API versioning or endpoint resolution
- [ ] JSON/HTML response reflects full URLs derived from Host
- [ ] Content negotiation influenced by Host injection

---

## Redirects & URL Generation (31–40)
- [ ] `/redirect?url=...` uses Host for validation or redirects
- [ ] Absolute URLs returned in `Location:` headers based on Host
- [ ] Sitemap or robots.txt includes full poisoned URLs
- [ ] Canonical tags rendered using Host
- [ ] Meta-refresh tags using Host-based logic
- [ ] Login/logout redirect URLs reflect Host
- [ ] Social media sharing buttons using poisoned absolute URLs
- [ ] QR codes or shortened links generated from Host
- [ ] PDF generation templates include links from Host
- [ ] In-app browser or iframe sources using poisoned Host

---

## Debugging / Dev Tools
- [ ] `/debug`, `/trace`, `/status` reflects full request headers
- [ ] Logs stored or shown publicly with `Host` value
- [ ] `/headers` or `/echo` endpoints reflecting host
- [ ] Dev environments trusting Host for routing (e.g., `dev.example.com`)
- [ ] Misconfigured `.env` or config files trusting Host
- [ ] Reverse proxy header forwarding incorrectly configured
- [ ] Load balancers passing Host unvalidated to apps
- [ ] Admin panel links generated using Host
- [ ] Caching based on Host header → Web Cache Poisoning risk
- [ ] Host header used to validate domain before sending emails

---

## Fuzzing Payloads
- [ ] `Host: attacker.com`
- [ ] `Host: 127.0.0.1`
- [ ] `Host: evil.com\nX-Forwarded-Host: target.com`
- [ ] `Host: trusted.com\nX-Host: evil.com`
- [ ] `X-Forwarded-Host: attacker.com`
- [ ] Check for response splits, poisoned redirects, or SSRF

---

## What to Look For
- [ ] Full URLs in body or headers with your injected host
- [ ] Redirection to external domains
- [ ] Password reset/activation links to attacker-controlled domain
- [ ] Cache poisoning via host-based differentiation
- [ ] SSRF endpoint using Host-derived URLs

---

## Tools
- [ ] Burp Suite (Repeater + Logger)
- [ ] `curl -H "Host: attacker.com"`
- [ ] Param Miner (Burp Extension)
- [ ] Web Cache Deception & Poisoning scripts
- [ ] Logger services (Burp Collaborator, Interactsh)

---
