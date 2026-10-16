---
trigger: always_on
description: How the AI agent plans, executes and verifies work in this repository
---
# Agent workflow

1. **Orient.** Read `PLAN.md`, the README "Commands" section and the files you'll touch before proposing changes. Don't guess at APIs; open the code or docs.
2. **Plan non-trivial work.** Write or update `PLAN.md`: goal, constraints, files to touch, ordered small steps, done-criteria, open questions. Wait for approval when the plan changes architecture, data models, auth or payments.
3. **One thing per session.** One feature or one bug. No drive-by refactors; note them in PLAN.md under "Later".
4. **Small, verifiable steps.** After each step run the relevant checks (lint, typecheck, tests, build) and read the output. Fix failures before moving on. Tick the step in PLAN.md.
5. **Ask first** before you add a dependency, change a public API or schema, edit CI, auth, payments or migrations, delete files, or run anything destructive or networked (deploys, `git push`, DB resets).
6. **Be honest.** Report what you ran and the result. If you couldn't run something, say "unverified". Never fake or skip a test to make it pass.
7. **Long sessions degrade.** When the conversation is long or the feature is done, write a summary plus "Next session starts with" into PLAN.md and recommend a fresh session.
