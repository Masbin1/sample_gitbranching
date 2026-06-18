# Branch Protection Rules

Configure these rules in **GitHub → Settings → Branches → Add branch protection rule**.

---

## `production`

| Setting | Value |
|---------|-------|
| Require a pull request before merging | ✅ Yes |
| Required approvals | 2 |
| Dismiss stale pull request approvals | ✅ Yes |
| Require review from code owners | ✅ Yes |
| Require status checks to pass | ✅ Yes |
| Require branches to be up to date | ✅ Yes |
| Restrict who can push | ✅ Yes — Technical Lead / Release Owner only |
| Allow force pushes | ❌ No |
| Allow deletions | ❌ No |

> `production` only accepts merges from `release/*`. This must be enforced manually via team discipline and PR review — GitHub does not natively restrict merge source branch.

---

## `staging`

| Setting | Value |
|---------|-------|
| Require a pull request before merging | ✅ Yes |
| Required approvals | 1 (Technical Lead) |
| Dismiss stale pull request approvals | ✅ Yes |
| Require status checks to pass | ✅ Yes |
| Restrict who can push | ✅ Yes — Technical Lead only |
| Allow force pushes | ❌ No |
| Allow deletions | ❌ No |

---

## `development-main`

| Setting | Value |
|---------|-------|
| Require a pull request before merging | ✅ Yes |
| Required approvals | 1 (peer or Technical Lead) |
| Dismiss stale pull request approvals | ✅ Yes |
| Allow force pushes | ❌ No |
| Allow deletions | ❌ No |

---

## `release/*`

| Setting | Value |
|---------|-------|
| Require a pull request before merging | ✅ Yes |
| Required approvals | 1 (Technical Lead) |
| Restrict who can push | ✅ Yes — Technical Lead / Release Owner only |
| Allow force pushes | ❌ No |
| Allow deletions | ✅ Yes — after successful production deployment |

---

## `feature/*`, `fix/*`, `hotfix/*`

No protection rules required. Developers manage their own working branches.
Force push is allowed on personal feature branches (needed after rebase).
