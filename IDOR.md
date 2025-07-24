
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
