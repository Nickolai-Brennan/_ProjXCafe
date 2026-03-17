# ☕ PROJXCAFE — UI/UX SYSTEM BREAKDOWN

---

# 1️⃣ DUAL PROFILE SYSTEM (Core UX Concept)

## Concept

Single profile with **mode toggle**:

* 🧑‍💻 Builder Mode (doing work)
* 📌 Client Mode (posting work)

UI flips context, not structure.

---

## 🧩 GitHub Issues

### [feature] Dual profile mode toggle

* Toggle: `Builder | Client`
* Persist preference per session
* AC:

  * Same layout, different data modules
  * No page reload (state-driven)

---

## 🧑‍💻 BUILDER PROFILE UI

### Sections

#### 1. Header Card

* Profile Image
* Username
* Satisfaction Score (⭐ 4.8)
* Completed Side Jobs (#)
* Skill Level badge (Beginner / Pro / Elite)

---

#### 2. “Currently Working On”

* Active tasks (cards)
* Status tags: `In Progress`, `Submitted`, `Waiting Approval`

---

#### 3. Expertise (Button Grid)

* Frontend
* Backend
* Database
* Design
* AI
* Marketing

👉 Click = filter profile + match engine

---

#### 4. Tools & Familiarity

Tag-based system:

* React
* FastAPI
* PostgreSQL
* Canva
* ChatGPT
* Figma

With levels:

* ● Basic
* ●● Intermediate
* ●●● Advanced

---

#### 5. Portfolio / Completed Work

* Cards with:

  * Task title
  * Time to complete
  * Rating received
  * Earnings

---

#### 6. CTA Panel

* 💬 Message Me Now (floating or sticky)
* ⭐ Hire Me / Invite to Task

---

## 📌 CLIENT PROFILE UI

Same structure, different modules:

---

### Key Differences

#### Instead of “Completed Tasks”

→ Shows:

* Projects Posted
* Tasks Created
* Total Credits Spent

---

#### Instead of “Tools”

→ Shows:

* Preferred Tools Stack
* Requirements they typically request

---

#### Additional Section

##### “Approval Behavior”

* Avg approval time
* Revision rate
* Satisfaction score (as client)

---

## 🧩 GitHub Issues

* [feature] Profile header card component
* [feature] Expertise tag system (clickable filters)
* [feature] Tool familiarity tagging system
* [feature] Portfolio / completed task cards
* [feature] Client metrics module (projects, spend, approval time)
* [feature] Sticky “Message Me Now” chat CTA

---

# 2️⃣ MAIN HOME PAGE (Marketplace Feed)

## Concept

Hybrid of:

* Reddit (feed)
* eBay (marketplace)
* Fiverr (tasks)

---

## Layout

### 🔝 Top Banner (Scrolling)

* Announcements
* Rewards
* “Flash Builds” (limited-time tasks)

👉 Horizontal auto-scroll

---

### 🔍 Filter Bar

* Search (tasks, users)
* Filters:

  * Time (15 min / 30 min / 1 hr)
  * Skill (Frontend, Backend, etc.)
  * Tools (React, etc.)
  * Budget (credits)

---

### 📜 Main Feed

Card-based tasks:

Each card shows:

* Title
* Time estimate (⏱ 30 min)
* Credits reward
* Tools required
* Skill tags
* Posted by (mini profile)
* Urgency badge

---

### 🧠 Smart Highlights

* “Recommended for you”
* “Quick cash tasks”
* “High XP tasks”

---

## 🧩 GitHub Issues

* [feature] Scrolling announcement banner
* [feature] Task feed (card-based)
* [feature] Filter/search system
* [feature] Recommendation engine (basic first)
* [feature] “Quick tasks” highlight row

---

# 3️⃣ PROJECT POST UI (Critical UX)

## Goal

Fast, structured, zero confusion for builder.

---

## Flow

### Step 1 — Basic Info

* Title
* Description
* Time estimate
* Credits offered

---

### Step 2 — Tools & Stack (KEY FEATURE)

Selectable tags:

* React
* FastAPI
* Canva
* WordPress
* etc.

👉 REQUIRED (core to your vision)

---

### Step 3 — Deliverable Type

* Fix
* Build
* Design
* Research
* Content

---

### Step 4 — Upload / Reference

* Files
* Links
* Screenshots

---

### Step 5 — Approval Rules

* Auto-approve after X hours?
* Revision limit

---

### Step 6 — Preview Card (looks like marketplace card)

---

## 🧩 GitHub Issues

* [feature] Multi-step project creation wizard
* [feature] Tool selection system (required field)
* [feature] Deliverable type selector
* [feature] File upload system
* [feature] Approval rules config
* [feature] Live preview card

---

# 4️⃣ TASK EXECUTION UI

---

## Builder Side

### Task View Page

* Full description
* Tools required (highlighted)
* Files
* Chat panel (right side)
* Submit button

---

### Submission Modal

* Upload work
* Add notes
* Mark complete

---

## Client Side

### Review Screen

* Submission preview
* Accept / Request revision / Reject
* Tip input
* Rating selector

---

## 🧩 GitHub Issues

* [feature] Task detail page UI
* [feature] Submission modal
* [feature] Client review panel
* [feature] Tip + rating UI

---

# 5️⃣ CHAT / COMMUNICATION

---

## UI

* Floating chat button
* Real-time messages
* Attached to:

  * Profile
  * Task
  * Project

---

## 🧩 GitHub Issues

* [feature] Real-time chat system
* [feature] Chat drawer UI
* [feature] Context-aware chat (task-linked)

---

# 6️⃣ XP + GAMIFICATION UI

---

## Components

* XP progress bar (profile header)
* Level badge
* Achievement popups
* Leaderboard page

---

## 🧩 GitHub Issues

* [feature] XP progress component
* [feature] Badge system UI
* [feature] Leaderboard page

---

# 7️⃣ DESIGN SYSTEM REQUIREMENTS (IMPORTANT)

---

## Visual Style

* Clean cards (border + soft shadow)
* Tag-based UI (chips)
* Dense info, minimal clutter
* Fast scanning (key metric icons)

---

## Required Components

* Card
* Tag / Chip
* Badge
* Button variants
* Modal
* Drawer (chat)
* Tabs (profile switch)

---

## 🧩 GitHub Issues

* [design] Core component library (cards, tags, badges)
* [design] Light/dark theme system
* [design] Responsive mobile layout

---

# 🔥 MVP UI PRIORITY

If you strip this down to launch:

1. Profile (basic dual mode)
2. Task feed
3. Post project wizard
4. Task page + submit
5. Approval + credit release
6. Chat (simple)

---

# 🧠 Key UX Insight (Your Edge)

Your strongest differentiator:

👉 **Tool-aware tasks + builder skill matching**

This should be:

* Required in posting
* Highlighted in UI
* Used in matching

---

If you want next:

* I can design exact wireframes (screen-by-screen)
* Or generate React component structure (Next.js + Tailwind)
* Or map this into a full frontend folder architecture

Pick one.
