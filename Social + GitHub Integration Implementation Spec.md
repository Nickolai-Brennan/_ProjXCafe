# ☕ CAFE — Social + GitHub Integration Implementation Spec

## 1. Feature Overview

Cafe should support two parallel external identity layers:

* **Social Accounts** for trust, reach, and profile enrichment
* **GitHub Integration** for technical proof-of-work and project collaboration

This makes Cafe profiles feel credible, active, and useful beyond the platform itself.

---

# 2. Integration Scope

## Social Integrations

Initial support:

* GitHub
* LinkedIn
* X
* Discord
* Personal website

These should begin as **profile link + account connection** features, not deep publishing systems.

## GitHub Integration

Initial support:

* GitHub OAuth login/connect
* Read connected profile metadata
* Attach repos to user profile
* Attach repo/issue/PR links to projects and tasks
* Store submission proof using PR, commit, or issue reference

---

# 3. System Modules

## A. Auth + Connected Accounts Module

Responsible for:

* OAuth connection flow
* token storage
* account sync state
* disconnect / revoke logic

## B. Profile Enrichment Module

Responsible for:

* displaying connected platforms
* showing public links
* showing GitHub-backed project proof
* verification badges

## C. Project Linkage Module

Responsible for:

* attaching external resources to projects
* mapping GitHub repos/issues/PRs to Cafe tasks
* validating link formats

## D. Activity + Proof Module

Responsible for:

* storing external contribution evidence
* showing recent GitHub/social-linked activity
* feeding proof into reputation/profile sections

---

# 4. Database Design

## users

Add:

```sql
github_username text null,
website_url text null,
linkedin_url text null,
x_url text null,
discord_handle text null
```

This is optional shortcut data for profile rendering, but actual connected account records should live separately.

---

## connected_accounts

```sql
id uuid primary key,
user_id uuid not null references users(id) on delete cascade,
provider text not null,              -- github, linkedin, x, discord
provider_user_id text not null,
username text null,
display_name text null,
profile_url text null,
avatar_url text null,
access_token_encrypted text null,
refresh_token_encrypted text null,
scope text null,
is_active boolean not null default true,
is_public boolean not null default true,
last_synced_at timestamptz null,
created_at timestamptz not null default now(),
updated_at timestamptz not null default now()
```

### Constraints

```sql
unique(user_id, provider)
unique(provider, provider_user_id)
```

---

## github_repositories

```sql
id uuid primary key,
user_id uuid not null references users(id) on delete cascade,
connected_account_id uuid not null references connected_accounts(id) on delete cascade,
github_repo_id bigint not null,
name text not null,
full_name text not null,
description text null,
repo_url text not null,
is_private boolean not null default false,
primary_language text null,
stars_count int not null default 0,
forks_count int not null default 0,
open_issues_count int not null default 0,
default_branch text null,
last_pushed_at timestamptz null,
is_featured boolean not null default false,
created_at timestamptz not null default now(),
updated_at timestamptz not null default now()
```

### Constraint

```sql
unique(github_repo_id)
```

---

## project_links

```sql
id uuid primary key,
project_id uuid not null references projects(id) on delete cascade,
link_type text not null,             -- github_repo, live_demo, figma, docs, youtube, linkedin, x
title text null,
url text not null,
platform text null,
display_order int not null default 0,
created_at timestamptz not null default now()
```

---

## task_external_links

```sql
id uuid primary key,
task_id uuid not null references tasks(id) on delete cascade,
provider text not null,              -- github
link_type text not null,             -- repo, issue, pr, branch, commit
external_id text null,
url text not null,
metadata jsonb not null default '{}'::jsonb,
created_at timestamptz not null default now()
```

---

## submission_proofs

```sql
id uuid primary key,
submission_id uuid not null references submissions(id) on delete cascade,
proof_type text not null,            -- github_pr, github_commit, github_issue, external_link, file_upload
url text not null,
label text null,
metadata jsonb not null default '{}'::jsonb,
created_at timestamptz not null default now()
```

---

# 5. API Route Map

## Connected Accounts

### POST `/api/integrations/github/connect`

Start GitHub OAuth flow

### GET `/api/integrations/github/callback`

Handle OAuth callback and store connection

### GET `/api/integrations/accounts`

Return user connected accounts

### PATCH `/api/integrations/accounts/:id`

Update visibility or active status

### DELETE `/api/integrations/accounts/:id`

Disconnect account

---

## GitHub Data

### GET `/api/integrations/github/profile`

Fetch synced GitHub profile metadata

### POST `/api/integrations/github/repos/sync`

Pull repositories from GitHub

### GET `/api/integrations/github/repos`

List repos available to attach

### POST `/api/profile/repos`

Attach repo to profile showcase

### DELETE `/api/profile/repos/:id`

Remove repo from showcase

---

## Project Links

### POST `/api/projects/:projectId/links`

Attach external link to project

### GET `/api/projects/:projectId/links`

Get all project links

### DELETE `/api/projects/:projectId/links/:linkId`

Remove project link

---

## Task GitHub Links

