# Odoo.sh Git Repository Template

This repository is a template for Odoo.sh multi-developer projects following the **four-tier branching strategy**.

---

## Branch Structure

| Branch | Odoo.sh Stage | Purpose |
|--------|--------------|---------|
| `production` | Production | Live code. Only receives merges from `release/*`. |
| `release/<version>` | — | Selective release candidate. Created fresh from `production` after UAT. |
| `staging` | Staging | UAT environment. Receives selective merges from `feature/*` branches. |
| `development-main` | Development | Technical integration. All feature branches merge here for conflict validation. |
| `feature/<ticket>-<desc>` | Development | Individual feature or fix. Always branched from `production`. |

---

## Flow

```
feature/*  ──→  development-main   (technical validation, all features)
feature/*  ──→  staging            (selective, only ready features)
staging    ──→  release/<version>  (selective, only UAT-passed features)
release/*  ──→  production         (after release approval)
```

---

## Getting Started

### 1. Use this template

Click **"Use this template"** on GitHub to create your own repository.

### 2. Setup branches

```bash
# Clone your new repo
git clone https://github.com/<your-org>/<your-repo>.git
cd <your-repo>

# Create and push all required branches
git checkout -b production
git push origin production

git checkout -b staging
git push origin staging

git checkout -b development-main
git push origin development-main
```

### 3. Set default branch

Go to **Settings → Branches** and set `production` as the default branch.

### 4. Configure branch protection

Go to **Settings → Branches → Add branch protection rule** and apply rules from [`docs/branch-protection.md`](docs/branch-protection.md).

---

## Creating a Feature Branch

```bash
# Always branch from production
git checkout production
git pull origin production
git checkout -b feature/<ticket-id>-<short-description>

# Work, commit, push
git add .
git commit -m "[ADD] module_name: short description"
git push origin feature/<ticket-id>-<short-description>
```

## Before PR to Staging — Rebase

```bash
git checkout feature/<ticket-id>-<short-description>
git rebase production
git push origin feature/<ticket-id>-<short-description> --force-with-lease
```

## Creating a Release Branch

```bash
# Always from production, never from staging or development-main
git checkout production
git pull origin production
git checkout -b release/v1.0.0

# Merge only UAT-passed features
git merge feature/AAA
git merge feature/CCC
# skip feature/BBB — not yet UAT-passed

git push origin release/v1.0.0
```

---

## Commit Message Format

```
[TAG] module_name: short description (under 50 characters)

Body: explain WHY, not WHAT. Reference ticket number.
```

| Tag | Use |
|-----|-----|
| `[ADD]` | New feature or module |
| `[IMP]` | Improvement to existing functionality |
| `[FIX]` | Bug fix |
| `[REF]` | Refactoring, no functional change |
| `[REM]` | Removal of feature or dead code |
| `[MOV]` | Moving files, no functional change |

---

## Branch Naming Convention

| Type | Format | Example |
|------|--------|---------|
| Feature | `feature/<ticket>-<desc>` | `feature/123-add-capture-sales` |
| Bug fix | `fix/<ticket>-<desc>` | `fix/456-correct-tax-rounding` |
| Hotfix | `hotfix/<desc>` | `hotfix/payment-posting-failure` |
| Release | `release/<version>` | `release/v1.4.0` |

---

## References

- [Branch Protection Rules](docs/branch-protection.md)
- [Git Workflow Guide](docs/git-workflow.md)
- [Pull Request Checklist](.github/PULL_REQUEST_TEMPLATE/pull_request_template.md)
