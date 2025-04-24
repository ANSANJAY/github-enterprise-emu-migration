# Task 4: Tooling Integration

## Objective

Update all CI/CD pipelines, webhooks, secrets, and automation configurations to point to the newly migrated GitHub Enterprise repositories (`emu-labs-org`). Ensure continuity for builds, deployments, and third-party integrations without impacting existing workflows.

---

## Environment Details

- Source Repositories: `gh-source-demo/demo-service-api`, `monitoring-tool`
- Destination Repositories: `emu-labs-org/demo-service-api`, `monitoring-tool`
- CI Tooling Simulated: GitHub Actions, Jenkins
- Notification Integration: Slack (simulated)
- Auth: GitHub CLI and GitHub Actions secrets

---

## Step-by-Step: CI/CD Pipeline Update

### Step 1: Update GitHub Actions Workflow Paths

Location:
```bash
.github/workflows/build.yml
.github/workflows/deploy.yml
```

Change any hardcoded repo links, branch references, or secrets as needed.

**Sample Edit:**

```yaml
- name: Checkout repo
  uses: actions/checkout@v3
  with:
    repository: emu-labs-org/demo-service-api
```

---

### Step 2: Recreate Repository Secrets

Use GitHub CLI:

```bash
gh secret set DOCKER_USERNAME --body "your-username" --repo emu-labs-org/demo-service-api
gh secret set DOCKER_PASSWORD --body "your-password" --repo emu-labs-org/demo-service-api
```

**Confirmation Output:**

```bash
✓ Set secret DOCKER_USERNAME for repo emu-labs-org/demo-service-api
✓ Set secret DOCKER_PASSWORD for repo emu-labs-org/demo-service-api
```

---

### Step 3: Reconnect Webhooks

If webhooks were used in the source repo (e.g., Slack or Jenkins), fetch them:

```bash
gh api /repos/gh-source-demo/demo-service-api/hooks
```

Recreate the webhook in the destination:

```bash
gh api --method POST /repos/emu-labs-org/demo-service-api/hooks \
  -f config.url='https://jenkins.example.com/github-webhook/' \
  -f config.content_type='json' \
  -f events='["push", "pull_request"]' \
  -f active=true
```

---

### Step 4: Update Jenkins or External CI

In your Jenkinsfile or Jenkins job config:

- Update repo URL:
  ```
  https://github.com/emu-labs-org/demo-service-api.git
  ```
- Update webhook trigger token or GitHub app credentials if needed

---

## Step-by-Step: External Integration Considerations

| Tool        | Action |
|-------------|--------|
| Slack       | Recreate GitHub App connection in Enterprise Org |
| Codecov     | Re-authorize repo access under `emu-labs-org` |
| Docker Hub  | Update auto-build triggers for new repo |
| Jira        | Re-map branch and PR references under new org |

---

## Post-Migration Checklist

- [x] GitHub Actions workflows pass in destination repo
- [x] Docker builds triggered post-push
- [x] Secrets validated for use in build and deploy jobs
- [x] Webhooks firing correctly


---
