
## Purpose:
Detect duplicate parameters or improperly parsed user input that leads to authentication bypass, WAF bypass, logic flaws, cache poisoning, or input validation failures.

---

## Authentication & Session Endpoint
- [ ] `/login?user=admin&user=guest`
- [ ] `/register?role=user&role=admin`
- [ ] `/forgot-password?email=attacker@x.com&email=victim@x.com`
- [ ] `/2fa?code=1234&code=0000`
- [ ] `/logout?token=abc&token=xyz`
- [ ] `/session?token=xyz&token=expired_token`
- [ ] `/sso/callback?redirect_uri=evil.com&redirect_uri=good.com`
- [ ] `/mfa/setup?step=1&step=2`
- [ ] `/otp/verify?otp=1111&otp=2222`
- [ ] `/auth?provider=google&provider=internal`

---

## Account/Profile Management
- [ ] `/profile?user_id=1&user_id=2`
- [ ] `/change-email?email=attacker@evil.com&email=victim@target.com`
- [ ] `/delete-account?confirm=yes&confirm=no`
- [ ] `/settings?dark_mode=1&dark_mode=0`
- [ ] `/update-password?password=abc&password=xyz`
- [ ] `/avatar/upload?file=avatar.jpg&file=evil.php`
- [ ] `/preferences?timezone=UTC&timezone=PST`
- [ ] `/notifications?enabled=true&enabled=false`
- [ ] `/roles?admin=false&admin=true`
- [ ] `/permissions?edit=true&edit=false`

---

## E-Commerce / Checkout Flows
- [ ] `/cart/add?item=101&item=102`
- [ ] `/cart/update?qty=1&qty=999`
- [ ] `/checkout?total=100&total=1`
- [ ] `/apply-coupon?code=XYZ&code=ABC`
- [ ] `/buy?product_id=200&product_id=1`
- [ ] `/payment?amount=0&amount=1000`
- [ ] `/shipping?method=standard&method=express`
- [ ] `/invoice?customer=abc&customer=def`
- [ ] `/subscription?plan=basic&plan=premium`
- [ ] `/wallet/topup?value=0&value=1000`

---

## API & Query Parameters
- [ ] `/api/users?id=1&id=admin`
- [ ] `/api/data?json=true&json=false`
- [ ] `/api/items?limit=10&limit=1000`
- [ ] `/search?q=abc&q=xyz`
- [ ] `/api/token?refresh=true&refresh=false`
- [ ] `/api/export?format=csv&format=json`
- [ ] `/api/filter?type=guest&type=admin`
- [ ] `/api/balance?currency=INR&currency=USD`
- [ ] `/api/upload?mime=jpg&mime=php`
- [ ] `/api/view?id=999&id=0`

---

## File Handling & Upload
- [ ] `/upload?file=img.jpg&file=img.php`
- [ ] `/download?name=doc.pdf&name=../../../etc/passwd`
- [ ] `/backup?file=config&file=../../db`
- [ ] `/export?file=valid.csv&file=malicious.exe`
- [ ] `/preview?doc=invoice.doc&doc=evil.html`
- [ ] `/report?type=pdf&type=zip`
- [ ] `/import?source=url1&source=url2`
- [ ] `/media?path=images&path=../secrets`
- [ ] `/pdfgen?template=official&template=attack`
- [ ] `/archive?target=logs&target=../../root`

---

## Common Bypass & Exploitation Patterns
- [ ] `param=value1&param=value2` → double keys
- [ ] `param[]=1&param[]=2` → array keys
- [ ] `param[0]=foo&param[1]=bar` → object/array bypass
- [ ] `param=value%00` + `param=value` → null-byte injection
- [ ] `param=value;param=value2` (semicolon injection)

---

## Test Vectors
- [ ] Check which parameter is prioritized: first or last?
- [ ] Does duplication affect security logic? (e.g. role=admin&role=user)
- [ ] Does backend parse arrays vs scalar values inconsistently?
- [ ] What happens when mixed data types are passed? (string + boolean)

---

## Tooling
- [ ] Burp Suite: Param Miner, Repeater
- [ ] HPP-Fuzzer (automated scanner)
- [ ] Custom curl/bash scripts for brute injection
- [ ] mitmproxy or Postman for manual inspection

---
