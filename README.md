# AI coding rules sampler: Cursor, Claude Code, Codex (AGENTS.md), Windsurf and Copilot

Free, copy-paste rules and skills that make AI coding agents **plan first, stay secure and prove their work**, in every tool's native format. AGENTS.md is the single source of truth; CLAUDE.md imports it with `@AGENTS.md`.

- 3 always-on rules: core engineering, security, and agent workflow
- 3 skills / slash commands: `/plan-feature`, `/review-changes`, `/record-decisions`
- 5 formats: `.cursor/rules/*.mdc`, `CLAUDE.md` + `.claude/skills`, `AGENTS.md` + `.agents/skills`, `.windsurf/rules` + workflows, `.github/copilot-instructions.md` + prompts
- MIT licensed. Use it in any project, commercial included.

## What the rules tell your agent

**Core engineering**
- Match the existing code style, structure and libraries; read neighbouring files before writing new ones.
- Prefer small, pure, typed functions; handle errors explicitly; no silent catches.
- Never invent APIs, config keys or package names; check the installed version's docs or source.
- No new dependency without asking; prefer the standard library and what's already installed.
- Keep secrets out of code, logs, tests and commits; config comes from environment variables.

**Security**
- Never hard-code, log or commit secrets; read from env; .env in .gitignore; rotate anything that leaked.
- Validate all external input at the boundary with a schema (zod / pydantic); reject unknown fields.
- Authorize every request server-side against the resource owner/role, never trust client-supplied ids or roles.
- Parameterized queries only; no string-built SQL, shell or HTML; encode output.
- No new dependency without checking maintenance, downloads and advisories; run the audit command.

**Agent workflow**
- Read PLAN.md first; for non-trivial work write/update it (goal, files, steps, done-criteria) before coding.
- One feature or bug per session; steps small enough to verify (~<150 changed lines).
- After each step run the project's checks (see "Commands" in README/AGENTS.md) and fix failures before continuing.
- Never claim something works without running it; say exactly what was and wasn't verified.
- Ask before adding dependencies, changing public APIs, touching auth/payments/migrations, or deleting files.
- When context gets long, summarize state into PLAN.md and suggest a fresh session.

Full text: [`codex/AGENTS.md`](codex/AGENTS.md).

## Install (copy one folder's contents into your repo root)

| Tool | Copy | Check it loaded |
|---|---|---|
| **Cursor** | `cursor/.cursor/` | Settings → Rules: `core`, `security`, `agent-workflow` show as Always. Workflows: type `@plan-feature`. |
| **Claude Code** | `claude/CLAUDE.md`, `claude/AGENTS.md`, `claude/.claude/` | Run `/context`. CLAUDE.md's first line `@AGENTS.md` imports the rules. Skills: `/plan-feature`, `/review-changes`, `/record-decisions`. |
| **Codex** (and other AGENTS.md tools) | `codex/AGENTS.md`, `codex/.agents/` | Codex reads AGENTS.md automatically. Skills: `$plan-feature`, `$record-decisions`. |
| **Windsurf / Devin** | `windsurf/.windsurf/` | Rules show as always-on; workflows run as `/plan-feature`. |
| **GitHub Copilot** | `copilot/.github/` | `copilot-instructions.md` applies to every chat; prompts run as `/plan-feature` in VS Code. |

```bash
# example: Claude Code
git clone https://github.com/<you>/ai-coding-rules-sampler /tmp/sampler
cp -r /tmp/sampler/claude/. ./
```

Already have an AGENTS.md or CLAUDE.md? Merge the sections instead of overwriting, and keep **one** AGENTS.md as the source of truth. In CLAUDE.md, add `@AGENTS.md` at the top.

Only want the raw Cursor rules? They're also in [`rules/`](rules/).

## The decisions log
`AGENTS.md` ends with a `## Decisions log`. At the end of a session, run `/record-decisions` (Claude Code), `$record-decisions` (Codex) or the `/record-decisions` workflow (Windsurf). The agent lists what was decided, asks you, and appends dated one-liners, so the next session doesn't re-argue settled choices.

## Want more?
This sampler is a slice of the paid kits at **[kitquarry.com](https://kitquarry.com)**:
- **AI Coding Rules Pack:** testing, git and code review rules; stack rules for TypeScript, React/Next.js, Python/FastAPI and Node; an agent-safe definition of done (never edit tests to pass); version pinning (Tailwind v4, Next.js 16, Supabase); local rule files for auth and billing; more skills.
- **Starter kits:** a tested AI agent starter (TypeScript, MCP), a SaaS starter (Next.js 16, auth, Lemon Squeezy) and a Godot 4 game kit, with rules pre-installed.

Free sampler zip and install docs: <https://kitquarry.com/free.html>

## License
MIT. See [LICENSE](LICENSE).
