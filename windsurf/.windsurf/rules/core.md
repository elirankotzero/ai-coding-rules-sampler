---
trigger: always_on
description: Always-on engineering rules for any language or stack in this repository
---
# Core engineering rules
- **Fit in.** Read neighbouring files first and copy their patterns: naming, folder layout, error handling, test style. Use the libraries already in the project.
- **Verify, don't invent.** Check package names, function signatures and config keys against the installed version (`package.json`, lockfile, `pyproject.toml`, and `node_modules`/site-packages source). If unsure, say so.
- **Simple first.** Write the most direct solution that meets the requirement. No speculative abstraction, no unused options. Delete dead code; don't comment it out.
- **Explicit errors.** Never swallow exceptions (`catch {}` / `except: pass`). Either handle the error meaningfully or let it propagate with context. Return typed results at boundaries.
- **Types are documentation.** Use strict typing (`strict` TS, type hints with a checker). Avoid `any` and `# type: ignore` unless you add a comment saying why.
- **Small units.** Functions do one thing. Files stay focused. Side effects (I/O, network, time, randomness) live at the edges so logic is testable.
- **Names over comments.** Comments explain *why*, not *what*. Keep docs and README in sync when behaviour changes.
- **Dependencies:** ask before adding one. Prefer well-maintained, widely used packages. Pin via the lockfile and never edit lockfiles by hand.
- **Config:** read config from environment variables validated at startup. Commit `.env.example`, never `.env`.
