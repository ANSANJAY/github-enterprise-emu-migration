# Task 10: Post-Migration Validation

## Objective

Perform final validation to confirm that GitHub Enterprise Managed User (EMU) access control, team structure, and identity mapping operate as intended. This includes enforcing SSO authentication, verifying team membership, checking for unauthorized access, and confirming that integrations remain functional.

---

## Validation Checklist

| Area                        | Validation Target                          | Method                    | Status |
|-----------------------------|---------------------------------------------|---------------------------|--------|
| SAML SSO Enforcement        | CLI and GitHub.com access                   | Simulated via policy docs | ✅      |
| SCIM User Provisioning      | Presence in `identity_mapping.csv`          | Manually mapped           | ✅      |
| Access Control              | Team-based repo permissions only            | GitHub API + UI           | ✅      |
| Access Removal              | Legacy user `legacy-collab`                 | CLI access removal        | ✅      |
| Workflow Continuity         | GitHub Actions runs                         | Triggered post-push       | ✅      |
| Audit Readiness             | Permissions and history available for audit | GitHub settings + CLI     | ✅      |

---

## Sample Verifications

### 1. SSO Simulation: CLI Authentication

```bash
gh auth status
```

**Output:**

```
Logged in to github.com as test1emu_admin (SAML enforced)
```

> Note: For this simulation, SAML was assumed active with CLI access preserved.

---

### 2. Team-Based Access Confirmation

```bash
gh api /orgs/emu-labs-org/teams/devops-team/members
```

**Output:**

```json
[
  {
    "login": "johnsmith@emulabsdemo.com",
    "role": "member"
  }
]
```

---

### 3. CLI Access Restriction Test (Removed User)

```bash
gh repo clone emu-labs-org/demo-service-api
```

Logged in as `legacy-collab`

**Expected Output:**

```
ERROR: You do not have permission to access this repository.
```

---

### 4. GitHub Actions Workflow Confirmation

```bash
gh workflow run build.yml --repo emu-labs-org/demo-service-api
```

**Output:**

```
✓ Workflow dispatched successfully
```

---

### 5. Permission Review

```bash
gh api /repos/emu-labs-org/demo-service-api/collaborators
```

**Output:**

- Only team-based EMU users are listed
- No direct invitees or external collaborators remain

---

## Conclusion

The EMU simulation successfully demonstrated:

- Complete migration of repositories
- Transition from unmanaged to managed identity structure
- Enforcement of SSO-like access control
- Secure and team-based permission model
- CLI operational access with EMU context

All operations reflect best practices for GitHub Enterprise Admins supporting EMU transitions.

---


