
## Abuse of Workflow & Multi-step Processes
- [ ] Skipping payment step via direct request
- [ ] Skipping identity verification (KYC bypass)
- [ ] Tampering with checkout flow via dev tools or proxy
- [ ] Accessing final-step URLs directly without completing prior steps
- [ ] Modifying multi-factor authentication (MFA) logic
- [ ] Assigning elevated roles during onboarding or invite
- [ ] Abusing broken redirects to bypass authentication/logic
- [ ] Directly submitting form data to bypass frontend checks
- [ ] Submitting steps in an unintended order (e.g., Step 3 before Step 1)
- [ ] Repeating the same step multiple times to cause denial-of-service or overwrite

## Pricing & Discount Abuse
- [ ] Price manipulation via parameter tampering
- [ ] Swapping product ID with cheaper one during checkout
- [ ] Reusing expired or one-time-use coupons
- [ ] Applying multiple coupons when only one is allowed
- [ ] Setting product price or quantity to 0 or negative
- [ ] Exploiting free shipping with altered address/weight
- [ ] Using test/staging environment coupon codes in production
- [ ] Tampering currency/rounding values to cause pricing bugs
- [ ] Abusing reward points or loyalty program for infinite credits
- [ ] Creating fake referrals or self-referrals

##  Payment & Financial Logic Flaws
- [ ] Triggering a refund larger than original payment
- [ ] Double refund by replaying the refund request
- [ ] Buying expensive item using cheaper product ID
- [ ] Changing account info (email/phone) during payment redirect
- [ ] Wallet underflow/overflow attacks
- [ ] Grace period abuse to avoid charges/subscription lock
- [ ] Directly interacting with backend payment APIs
- [ ] Gaining full access after partial payment
- [ ] Exploiting race conditions in purchase/booking APIs
- [ ] Reusing tokens or payloads after logical invalidation

##  Account, Roles & Access Escalation
- [ ] Role escalation via account update (e.g., `role=admin`)
- [ ] Switching user IDs during account linking/invite
- [ ] Accessing premium/paid features post-upgrade without paying
- [ ] Creating duplicate admin accounts using flawed invite logic
- [ ] Self-inviting to privileged roles
- [ ] Guest checkout bypassing user restrictions
- [ ] Accessing deleted/archived user data or orders
- [ ] Changing username/email to impersonate others
- [ ] Exploiting flawed social login logic for identity takeover
- [ ] Deleting accounts to trigger refund or credit abuse

##  State Manipulation & Trust Violations
- [ ] Replaying the same transaction to duplicate purchases/rewards
- [ ] Tampering with timestamps to unlock expired features
- [ ] Unlocking premium features via JS function calls or localStorage
- [ ] Sending multiple simultaneous requests to bypass limits
- [ ] Changing app state client-side and syncing with backend
- [ ] Trusting user-controlled values for privilege logic (`is_admin: true`)
- [ ] Using inactive or legacy promo codes
- [ ] Bypassing bans/suspensions through client-side controls
- [ ] Faking task completions to earn rewards (e.g., “watch ad”)
- [ ] Abusing APIs or endpoints exposed from staging/internal builds

# Extra Areas to Consider
- [ ] Feature abuse (e.g., modifying drafts to skip moderation)
- [ ] Rate limit and quota bypass
- [ ] Leaderboard manipulation or fake achievements
- [ ] File upload abuse via import flows (JSON, CSV)