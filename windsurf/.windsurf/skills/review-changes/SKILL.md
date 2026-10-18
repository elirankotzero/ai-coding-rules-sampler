---
name: review-changes
description: Review the current uncommitted diff or branch for bugs, security issues, missing tests and rule violations before committing. Use when asked to review, check or audit changes.
---
Review the current changes (`git diff` and `git diff --staged`; for a branch, use `git diff main...HEAD`).

Report findings grouped by severity: **Blocker / Should fix / Nit**. Give file:line for each. Check:
- **Correctness:** edge cases, error handling, null/undefined, async races, off-by-one.
- **Security:** secrets in code or logs, unvalidated input, missing authz checks, injection (SQL/shell/HTML), unsafe deserialization, overly broad CORS, new dependencies.
- **Tests:** is new behaviour covered? Are tests meaningful (not snapshot-only)? Do they still pass?
- **Project rules:** naming, structure, typing, and the stack rules in this repo.
- **Scope:** unrelated changes, debug leftovers, TODOs without an owner.
End with a one-line verdict: ready to commit / needs changes. Don't edit files unless asked.
