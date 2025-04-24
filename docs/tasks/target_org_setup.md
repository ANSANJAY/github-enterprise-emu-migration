# Task 2: Target Organization Setup

## Objective

Create and configure a GitHub Enterprise organization (`emu-labs-org`) under the Enterprise EMU account (`emu-testing`). Define role-based teams, assign access levels, and prepare the org for secure repo hosting and user governance.

---

## Environment Details

- GitHub Enterprise: `emu-testing`
- GitHub Organization: `emu-labs-org`
- GitHub CLI Version: 2.45.0
- Admin User: `test1emu_admin`

---

## Step-by-Step Execution

### Step 1: Create the Organization

Executed under the `emu-testing` Enterprise:

```bash
gh api --method POST /admin/organizations \
  -f login='emu-labs-org' \
  -f admin='test1emu_admin' \
  -f profile_name='EMU Labs Org' \
  -H "Accept: application/vnd.github+json"
```

> Note: Enterprise org creation requires SAML setup. For this simulation, org was created under a GitHub Enterprise trial account (non-EMU locked) to simulate downstream behavior.

---

### Step 2: Create Teams Within the Organization

```bash
gh api \
  -X POST /orgs/emu-labs-org/teams \
  -f name='devops-team' \
  -f privacy='closed'

gh api \
  -X POST /orgs/emu-labs-org/teams \
  -f name='security-reviewers' \
  -f privacy='closed'

gh api \
  -X POST /orgs/emu-labs-org/teams \
  -f name='admin-engineering' \
  -f privacy='closed'
```

**Sample Response:**

```json
{
  "name": "devops-team",
  "slug": "devops-team",
  "permission": "pull"
}
```

---

### Step 3: Add Team Members (Manual or Scripted)

```bash
gh api \
  -X PUT /orgs/emu-labs-org/teams/devops-team/memberships/anamikasanjay \
  -f role='member'

gh api \
  -X PUT /orgs/emu-labs-org/teams/security-reviewers/memberships/johnsmith \
  -f role='member'
```

---

### Step 4: Configure Default Repo Settings

```bash
gh api \
  -X PATCH /orgs/emu-labs-org \
  -f default_repository_permission='read' \
  -f members_can_create_repositories='false' \
  -H "Accept: application/vnd.github+json"
```

---

## Visual Confirmation (Simulated)

- Teams visible in GitHub UI under `https://github.com/orgs/emu-labs-org/teams`
- Members assigned via CLI and visible under each team

---

## Notes

- Teams align with least-privilege design: devops, security, admins
- Default org policy prevents new repo creation without approval
- Further access control is defined during repository migration and policy enforcement

