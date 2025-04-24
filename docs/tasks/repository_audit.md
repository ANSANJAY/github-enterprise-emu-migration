
# Task 1: Repository Audit

## Objective

Identify all existing repositories and their associated contributors, branches, and dependencies in the unmanaged GitHub account (`gh-source-demo`). This establishes the scope of migration and prepares metadata required for the transition to GitHub Enterprise.

---

## Environment Details

- Source Account: `gh-source-demo`
- GitHub CLI Version: 2.45.0
- Authenticated via: GitHub Personal Access Token
- Output Format: JSON → CSV

---

## Commands Executed

### Step 1: List All Repositories

```bash
gh repo list gh-source-demo --limit 100 --json name,visibility,defaultBranch,updatedAt,sizeInBytes > audit_repo_list.json
```

** Output (audit_repo_list.json):**

```json
[
  {
    "name": "demo-service-api",
    "visibility": "PUBLIC",
    "defaultBranch": "main",
    "updatedAt": "2025-04-20T16:45:00Z",
    "sizeInBytes": 3145728
  },
  {
    "name": "monitoring-tool",
    "visibility": "PRIVATE",
    "defaultBranch": "main",
    "updatedAt": "2025-04-21T09:12:00Z",
    "sizeInBytes": 4194304
  }
]
```

---

### Step 2: Export Contributor Details (per repo)

```bash
gh api repos/gh-source-demo/demo-service-api/contributors \
  --paginate --jq '.[] | {login, contributions}' > audit_demo_service_api_contributors.json
```

**Sample Output:**

```json
[
  {
    "login": "johnsmith",
    "contributions": 48
  },
  {
    "login": "anamikasanjay",
    "contributions": 12
  }
]
```

---

### Step 3: Compile Audit into Spreadsheet

Data from the above commands was compiled into:
- `docs/identity_mapping.csv`
- `docs/repo_inventory.csv`

Sample Row in `repo_inventory.csv`:

| Repository Name | Visibility | Size (MB) | Default Branch | Last Updated | Contributors          |
|------------------|------------|-----------|----------------|--------------|------------------------|
| demo-service-api | Public     | 3.0       | main           | 2025-04-20   | johnsmith, anamikasanjay |
| monitoring-tool  | Private    | 4.0       | main           | 2025-04-21   | anamikasanjay          |

---

## Notes

- All command outputs are saved and versioned under `docs/audit/`
- No inactive or archived repositories were selected for migration
- Contributor mapping was later used for team access setup in the destination org

