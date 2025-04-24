# Task 5: Post-Migration Validation

## Objective

Verify that each repository migrated to the GitHub Enterprise organization (`emu-labs-org`) is functionally identical to its source. This includes confirming repository history, access controls, integrations, CI/CD pipelines, and developer tooling compatibility.

---

## Validation Scope

| Area                | Checks Performed                        |
|---------------------|-----------------------------------------|
| Git History         | Branches, tags, commit logs             |
| Permissions         | Team access, visibility, collaborators  |
| CI/CD               | GitHub Actions, webhooks                |
| Secrets             | Encrypted repo secrets via `gh` CLI     |
| Tooling Integration | Slack, Jenkins, Docker, Codecov         |

---

## Step-by-Step Checklist

### 1. Validate Commit History

```bash
git clone https://github.com/emu-labs-org/demo-service-api.git
cd demo-service-api
git log --oneline --graph
```

Expected Output:
- Matches original repo (`gh-source-demo`)
- No history loss or rebase artifacts

---

### 2. Validate Branches and Tags

```bash
git branch -a
git tag
```

Confirm that:
- `main` and any feature branches are intact
- All version tags (e.g., `v1.0.0`, `v2.0.1`) are present

---

### 3. Validate GitHub Actions Workflow Execution

View in GitHub UI under:
```
https://github.com/emu-labs-org/demo-service-api/actions
```

Or trigger manually:

```bash
gh workflow run build.yml --repo emu-labs-org/demo-service-api
```

Expected:
- Build completes successfully
- Artifacts (if any) are generated
- Secrets are consumed without error

---

### 4. Validate Access Control

Go to:
```
https://github.com/emu-labs-org/demo-service-api/settings/access
```

Check:
- Only enterprise team members (`devops-team`, `security-reviewers`) have access
- No external collaborators remain
- Branch protection rules enforced

---

### 5. Validate Webhook and Integration Firing

Push a test commit to the main branch:

```bash
echo "# test" >> README.md
git add README.md
git commit -m "Post-migration test push"
git push origin main
```

Monitor webhook or Slack/Jenkins endpoint logs for trigger confirmation.

---

## Final Validation Outcome

| Validation Area     | Status   | Notes                              |
|---------------------|----------|-------------------------------------|
| Commit History      | Success  | All commits and authors preserved  |
| Branches & Tags     | Success  | Verified against source repo        |
| CI/CD Execution     | Success  | Workflows triggered successfully    |
| Permissions & Teams | Success  | Enforced via org-level setup        |
| Webhooks            | Success  | All external integrations responded |

---

## Result

Repositories are validated and stable. The organization is now ready for EMU-style identity enforcement, automated provisioning, and SSO enablement (documented in subsequent tasks).

---
