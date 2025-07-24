
##  Goal:
Test all user-controllable redirection points that may allow unvalidated redirection to attacker-controlled domains.

---

## URL Parameters with Redirection Logic
- [ ] `/redirect?url=https://evil.com`
- [ ] `/login?redirect=https://evil.com`
- [ ] `/auth/callback?continue=https://evil.com`
- [ ] `/home?next=https://evil.com`
- [ ] `/checkout?returnUrl=https://evil.com`
- [ ] `/dashboard?go=https://evil.com`
- [ ] `/exit?destination=https://evil.com`
- [ ] `/signin?ret=https://evil.com`
- [ ] `/start?redir=https://evil.com`
- [ ] `/forward?link=https://evil.com`

---

## Variants with Different Parameter Encodings
- [ ] `/redirect?url=//evil.com`
- [ ] `/redirect?url=evil.com`
- [ ] `/redirect?url=http://evil.com@trusted.com`
- [ ] `/redirect?url=http:evil.com`
- [ ] `/redirect?url=%2f%2fevil.com`
- [ ] `/redirect?url=https://evil.com/%2e%2e`
- [ ] `/redirect?url=https%3a%2f%2fevil.com`
- [ ] `/redirect?url=evil.com#@trusted.com`
- [ ] `/redirect?url=//evil.com%23@trusted.com`
- [ ] `/redirect?url=data:text/html,<script>`

---

## Parameter Names in Common Use
- [ ] `/api/forward?u=https://evil.com`
- [ ] `/jump?url=https://evil.com`
- [ ] `/click?target=https://evil.com`
- [ ] `/open?file=https://evil.com`
- [ ] `/view?image=https://evil.com`
- [ ] `/load?link=https://evil.com`
- [ ] `/download?resource=https://evil.com`
- [ ] `/path?redir_url=https://evil.com`
- [ ] `/fetch?redirect_uri=https://evil.com`
- [ ] `/api/oauth?redirect_to=https://evil.com`

---

## Redirection Inside Path or Fragments
- [ ] `/goto/https://evil.com`
- [ ] `/redirect/https://evil.com`
- [ ] `/auth/forward/https://evil.com`
- [ ] `/preview/#https://evil.com`
- [ ] `/start#url=https://evil.com`
- [ ] `/callback?next_page=%23https://evil.com`
- [ ] `/action?url=https://evil.com&foo=bar`
- [ ] `/continue?state=xyz&url=https://evil.com`
- [ ] `/jump-to?redirect=https://evil.com`
- [ ] `/confirm?forward_url=https://evil.com`

---

## Advanced/Tricky Test Cases
- [ ] Redirection via JavaScript: `location.href = getParam('redirect');`
- [ ] Redirection in `meta refresh` tags
- [ ] Redirection after OAuth login without strict validation
- [ ] Redirect chained after CAPTCHA solve
- [ ] Redirect during 2FA (e.g., `/2fa?next=...`)
- [ ] Hidden in base64 encoding: `/redirect?url=aHR0cHM6Ly9ldmlsLmNvbQ==`
- [ ] Mixed protocol redirection: `/redirect?url=javascript:alert(1)`
- [ ] Using CRLF injection for redirect manipulation
- [ ] CDN cache misconfiguration + redirect param
- [ ] Open redirect triggered via JSON input in POST requests

---

## Testing Notes
- [ ] Try schemes: `http`, `https`, `//`, `javascript:`, `data:`
- [ ] Test relative path bypass: `/%5cevil.com`, `%2f%2fevil.com`
- [ ] Test subdomain tricks: `evil.com.trusteddomain.com`
- [ ] Test URL fragments: `trusted.com#evil.com`
- [ ] Observe HTTP headers (`Location`, `Refresh`) and JS-based redirects

---

## Tools
- [ ] Burp Suite with *Open Redirect* plugin
- [ ] Turbo Intruder for automation
- [ ] Param-miner for discovering hidden redirect params
- [ ] Gau + GF + qsreplace combo
- [ ] FFUF or Kiterunner for redirect fuzzing

---
