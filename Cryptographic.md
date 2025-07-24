
## 🎯 Goal:
Identify user-controllable inputs and vulnerable configurations that lead to cryptographic weaknesses in web applications — including encryption/decryption flaws, key handling issues, signature manipulation, insecure storage, and randomness problems.

---

## Encryption/Decryption Flaws
- [ ] User input passed to `crypto.createCipheriv()` without sanitization
- [ ] Attacker-controlled IV used in AES-CBC/CTR modes
- [ ] Reusing IVs or keys from user-controlled sources
- [ ] Input used as encryption key or salt
- [ ] AES ECB mode used on attacker-supplied data
- [ ] Partial plaintext knowledge leaks via padding oracle
- [ ] URL param decrypted server-side with no integrity checks
- [ ] No HMAC applied to ciphertext before storage
- [ ] Upload/download endpoint decrypts blob without verifying source
- [ ] LocalStorage encrypted with hardcoded or weak key

---

## Symmetric Key Management Issues
- [ ] Password used directly as symmetric encryption key
- [ ] Static key loaded from config used across all users
- [ ] User-submitted key material accepted in JSON body
- [ ] KDF (PBKDF2, bcrypt) used with low iterations
- [ ] No salting applied when hashing passwords or sensitive data
- [ ] Attacker controls parameters of key derivation (salt, iteration)
- [ ] Key rotation endpoints exposed or weakly authenticated
- [ ] User-controllable key used to sign tokens or files
- [ ] Multi-tenant app uses shared encryption key across users
- [ ] Base64-decoded keys accepted from URL parameters

---

## 🧾 Signature Manipulation/Verification Issues (21–30)
- [ ] JWT `alg` header not validated, allows `none`
- [ ] JWT key confusion (HMAC vs RSA public key misuse)
- [ ] Signed requests (HMAC) accept attacker-controlled timestamp/body
- [ ] Signature verification done after deserialization
- [ ] Signature keys exposed via error/debug endpoint
- [ ] Replay attacks due to lack of nonce or timestamp checks
- [ ] Webhook signature computed using predictable secret
- [ ] Base64 encoding applied before signature verification
- [ ] Tampered payloads with unchanged signatures accepted
- [ ] Signed cookies or URLs that allow tampering

---

## 🧂 Hashing & Collisions (31–40)
- [ ] MD5/SHA1 used to hash attacker-supplied input
- [ ] Uploads checked with `md5(filename)` — predictable hash
- [ ] SHA-1 HMAC used with short keys
- [ ] No length checking on hash values submitted by user
- [ ] Hash comparisons vulnerable to timing attacks
- [ ] Weak uniqueness checks via hash of form fields
- [ ] User-supplied hash used to validate download/upload integrity
- [ ] Predictable file content leads to hash collision
- [ ] No salt added to hashed user attributes (e.g., email, ID)
- [ ] Session identifiers hashed from guessable info

---

## 🎲 Entropy / Randomness Failures (41–45)
- [ ] `Math.random()` used for token/session generation
- [ ] `crypto.randomBytes()` size too small (< 16 bytes)
- [ ] Non-cryptographic PRNG used in password reset flows
- [ ] Predictable OTP/token generation by timestamp
- [ ] Entropy source partially under attacker control

---

## 🧱 Web Crypto API / JS Crypto Issues (46–50)
- [ ] Using `SubtleCrypto.encrypt()` with weak/unsupported modes
- [ ] Storing keys in browser’s IndexedDB/localStorage
- [ ] Hardcoded keys in front-end JS
- [ ] Exposing key material via source maps or debug tools
- [ ] Exported keys accessible via ServiceWorker or DevTools

---

## 🚨 Payload Examples
- [ ] `eyJhbGciOiJub25lIn0.eyJ1c2VyIjoiYWRtaW4ifQ.`
- [ ] `/api/download?file=encrypted&key=guessme123`
- [ ] `iv=00000000000000000000000000000000`
- [ ] `{"alg":"HS256", "key":"public.pem contents"}`
- [ ] `GET /reset?token=123456`

---

## 🧠 Tags
#crypto #cryptography #checklist #obsidian #bugbounty #jwt #encryption #paddingoracle #hashing #keymisuse #tokenvalidation