
## Goal:
Identify vulnerable insertion points across WebSocket connections that may lead to:
- Injection
- Authorization bypass
- Protocol abuse
- Sensitive data leakage
- Business logic abuse

---

## WebSocket Handshake Manipulation
- [ ] `Sec-WebSocket-Protocol` header injection
- [ ] `Origin` header spoofing for CSWSH attacks
- [ ] `Host` header manipulation during handshake
- [ ] `Cookie` injection to test session abuse
- [ ] Inject CRLF into handshake headers
- [ ] Downgrade attack via invalid `Upgrade` headers
- [ ] Tamper `Connection: Upgrade` logic
- [ ] Test for insecure `wss://` ➝ `ws://` fallback
- [ ] Check for handshake failure leakage
- [ ] Check `Referer` header for leak or redirect issues

---

## Payload-Based Injection
- [ ] JSON injection in WebSocket messages (`{"isAdmin":true}`)
- [ ] Command injection inside structured payload
- [ ] SQL/NoSQL injection inside message field
- [ ] DOM injection in HTML/JS payload sent via socket
- [ ] SSTI inside WebSocket message template
- [ ] JavaScript expression evaluation in frontend logic
- [ ] LDAP injection if payload reaches directory services
- [ ] Header manipulation via payload reflection
- [ ] Payload that triggers unsafe deserialization
- [ ] Arbitrary object overwrite in complex message types

---

## Authorization Bypass Insertion
- [ ] Reuse WebSocket token in unauthorized context
- [ ] Replay of message from lower-privileged user
- [ ] Change of `userId` in WebSocket message
- [ ] Tamper `role` or `group` attributes in message
- [ ] Bypass subscription-level access control
- [ ] Direct access to admin-only socket events
- [ ] Unsubscribe/resubscribe hijack attempts
- [ ] Data leakage via universal subscription event
- [ ] Endpoint switching after upgrade bypass
- [ ] Message crafted to simulate trusted source

---

## Functional / Business Logic Abuse
- [ ] Abuse real-time messaging API (e.g., `sendMessage`)
- [ ] Repeat event to drain tokens, balance, etc.
- [ ] Manipulate `action` field (e.g., `action: delete`)
- [ ] Race condition via simultaneous message send
- [ ] Use `*` wildcards to gain unintended access
- [ ] Exploit lack of rate limiting in message stream
- [ ] Tamper workflow sequence (`init ➝ cancel ➝ commit`)
- [ ] Supply invalid object references (broken validation)
- [ ] Bypass client validation with tampered event type
- [ ] Access server logs/events via debug message types

---

## Protocol / Infrastructure Misuse
- [ ] Attempt binary message injection
- [ ] Send raw XML if XML parsing is supported
- [ ] Inject control characters (0x00–0x1F) in payload
- [ ] Abuse socket fragmentation for DoS/logic abuse
- [ ] Force socket keep-alive flood
- [ ] Connect from unauthorized origin
- [ ] Switch to alternative protocols (e.g., MQTT)
- [ ] Misuse ping/pong frame to maintain ghost sessions
- [ ] Fuzz compression extensions (e.g., `permessage-deflate`)
- [ ] Abuse reconnect logic for spam/flooding

---
