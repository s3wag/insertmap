# Authentication Bypass

##  Goal:
Identify and test all potential insertion points where authentication mechanisms may be bypassed due to misconfigurations, flawed logic, insecure token handling, or parameter tampering.

---

## Token-Based Authentication
- [ ] `Authorization: Bearer <user-input>` — Replace with random/expired tokens
- [ ] JWT payload tampering: change `alg`, `sub`, `role`, `exp`
- [ ] `access_token` in URL: `?access_token=...`
- [ ] `X-API-Key` header (try null/invalid/old keys)
- [ ] Token reuse across different users or sessions
- [ ] JWT without signature verification (`alg=none`)
- [ ] Changing JWT `kid` to path traversal or pointing to public file
- [ ] Replay of tokens issued to other roles (e.g. `refresh_token`)
- [ ] Leaked token reuse in Authorization or Cookie
- [ ] Access using expired token or invalid `iat`/`exp`

---

## Session-Based Auth Weakness
- [ ] `Set-Cookie: session=...` — reuse or brute force old session tokens
- [ ] Missing `HttpOnly` or `Secure` flags in auth cookies
- [ ] Tampering with `userid`, `username`, or `role` in cookie value
- [ ] Session fixation via predefined `session_id`
- [ ] Cookie used from different user agent/IP
- [ ] Session not invalidated after logout or password change
- [ ] Session cookie guessable or sequential
- [ ] Multiple cookies accepted — test injection (`Cookie: user=admin; user=guest`)
- [ ] Downgrade of session (e.g. from MFA to single factor)
- [ ] Lack of CSRF protection allowing session riding

---

## Bypassing Login Logic
- [ ] `email=admin@example.com&password=admin` — test weak creds
- [ ] Bypass with SQLi: `' OR 1=1--`
- [ ] Logic-based bypass using `username=admin&password[0]=a`
- [ ] Overriding fields like `isAdmin=true` or `role=admin`
- [ ] Brute-force endpoints without rate limiting or lockout
- [ ] Login using `X-Original-URL`, `X-Forwarded-For`, etc.
- [ ] Login using only user ID (no password required)
- [ ] Forgotten password endpoints with insecure token verification
- [ ] Login bypass via API versioning (`/api/v1/login`)
- [ ] POST-to-GET login endpoint confusion

---

## Hidden or Forgotten Endpoints
- [ ] `/admin` or `/admin/login` — hidden login panel
- [ ] `/debug`, `/dev-login`, `/api/dev-auth`
- [ ] `/login-as?user=123` for impersonation
- [ ] `/bypass-auth?token=guest123`
- [ ] Unprotected `/graphql` or `/introspect`
- [ ] `/api/users/me` responds without authentication
- [ ] `/actuator`, `/health`, `/metrics` exposing user data
- [ ] `/reset-password` token not verified
- [ ] `GET /config.json` leaking admin credentials
- [ ] `OPTIONS` method responding with unexpected access

---

## Misc Exploitable Vectors
- [ ] Bypass via `X-Original-URL` header (reverse proxy misconfig)
- [ ] Tampering with `Referer` or `Origin` headers
- [ ] `X-Forwarded-For: 127.0.0.1` for IP-based auth bypass
- [ ] Caching token responses (reusing token of other users)
- [ ] OAuth flow skipping token exchange step
- [ ] Access tokens not scoped or validated (`scope: *`)
- [ ] SSO bypass via unvalidated email domain in ID token
- [ ] Forgotten test user still valid (`test:test`)
- [ ] Pre-auth endpoints calling internal protected APIs
- [ ] Lack of user verification in 2FA or login flows

---

## Authentication Bypass
[ ] 
```
1. Check if post authentication URLs are directly accessible and do not have any session bound to it.
2. In case the URL is stolen/guessable/brute-forceable, it can lead to account takeover.
```

[ ] CAPTCHA Bypass - X-Forwarded-For
```
1. Bypass the CAPTCHA check by injecting a random value into the **X-Forwarded-For header
```

[ ] Lack of Password Confirmation
```
Test if password confirmation is necessary with these actions:
- Change Email Address
- Change Password
- Delete Account
- Manage 2FA
```

[ ] Lack of Verification Email
```
1. Check that during the registration process, an email verification is necessary
```


[ ] No Rate Limiting on a Form
```
1. Send a form and intercept the request with Burp proxy
2. Send the request to intruder
3. Repeat sending the same request 20-30 times
4. Observe that all of these forms are sent without any restrictions
```


[ ] No Rate Limiting or Captcha on Login Page
```
1. Go to login page and send the unsuccessful login attempt request to Burp Intruder
2. Change the password values for brute force as random values
3. Observe that the response to the 20 or 30th request doesn't change and the account is not locked.
```

[ ] Username Email Address Enumeration
```
1. Go to password reset/login/register or any other area that allows writing username or email address input
2. Write an existing username/email address with wrong password to observe error message
3. Write a non-existing username/email address to observe error message
4. See if error message leaks the information of the existence of username/email addresses
```

[ ] Weak Password Policy
```
1. Change password to only numerical
2. Change password to only lower case
3. Change password to common passwords
4. Change password to short passwords
5. Observe that the application has weak or no password policy
```

[ ] Weak Registration Implementation over HTTP
```
1. Intercept the request during the registration to the application via Burp
2. Observe that registration request is sent over HTTP
```

[ ] secure data transport
```
1. search on login page 
2. Send a form and intercept the request with Burp proxy
3. intercept the request with wireshark
4. make sure that the data transport is encryption or not 
```

[ ] Username enumeration
```
1. Status codes
2. Error messages
3. Response times 
   X-Forwarded-For: 
```
   
[ ] Broken Authentication Session Token Bug
```
1. Create a courier account or use existing one.
2. Confirm Your email address.
3. Now log out from your account and request for password reset code for your account .
4. Don't use the code that has been sent to your email address.
5. In new tab or new browser log in back to your account.
6. Go to account setting and change your password .
7. Now go to email and check the password reset code that we requested in step 3.
8. Change Your password using that reset password code .
9. You can see that your password has been changed.
```

[ ] Broken Authentication and Session Management
```
1. Create a Fabricator account having email address "a@x.com".
2. Now Logout and ask for password reset link. Don't use the password reset link sent to your mail address.
3. Login using the same password back and update your email address to "b@x.com" and verify the same. Remove "a@x.com".
4. Now logout and use the password reset link which was mailed to "a@x.com" in step 2.
5. Password will be changed.
```


---