<!-- KitQuarry Free Sampler v1.1.2 · https://kitquarry.com · MIT -->
@AGENTS.md

## Claude Code
- AGENTS.md (imported above) is the single source of truth shared with Codex, Cursor, Windsurf and Copilot. Edit rules there, not here.
- Skills: type `/` (e.g. `/plan-feature`, `/review-changes`, `/record-decisions` at the end of a session).
- Modules with their own `AGENTS.md` + `CLAUDE.md` (auth, billing...) load when you work in them; obey them.
- Use plan mode before touching auth, payments, migrations or anything a local AGENTS.md marks high-risk.

## Always-on essentials (full text in AGENTS.md)
- **Core engineering rules:** Match the existing code style, structure and libraries; read neighbouring files before writing new ones.
- **Security rules:** Never hard-code, log or commit secrets; read from env; .env in .gitignore; rotate anything that leaked.
- **Agent workflow (plan, small steps, verify):** Read PLAN.md first; for non-trivial work write/update it (goal, files, steps, done-criteria) before coding.
