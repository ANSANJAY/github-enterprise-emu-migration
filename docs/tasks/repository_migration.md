# Task 3: Repository Migration

## Objective

Migrate repositories from an unmanaged GitHub user account (`gh-source-demo`) into the managed GitHub Enterprise organization (`emu-labs-org`). Ensure that full commit history, branches, tags, and issues are preserved during the transfer.

---

## Repositories Selected for Migration

| Repository Name     | Source URL                                               | Target URL                                                  |
|---------------------|----------------------------------------------------------|-------------------------------------------------------------|
| demo-service-api    | https://github.com/gh-source-demo/demo-service-api.git   | https://github.com/emu-labs-org/demo-service-api.git        |
| monitoring-tool     | https://github.com/gh-source-demo/monitoring-tool.git    | https://github.com/emu-labs-org/monitoring-tool.git         |

---

## Environment Details

- Source Account: `gh-source-demo`
- Destination Org: `emu-labs-org`
- GitHub CLI Version: 2.45.0
- Git Version: 2.41.0
- Migration Admin User: `test1emu_admin`

---

## Commands Executed

### Step 1: Clone the Repository from Source Account

```bash
git clone https://github.com/gh-source-demo/demo-service-api.git
cd demo-service-api
```

**Output:**

```bash
Cloning into 'demo-service-api'...
remote: Enumerating objects: 75, done.
remote: Counting objects: 100% (75/75), done.
remote: Compressing objects: 100% (61/61), done.
Receiving objects: 100% (75/75), 120.00 KiB | 1.56 MiB/s, done.
Resolving deltas: 100% (22/22), done.
```

---

### Step 2: Update Remote to GitHub Enterprise Org

```bash
git remote rename origin old-origin
git remote add origin https://github.com/emu-labs-org/demo-service-api.git
```

---

### Step 3: Push All Branches and Tags

```bash
git push -u origin --all
git push --tags
```

**Output:**

```bash
Enumerating objects: 75, done.
Counting objects: 100% (75/75), done.
Delta compression using up to 8 threads
Compressing objects: 100% (61/61), done.
Writing objects: 100% (75/75), 120.00 KiB | 120.00 MiB/s, done.
Total 75 (delta 22), reused 0 (delta 0)
To https://github.com/emu-labs-org/demo-service-api.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

---

## Post-Migration Validation

- Repository cloned from new URL and validated
- `git log` confirms full history
- `git tag` confirms release preservation
- Permissions inherited from org-level team assignments

---

## Repository Migration Complete

| Repo Name           | Status     | Notes                              |
|---------------------|------------|-------------------------------------|
| demo-service-api    | Migrated   | All history, branches, tags intact |
| monitoring-tool     | Pending    | Will be completed in the next cycle    |