### POST `/api/tasks/:taskId/external-links`

Attach issue/PR/repo/branch

### GET `/api/tasks/:taskId/external-links`

List task external links

### DELETE `/api/tasks/:taskId/external-links/:linkId`

Remove link

---

## Submission Proof

### POST `/api/submissions/:submissionId/proofs`

Attach PR/commit/demo proof

### GET `/api/submissions/:submissionId/proofs`

Get proofs for review

---

# 6. Core Workflows

## A. Connect GitHub

1. User clicks “Connect GitHub”
2. OAuth flow starts
3. Callback stores provider identity and tokens
4. Cafe pulls profile metadata
5. GitHub badge appears on profile

### Acceptance criteria

* account connected successfully
* GitHub username saved
* profile link visible
* disconnect supported

---

## B. Attach Repo to Profile

1. Connected user opens profile settings
2. User selects repo from synced list
3. Repo marked as featured
4. Repo card appears on profile

### Acceptance criteria

* only connected user can attach
* repo name, language, stars, updated date visible
* private repos hidden unless explicitly allowed in future scope

---

## C. Link Task to GitHub Issue

1. Creator creates task
2. Creator adds GitHub repo and issue URL
3. Task page shows linked issue
4. Worker sees exact source work item

### Acceptance criteria

* valid GitHub URL required
* issue link visible on task detail
* task can exist without GitHub link

---

## D. Submit Work with PR Proof

1. Worker completes task
2. Worker submits PR URL or commit URL
3. Submission stores proof record
4. Creator reviews proof + deliverable
5. Approval releases credits

### Acceptance criteria

* submission accepts external proof URL
* proof visible in review UI
* multiple proofs allowed

---

# 7. Frontend UI Components

## Profile Page

### Components

* `ConnectedAccountsCard`
* `FeaturedReposGrid`
* `SocialLinksBar`
* `ContributionProofList`
* `ProfileBadges`

### What should show

* platform icons
* connected usernames
* repo cards
* website/portfolio links
* proof-of-work items

---

## Project Detail Page

### Components

* `ProjectLinksPanel`
* `TechStackTags`
* `RepoPreviewCard`
* `ShareProjectBar`

### What should show

* attached repo
* live demo
* docs link
* figma link
* share buttons

---

## Task Detail Page

### Components

* `TaskExternalLinks`
* `GitHubIssueCard`
* `SubmissionProofUploader`
* `ReviewProofPanel`

### What should show

* linked repo/issue
* branch naming note if needed
* PR/commit proof during review

---

## Settings Page

### Components

* `ConnectedAccountsSettings`
* `SocialVisibilityToggles`
* `GitHubRepoSyncPanel`

### What should show

* connect/disconnect actions
* last sync time
* visibility options
* featured repo selector

---

# 8. UX Rules

## Keep it simple

For MVP:

* do not auto-import everything
* do not overload profiles with noisy activity
* let users choose what is shown publicly

## Public vs private

Each account connection should support:

* connected privately
* public on profile
* hidden from profile

## Validation

When users add external links:

* validate domain
* validate format
* normalize URLs before save

---

# 9. Permissions + Security

## OAuth principles

* least privilege first
* read-only scopes first
* write access only later if needed

## Storage rules

* encrypt tokens
* store refresh tokens only when necessary
* support revoke/disconnect
* never expose raw tokens to client

## GitHub privacy

For MVP:

* use public repo metadata only unless broader permissions are intentionally added later

---

# 10. MVP Build Order

## Phase 1

1. Connected accounts table
2. GitHub OAuth connect/disconnect
3. Social links on profile
4. Repo sync and attach-to-profile
5. Project external links
6. Task GitHub issue/PR links
7. Submission proof links

## Phase 2

1. auto-sync activity
2. import issues from repo
3. create GitHub issues from Cafe
4. PR status verification
5. contribution heatmap
6. social composer / sharing automation

---

# 11. GitHub Issues Breakdown

## Auth / Integrations

* [feature] Create connected accounts schema
* [feature] Implement GitHub OAuth flow
* [feature] Store encrypted provider tokens
* [feature] Build account disconnect flow

## Profile

* [feature] Add connected accounts section to profile
* [feature] Add social links bar
* [feature] Add featured GitHub repos section
* [feature] Add profile badges for connected accounts

## Projects / Tasks

* [feature] Attach external links to project
* [feature] Attach GitHub issue/repo links to tasks
* [feature] Validate supported external URLs
* [feature] Add submission proof model

## UI

* [feature] Build connected account settings panel
* [feature] Build repo sync selector
* [feature] Build task proof review panel
* [feature] Build project share bar

---

# 12. Product Definition Update

Cafe is no longer just a task marketplace.
It becomes a **social proof-of-work platform** where users connect identities, attach live projects, and show verified contribution history.

---

# 13. Best Next Deliverable

The most useful next step is a **full Postgres schema + SQL migration file set** for:

* users
* connected_accounts
* github_repositories
* project_links
* task_external_links
* submission_proofs
* indexes and constraints
