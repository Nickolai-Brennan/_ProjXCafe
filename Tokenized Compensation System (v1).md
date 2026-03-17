# ☕ CAFE — Tokenized Compensation System (v1)

## 1. Core Problem (What We’re Fixing)

Your current model:

* You pay developers **$5 / 30 min out of pocket**
* Users don’t pay upfront
* Risk = **you burn cash fast with no guarantee of recovery**

This will fail at scale.

👉 Solution: introduce a **controlled internal token + credit economy**

---

# 2. Currency Structure (3-Layer System)

## A. Platform Credits (Internal Currency)

**Name:** Cafe Credits (CC)

* 1 CC = $1 (pegged internally, NOT withdrawable)
* Users must **purchase credits to request work**
* Credits are **held during job lifecycle**

---

## B. Earned Tokens (Developer Earnings)

**Name:** Builder Tokens (BT)

* Developers earn BT when completing tasks
* BT can be:

  * Converted → Cash (with fee)
  * Used → Platform perks (boosts, visibility, tools)

---

## C. Reputation Layer (Non-Financial)

**Name:** XP / Trust Score

* Earned from:

  * Completed jobs
  * Ratings
  * Verified GitHub work 
* Impacts:

  * Job access
  * Priority payouts
  * Dispute weighting

---

# 3. Revised Payment Flow (Critical Fix)

## Step-by-Step

### 1. User Posts Job

* First 1000 users → free posting (growth lever)
* Must still **fund job before assignment**

---

### 2. Budget Lock (Escrow System)

User selects:

* Estimated time (ex: 2 hours)
* System calculates:

  * 2 hours = 4 units (30 min blocks)
  * Cost = 4 × $5 = **$20 = 20 CC**

👉 User must deposit **20 CC upfront**

---

### 3. Platform Holds Funds

* Credits move to:
  → `locked_wallet`

* Cannot be withdrawn or reused

* Guarantees developer payment

---

### 4. Developer Works

* Time tracked in **30-min increments**
* Max payout capped by locked amount

---

### 5. Completion + eDoc Sign

Both parties:

* Approve → funds released
* Reject → dispute triggered

---

### 6. Payout Logic

Instead of you paying:

* Platform releases **locked credits → Developer**

Conversion:

* 20 CC → 20 BT

---

### 7. Developer Withdrawal

Options:

* Cash out:

  * 20 BT → $16 (20% platform fee)
* Keep as BT:

  * Boost profile
  * Buy tools
  * Priority job placement

---

# 4. Your Revenue Model (Now Safe)

## A. Monthly Dev Subscription

* $10/month (as you planned)

---

## B. Credit Purchase Margin

Example:

* User buys 100 CC for $105
* You keep $5 margin

---

## C. Withdrawal Fee

* 15–25% fee on BT → USD

---

## D. Optional Add-ons

* Job boosting
* Featured profiles
* Faster dispute resolution

---

# 5. Why This Works

## You eliminate:

* ❌ Paying devs out of pocket
* ❌ Unlimited liability
* ❌ Abuse from free users

## You gain:

* ✅ Guaranteed funding before work starts
* ✅ Predictable margins
* ✅ Scalable system

---

# 6. Tip System (Keep Yours, but Structured)

After completion:

User can:

* Tip in CC

Flow:

* Tip CC → converts to BT → goes to dev

Optional:

* Platform takes 5–10% tip fee

---

# 7. Dispute System (Critical for Trust)

## If user rejects work:

Trigger:
→ `dispute_case`

### Resolution Options

1. **Partial Release**

   * % of credits paid out

2. **Expert Review Pool**

   * High XP users review work

3. **Redo Window**

   * Developer gets revision chance

---

## Funding Safety

Even in dispute:

* Funds are already locked
* No risk to platform

---

# 8. Time-Based Pay (Refined Version)

Instead of manual tracking:

## Use “Work Units”

* 1 Unit = 30 minutes = 5 CC

System enforces:

* Pre-selected units
* Prevents time inflation

---

# 9. Database Layer (Simplified)

## wallets

```sql
user_id
balance_cc
balance_bt
locked_cc
```

## transactions

```sql
id
user_id
type (purchase, lock, release, tip, withdraw)
amount
currency (CC, BT, USD)
status
created_at
```

## jobs

```sql
id
creator_id
developer_id
units_reserved
total_cc_locked
status
```

## payouts

```sql
id
developer_id
bt_amount
usd_amount
fee
status
```

---

# 10. Guardrails (Prevent Abuse)

## Required:

* Minimum job funding (ex: 2 units = $10)
* Max units per job (MVP cap)
* Rate limits on disputes
* Developer tier unlocks higher jobs

---

# 11. Strategic Adjustment (Important)

### DO NOT:

Pay developers directly from company funds

### DO:

Act as:
→ **Settlement Layer + Marketplace**

You:

* Hold funds
* Distribute funds
* Take fees

---

# 12. Positioning (Investor / Legal Safe)

Do NOT say:
❌ “We pay developers”

Say:
✅ “Users fund jobs via platform credits, which are released upon completion”

---

# 13. Optional Upgrade (Future)

* Dynamic pricing (higher XP = higher rate)
* Auction-based jobs
* Subscription credit bundles
* AI-estimated job pricing

---

# 14. Final System Summary

User:

* Buys credits
* Funds job

Platform:

* Holds funds
* Enforces rules
* Takes fees

Developer:

* Completes work
* Earns tokens
* Cashes out

---

If you want next step:
I can design:

* Full **PostgreSQL wallet + transaction schema**
* API routes (`/wallet`, `/jobs/lock`, `/payouts`)
* UI flows (job funding modal, payout dashboard)

Or go deeper into:
👉 fraud prevention + financial compliance (this is where most platforms fail)
