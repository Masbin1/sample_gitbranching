# Git Workflow Guide

## Day-to-Day Developer Workflow

### 1. Start a new feature

```bash
# Always start from production
git checkout production
git pull origin production
git checkout -b feature/123-add-capture-sales
```

### 2. Develop and commit

```bash
git add .
git commit -m "[ADD] al3_boerdery: add capture sales wizard"

# Push early and often
git push origin feature/123-add-capture-sales
```

### 3. Open PR to development-main (technical validation)

- Open a Pull Request targeting `development-main`
- At least 1 peer or Technical Lead must review and approve
- Odoo.sh will build the branch automatically with demo data

### 4. Rebase before PR to staging

```bash
git checkout feature/123-add-capture-sales
git fetch origin
git rebase origin/production
# Resolve conflicts if any
git push origin feature/123-add-capture-sales --force-with-lease
```

### 5. Technical Lead: open PR to staging (selective)

Only features that are technically validated and ready for UAT are merged into staging.
Features with known bugs or incomplete work are skipped and deferred to the next cycle.

---

## Release Cycle (Technical Lead)

### After UAT — create release branch

```bash
# Always from production
git checkout production
git pull origin production
git checkout -b release/v1.2.0

# Merge only UAT-passed features
git merge feature/123-add-capture-sales   # ✅ UAT passed
git merge feature/124-analytic-hierarchy  # ✅ UAT passed
# feature/125-broken-widget               # ❌ skip, deferred

git push origin release/v1.2.0
```

### After release approval — merge to production

```bash
git checkout production
git merge release/v1.2.0
git push origin production

# Tag the release
git tag -a v1.2.0 -m "Release v1.2.0"
git push origin v1.2.0
```

### Clean up

```bash
# Delete release branch after successful deployment
git push origin --delete release/v1.2.0

# Delete merged feature branches
git push origin --delete feature/123-add-capture-sales
git push origin --delete feature/124-analytic-hierarchy
```

---

## Hotfix Workflow

For urgent production fixes only.

```bash
# Branch from production
git checkout production
git pull origin production
git checkout -b hotfix/payment-posting-failure

# Fix, commit
git commit -m "[FIX] account: resolve payment posting failure"

# PR directly to production (bypasses normal flow — requires release owner approval)
# After merge, also merge back to staging and development-main
git checkout staging
git merge hotfix/payment-posting-failure

git checkout development-main
git merge hotfix/payment-posting-failure

# Cleanup
git push origin --delete hotfix/payment-posting-failure
```

---

## Common Commands Reference

```bash
# Check branch status
git log --oneline --graph --all

# See what's different between your branch and production
git diff production...feature/123-add-capture-sales

# Undo last commit (keep changes)
git reset --soft HEAD~1

# Stash work in progress
git stash
git stash pop

# Check which branches are merged into production
git branch --merged production
```

---

## Anti-Patterns to Avoid

| ❌ Don't | ✅ Do instead |
|---------|--------------|
| Commit directly to `staging` or `production` | Always use PRs |
| Bundle multiple features in one branch | One branch per feature/ticket |
| Merge `staging` directly to `production` | Always go through `release/*` |
| Use `development-main` for daily work | Use `feature/*` branches |
| Forget to delete merged branches | Clean up after every deployment |
| Push without rebasing first | Always rebase onto `production` before PR to staging |
