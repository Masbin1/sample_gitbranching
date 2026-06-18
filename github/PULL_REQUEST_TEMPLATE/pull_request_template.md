## Summary

<!-- What does this PR do? Link to ticket/issue. -->

Ticket: #
Type: <!-- feature / fix / hotfix / refactor -->

---

## Target Branch Checklist

**If targeting `development-main`:**
- [ ] Branch created from `production`
- [ ] Commit messages follow `[TAG] module: description` format
- [ ] No unrelated changes bundled in this branch
- [ ] Module installs cleanly on empty database

**If targeting `staging`:**
- [ ] Feature already merged and validated in `development-main`
- [ ] Branch rebased onto `production` (`git rebase production`)
- [ ] No known bugs or incomplete functionality

**If targeting `production` (via `release/*` only):**
- [ ] UAT sign-off received from project authority
- [ ] Release approval obtained
- [ ] Branch is `release/<version>` created fresh from `production`
- [ ] Only UAT-passed features included

---

## Code Review Checklist (for reviewer)

- [ ] Code follows Odoo coding guidelines
- [ ] Module installs cleanly on empty database
- [ ] Unit tests pass
- [ ] No unnecessary dependencies introduced
- [ ] ACLs, record rules, and `sudo()` usage properly handled
- [ ] No debug code or commented-out blocks left in

---

## Testing Notes

<!-- Describe how to test this change. Include test data or setup steps if needed. -->

---

## Screenshots (if applicable)

<!-- Add before/after screenshots for UI changes -->
