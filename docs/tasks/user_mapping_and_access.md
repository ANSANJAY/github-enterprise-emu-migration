# Task 9: User Mapping and Access Transition

## Objective

Simulate the transition of unmanaged GitHub user identities to GitHub Enterprise Managed Users (EMU). This includes mapping legacy contributors to new SAML/SCIM identities and transferring their access through team-based permissions.

---

## Inputs and Sources

- Audit data from: `docs/tasks/repository_audit.md`
- Identity mappings compiled in: `docs/identity_mapping.csv`
- GitHub teams created in: `docs/tasks/target_org_setup.md`

---

## Identity Mapping Example

Saved in: `docs/identity_mapping.csv`

| GitHub Username     | New EMU Identity               | Assigned Team       |
|---------------------|--------------------------------|----------------------|
| johnsmith           | johnsmith@emulabsdemo.com      | devops-team          |
| anamikasanjay       | anamika@emulabsdemo.com        | security-reviewers   |
| legacy-collab       | decommissioned (access removed)| none                 |

---

## Step-by-Step: Team-Based Access Setup

### 1. Add EMU Users to GitHub Teams

```bash
gh api \
  -X PUT /orgs/emu-labs-org/teams/devops-team/memberships/johnsmith@emulabsdemo.com \
  -f role='member'

gh api \
  -X PUT /orgs/emu-labs-org/teams/security-reviewers/memberships/anamika@emulabsdemo.com \
  -f role='member'
```

---

### 2. Remove Legacy GitHub Users from Repos

```bash
gh api \
  -X DELETE /repos/emu-labs-org/demo-service-api/collaborators/legacy-collab
```

**Output:**

```
204 No Content — Collaborator successfully removed
```

---

### 3. Validate Team Membership and Repo Access

```bash
gh api /orgs/emu-labs-org/teams/devops-team/members
gh api /repos/emu-labs-org/demo-service-api/collaborators
```

---

## Post-Migration Access Review

| User                    | Access Method            | Access Level |
|-------------------------|--------------------------|--------------|
| johnsmith@emulabsdemo.com | Team-based via SAML SSO | Write        |
| anamika@emulabsdemo.com   | Team-based via SAML SSO | Read         |
| legacy-collab             | Removed                 | None         |

---

## Result

Legacy unmanaged GitHub users are fully transitioned to managed EMU identities (simulated). Access is scoped strictly through teams, in alignment with enterprise access control practices.

---

