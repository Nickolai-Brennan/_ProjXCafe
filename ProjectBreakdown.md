# ☕ PROJX CAFE — Product Breakdown

## Core Concept

A social task marketplace + profile-based platform where:

* Users post projects
* Other users complete micro-tasks
* Payment via membership credits + tips
* Approval-based fund release
* XP system rewards task creators

---

# 1️⃣ ACCOUNT SYSTEM

### Issues

* [feature] User authentication (email + OAuth)
* [feature] Membership tier system
* [feature] Credit wallet system
* [feature] XP tracking system
* [feature] Profile page (public view)

### Acceptance Criteria

* Wallet balance visible
* XP visible on profile
* Tier affects credit allowances
* Transaction history accessible

---

# 2️⃣ PROFILE SYSTEM

### Issues

* [feature] Public profile page
* [feature] Skills + tags system
* [feature] Portfolio project posting
* [feature] Reputation rating system
* [feature] Social activity feed

### Profile Must Show

* Projects
* Completed tasks
* XP level
* Reviews
* Skill badges

---

# 3️⃣ PROJECT POSTING SYSTEM

### Issues

* [feature] Create project listing
* [feature] Add task to project
* [feature] Attach files
* [feature] Set credit amount
* [feature] Optional tip pool

### Fields Required

* Title
* Description
* Deliverable type
* Time estimate (ex: 30 min)
* Credit amount
* Approval window
* Required skills

---

# 4️⃣ TASK EXECUTION FLOW

### Issues

* [feature] Task claim system
* [feature] Submission upload system
* [feature] Revision request system
* [feature] Approval / reject flow
* [feature] Auto-release escrow

### Workflow

1. Task posted
2. User claims
3. User submits
4. Creator approves
5. Credits released
6. XP granted

---

# 5️⃣ PAYMENT + CREDIT ENGINE

### Issues

* [feature] Escrow credit locking
* [feature] Tip functionality
* [feature] Membership credit top-ups
* [feature] Stripe integration
* [feature] Withdrawal request system

### Rules

* Credits locked when task claimed
* Released on approval
* Tips add bonus payout
* Creator receives XP
* Worker receives credits

---

# 6️⃣ XP SYSTEM (Gamification Layer)

### Issues

* [feature] XP logic model
* [feature] XP levels + badges
* [feature] XP reward rules
* [feature] Leaderboard page

### XP Model Example

* Posting project: +10 XP
* Approving task: +5 XP
* Completing task: +X XP
* High rating bonus: +XP multiplier

---

# 7️⃣ MARKETPLACE DISCOVERY

### Issues

* [feature] Category filtering
* [feature] Skill-based filtering
* [feature] “30 minute tasks” quick filter
* [feature] Trending tasks
* [feature] Recommended tasks

---

# 8️⃣ MODERATION + TRUST

### Issues

* [feature] Dispute resolution system
* [feature] Flag/report system
* [feature] Manual admin override
* [feature] Rating fraud detection
* [feature] Timeout auto-cancel system

---

# 9️⃣ SOCIAL LAYER

### Issues

* [feature] Activity feed
* [feature] Follow users
* [feature] Comment system
* [feature] Project updates
* [feature] Achievement posts

---

# 🔟 ADMIN DASHBOARD

### Issues

* [feature] User management panel
* [feature] Transaction audit log
* [feature] Credit system controls
* [feature] XP rule editor
* [feature] Content moderation panel

---

# 🔁 SYSTEM ARCHITECTURE ISSUES

### Backend

* User service
* Wallet service
* Task service
* XP service
* Notification service

### Frontend

* Profile UI
* Task board UI
* Submission modal
* Wallet dashboard
* XP progress component

---

# 🔥 Critical MVP Path

If building lean:

1. Auth
2. Profile
3. Post task
4. Claim task
5. Submission upload
6. Approval → credit release
7. Basic XP counter

Everything else = phase 2+

---

If you want, I can next:

* Design database schema (Postgres)
* Map API routes (REST or GraphQL)
* Design escrow logic model
* Create GitHub milestone phases
* Or build MVP folder structure (frontend + backend)

Where do you want to go next?
