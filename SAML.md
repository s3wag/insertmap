

> Use this checklist to assess vulnerabilities in SAML authentication & identity assertions across parameters, XML content, metadata, and signature verification logic.

## SAML Message Injection Points
- [ ] `SAMLResponse` (Base64 encoded in POST body)
- [ ] `RelayState` parameter (used for redirection)
- [ ] `SAMLRequest` parameter (in SSO flows)
- [ ] `Issuer` in the assertion
- [ ] `Subject` / `NameID` → impersonate users
- [ ] `AuthnContextClassRef` → bypass MFA
- [ ] `Conditions/NotBefore` and `NotOnOrAfter`
- [ ] `AudienceRestriction` (test audience mismatch)
- [ ] `AttributeStatement` → escalate user roles
- [ ] `AssertionConsumerServiceURL` (ACS URL)

## Signature-Based Attacks
- [ ] Remove the signature block (see if it validates)
- [ ] Sign a dummy assertion (if signature not enforced)
- [ ] External entity referencing (XXE inside SAML)
- [ ] Use public key in place of private (key confusion)
- [ ] Signature Wrapping Attack (placing valid assertion inside an unsigned section)
- [ ] Duplicate elements → signature validates first, app uses second
- [ ] Canonicalization bypass (c14n mismatch)
- [ ] Test weak RSA keys (under 1024 bits)
- [ ] Sign only partial XML (not the entire assertion)
- [ ] Using deprecated algorithms (SHA-1)

## SAML Replay & Timing
- [ ] Replay previously issued SAMLResponses
- [ ] Expired `NotOnOrAfter` → still accepted
- [ ] Future `NotBefore` still accepted
- [ ] No validation of timestamps
- [ ] Modify `AuthnInstant` or `SessionNotOnOrAfter` for session abuse
- [ ] Replay IDPs assertion across different SPs (no audience restriction)

## Logic & Role Abuse
- [ ] Modify `AttributeStatement` → `isAdmin = true`
- [ ] Change `Groups`, `Role`, `AccessLevel`
- [ ] Use another user’s `NameID`/`Subject`
- [ ] Injection into `Issuer` → mismatch spoof
- [ ] IDP accepts any `ACS URL` (open redirect or injection)
- [ ] Bypass forced login by replaying `SAMLResponse`

## Misconfiguration Checks
- [ ] SP doesn’t validate signature
- [ ] SP accepts unsigned assertions
- [ ] Accepts assertion from untrusted issuer
- [ ] Uses GET instead of POST (leak in logs)
- [ ] Assertion includes sensitive PII in plain text
- [ ] `RelayState` used for open redirect
- [ ] IDP metadata includes HTTP endpoint, not HTTPS
- [ ] ACS endpoints don’t validate Host/CSP
- [ ] Dynamic SP endpoint validation skipped

## File & XML Payload Injection
- [ ] XXE injection inside `<saml:NameID>` or `<saml:Attribute>`
- [ ] XXE via metadata endpoint (external DTD)
- [ ] External file inclusion via custom attributes
- [ ] Entity injection: load local files into attribute fields
- [ ] Replace `Issuer` or `Audience` with XXE vectors

## Token Processing Issues
- [ ] SP trusts self-signed certs
- [ ] Multiple assertions in single response
- [ ] Assertion reused in JWT (check for downstream injection)
- [ ] SAML assertions leaked in browser history or logs
- [ ] Assertion not invalidated on logout

## Developer/Debug Logic
- [ ] SAML debug mode shows parsed assertion in UI/logs
- [ ] Accepts SAML from dev/test IDPs in prod
- [ ] Hardcoded `acsUrl` or `issuer` bypassable
- [ ] Relies on frontend JS for validation