
## Goal:
Identify locations where user-controllable object references (IDs, usernames, tokens, filenames, etc.) are used without proper authorization checks.

---

## User & Account References
- [ ] `/profile?id=1234`
- [ ] `/user/1234/settings`
- [ ] `/users/username123`
- [ ] `POST /update_email { "user_id": 4321 }`
- [ ] `/account/view?uid=1002`
- [ ] `/avatar/user123.png`
- [ ] `/auth/verify?user=me@example.com`
- [ ] Mobile app endpoints: `GET /api/v2/user/me`
- [ ] Changing `user_id` in JWT payload
- [ ] `/api/users/1234/password/change`

---

## Files & Resources
- [ ] `/files/download/1234`
- [ ] `/documents/5678/view`
- [ ] `/images/uploads/avatar_4321.jpg`
- [ ] `/pdfs/statement?id=9876`
- [ ] `/invoices/1009.pdf`
- [ ] Download endpoint: `GET /download?id=report_final`
- [ ] Shared links: `/file?id=abcdef123456`
- [ ] `/api/files/filename.ext`
- [ ] Upload preview endpoints with `file_id`
- [ ] `/backup.zip` with `file=param`

---

## Messaging & Communication
- [ ] `/messages?id=4532`
- [ ] `/api/chat/room/908`
- [ ] `GET /api/messages/thread?id=1001`
- [ ] Changing thread/message ID in body payload
- [ ] `/api/conversations/user/100`
- [ ] `PUT /message/update?id=458`
- [ ] `/notifications/view?id=222`
- [ ] `/support/tickets?id=3111`
- [ ] `/email?id=sent_email_123`
- [ ] `/feedback/view?id=9009`

---

## Orders, Payments & Cart Items
- [ ] `/orders/view?id=9999`
- [ ] `/api/cart/item/123`
- [ ] `/checkout?id=order001`
- [ ] `POST /cancel_order { "order_id": "ORD-101" }`
- [ ] `/invoices?id=inv-9090`
- [ ] `/payment/status?txn_id=abc123`
- [ ] `/subscription/edit?id=sub102`
- [ ] `/download_invoice?uid=1002`
- [ ] `/refund?id=trans_002`
- [ ] `/api/receipts/view/receipt_101`

---

## Admin & Multi-Tenant Misconfigurations
- [ ] `/admin/users?id=basic_user_id`
- [ ] `/tenant/data?org_id=ACME001`
- [ ] `/api/clients?id=clientXYZ`
- [ ] `/dashboard?client_id=1122`
- [ ] `/reports/view?id=report_id`
- [ ] `/departments/edit?id=3`
- [ ] `/project/manage?id=projectA`
- [ ] `/api/internal/users/list?uid=abc123`
- [ ] `/team/edit_member?user=guest01`
- [ ] `/audit/logs?id=some_other_user`

---

## Testing Notes
- [ ] Test for both **GET** and **POST** parameters.
- [ ] Fuzz numeric IDs (`+1`, `-1`, `9999`), UUIDs, usernames, slugs, emails.
- [ ] Use **two user accounts** for differential testing.
- [ ] Always check **response data leakage**, access controls, or state changes.
- [ ] Look out for **mass assignment** or **forced browsing**.

---
Base Steps:
```bash
1. Create two accounts if possible or else enumerate users first. 
2. Check if the endpoint is private or public and does it contains any kind of id param.
3. Try changing the param value to some other user and see if does anything to their account.
4. Done !!
```

[ ]
[ ] image profilie
[ ] delete acount 
[ ] infromation acount
[ ] VIEW & DELETE & Create api_key
[ ] allows to read any comment
[ ] change price
[ ] chnage the coin from dollar to uaro
[ ] Try decode the ID, if the ID encoded using md5,base64,etc
```html
GET /GetUser/dmljdGltQG1haWwuY29t
[...]
```

[ ] change HTTP method
```bash
GET /users/delete/victim_id  ->403
POST /users/delete/victim_id ->200
```

[ ] Try replacing parameter names
```bash
Instead of this:
GET /api/albums?album_id=<album id>

Try This:
GET /api/albums?account_id=<account id>

Tip: There is a Burp extension called Paramalyzer which will help with this by remembering all the parameters you have passed to a host.
```

[ ] Path Traversal
```bash
POST /users/delete/victim_id          ->403
POST /users/delete/my_id/..victim_id  ->200
```

[ ] change request content-type
```bash
Content-Type: application/xml ->
Content-Type: application/json
```

[ ] swap non-numeric with numeric id
```bash
GET /file?id=90djbkdbkdbd29dd
GET /file?id=302
```

[ ] Missing Function Level Acess Control 
```bash
GET /admin/profile ->401
GET /Admin/profile ->200
GET /ADMIN/profile ->200
GET /aDmin/profile ->200
GET /adMin/profile ->200
GET /admIn/profile ->200
GET /admiN/profile ->200
```

[ ]send wildcard instead of an id
```bash
GET /api/users/user_id ->
GET /api/users/*
```

[ ] Never ignore encoded/hashed ID
```bash
for hashed ID ,create multiple accounts and understand the ppattern application users to allot an iD
```

[ ] Google Dorking/public form
```bash
search all the endpoints having ID which the search engine may have already indexed
```

[ ] Bruteforce Hidden HTTP  parameters
```bash
use tools like arjun , paramminer 
```

[ ] Bypass object level authorization Add parameter onto the endpoit if not present by defualt
```bash
GET /api_v1/messages ->200
GET /api_v1/messages?user_id=victim_uuid ->200
```

[ ] HTTP Parameter POllution Give mult value for same parameter
```bash
GET /api_v1/messages?user_id=attacker_id&user_id=victim_id
GET /api_v1/messages?user_id=victim_id&user_id=attacker_id
```

[ ] change file type
```bash
GET /user_data/2341        -> 401
GET /user_data/2341.json   -> 200
GET /user_data/2341.xml    -> 200
GET /user_data/2341.config -> 200
GET /user_data/2341.txt    -> 200
```

[ ] json parameter pollution
```bash
{"userid":1234,"userid":2542}
```

[ ] Wrap the ID with an array in the body
```bash
{"userid":123} ->401
{"userid":[123]} ->200
```

[ ] wrap the id with a json object
```bash
{"userid":123} ->401
{"userid":{"userid":123}} ->200
```

[ ] Test an outdata API version 
```bash
GET /v3/users_data/1234 ->401
GET /v1/users_data/1234 ->200
```

[ ] If the website using graphql, try to find IDOR using graphql!
```bash
GET /graphql
[...]
```
```html
GET /graphql.php?query=
[...]
```
