
## Identify places where concurrent requests may lead to business logic abuse or unexpected behavior

---

## Financial & Transaction-Based Points
- [ ] Coupon redemption endpoints (`/redeem-coupon`)
- [ ] Wallet top-up or withdraw (`/wallet/withdraw`)
- [ ] Payment confirmation or checkout (`/checkout/pay`)
- [ ] Refund process (`/refund`)
- [ ] Reward claim (`/claim-reward`)
- [ ] Point conversion (e.g., points → cash)
- [ ] Bank transfer initiation (`/bank/transfer`)
- [ ] Discount application logic
- [ ] Buy-one-get-one or loyalty logic
- [ ] Auction bid/claim functionality

---

## Account & User Actions
- [ ] Account registration (`/signup`)
- [ ] Email/phone verification endpoints
- [ ] Password change (`/change-password`)
- [ ] OTP validation or resend (`/verify-otp`)
- [ ] MFA reset or rebind actions
- [ ] Subscription start/stop toggle
- [ ] User role change or upgrade
- [ ] User deletion (`/delete-account`)
- [ ] Referral bonus claiming (`/referral/claim`)
- [ ] User profile update race

---

## Token, Session & Code Logic (21–30)
- [ ] Session invalidation (`/logout`)
- [ ] API key regeneration (`/regenerate-key`)
- [ ] Token-based redemption (e.g., `/activate`)
- [ ] OTP consumption (`/verify-otp`)
- [ ] Password reset token usage
- [ ] Magic login link usage
- [ ] Access token refresh flow
- [ ] Download link or pre-signed URL access
- [ ] Email link-based verification logic
- [ ] Invite link logic (`/accept-invite`)

---

## Inventory & Stock-Based Operations (31–40)
- [ ] Product purchase when stock is low
- [ ] Cart quantity manipulation
- [ ] Inventory reservation system
- [ ] Flash sale logic (`/buy-now`)
- [ ] Out-of-stock bypass attempt
- [ ] Limited edition item purchase
- [ ] Waitlist bypass
- [ ] Stock allocation race during checkout
- [ ] Pre-order claim
- [ ] Booking slot (seat/room/ticket) race

---

## Order & Workflow Race Conditions
- [ ] Order confirmation (`/confirm-order`)
- [ ] Order cancellation (`/cancel-order`)
- [ ] Shipping/billing info update
- [ ] Order status update endpoints
- [ ] File upload + process (e.g., image + resize)
- [ ] Resource deletion and access
- [ ] Multi-stage form submission
- [ ] Service subscription activation
- [ ] Purchase + Refund at same time
- [ ] API for creating + deleting the same resource

---

## Pro Tips
- [ ] Test using Burp's Intruder/Repeater + parallel threads
- [ ] Test with Turbo Intruder / racepwn / sniper.py
- [ ] Validate if backend uses `lock`, `mutex`, or async queues
- [ ] Look for non-idempotent operations (`POST`/`PUT`)
- [ ] Test high-value operations under slow/laggy network

---
