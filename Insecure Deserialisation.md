
## Focus: Java (Serialized), PHP, .NET, Python, Ruby, YAML, JSON, XML formats

---

## Authentication & Session Management
- [ ] `Cookie: session=...` (Base64/Hex-encoded object)
- [ ] `Cookie: auth_token=...`
- [ ] `Authorization: Bearer <serialized_token>`
- [ ] JWT tokens with `alg: none` or `alg: HS256` using public key
- [ ] POST /login → `rememberMe`
- [ ] SAML or SSO tokens passed in POST
- [ ] Hidden form fields storing serialized session objects
- [ ] `/resume_session` endpoint with session_id param
- [ ] `/auth/validate` using serialized `state` or `token`
- [ ] WebSocket initial handshake payload with embedded objects

---

## User Profiles & Preferences
- [ ] `/profile` → `settings` parameter
- [ ] `/user` → `preferences` (JSON/YAML/XML/PHP object)
- [ ] POST /update-profile → custom object in `body`
- [ ] `/avatar` upload with metadata in serialized format
- [ ] Client-side encrypted blob passed in user settings
- [ ] `/save-state` → `windowState` parameter
- [ ] `/layout` → `gridConfig`
- [ ] `/customization` → object passed as Base64
- [ ] `/theme` or `/ui` → `style` as serialized object
- [ ] `?config=...` param in GET with full object config

---

## API / Webhook Payloads
- [ ] Webhook POSTs containing entire serialized request object
- [ ] `/api/submit` with serialized `data` field
- [ ] `/api/update` with file upload (XML/YAML/JSON blob)
- [ ] `/process` → `taskData`
- [ ] `/message` or `/notification` → `payload`
- [ ] `/execute` with custom command object
- [ ] `/sync` → `syncData`
- [ ] `/merge` → merge conflict object passed
- [ ] `/api/event` → serialized event object
- [ ] `/callback` → serialized response or payload

---

## File Uploads & Imports
- [ ] File upload endpoint accepting `.ser`, `.dat`, `.yml`, `.pickle`, `.pl`, `.php`
- [ ] `/import` → config file containing serialized object
- [ ] `.php` or `.asp` file containing embedded base64 object
- [ ] CSV/Excel import with serialized blobs in fields
- [ ] Archive uploads (ZIP/JAR) containing serialized files
- [ ] `.bson` or `.msgpack` uploads
- [ ] YAML or XML containing external entity references
- [ ] `.pkl` files for ML model upload
- [ ] `/restore` from user backup file
- [ ] Deserialized PDF/XLS macros or metadata

---

## App Functionality / Internal Features
- [ ] `/debug` → `trace` parameter
- [ ] `/admin/load` → config object passed via POST
- [ ] `/preview` → serialized object previewed
- [ ] `/render` → widget config passed as object
- [ ] `/report` → report filter as serialized blob
- [ ] `/engine/start` → object controlling execution
- [ ] `/replay` → replay session with serialized input
- [ ] `/test` → test case object passed to server
- [ ] `/serialize`/`/deserialize` dev endpoints (dev mode)
- [ ] `/hook` → middleware object passed from frontend

---

## Deserialization Exploit Tips
- [ ] Try: `Base64`, `Hex`, `Zlib`, `gzip`, `PHP serialization`, `pickle`, `Java object stream`
- [ ] Look for: `rO0AB`, `O:`, `a:`, `s:`, `%00`, YAML/JSON/XML injection vectors
- [ ] Use gadgets: `ysoserial`, `PHPGGC`, `Marshalsec`, `pickle-deser`
- [ ] Observe exceptions: `java.io.InvalidClassException`, `unmarshal`, `ObjectInputStream`, etc.
- [ ] Fuzz endpoints with serialized payloads using repeater or intruder

---

## Tools
- [ ] `ysoserial` (Java)
- [ ] `PHPGGC` (PHP)
- [ ] `pickle-shell` (Python)
- [ ] `Burp Deserialization Plugin`
- [ ] `SerialSniper`, `Inql`, `GadgetProbe`

---
