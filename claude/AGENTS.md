<!-- KitQuarry Free Sampler v1.1.0. This file is yours: edit it freely. It is the single source of truth for Codex, Cursor, Windsurf/Devin, Copilot and (via @AGENTS.md in CLAUDE.md) Claude Code. Keep the Decisions log at the end. -->
# AGENTS.md: Free Sampler

Free sampler: core engineering, security and agent-workflow rules, plus the /plan-feature, /review-changes and /record-decisions skills. AGENTS.md is the single source of truth; CLAUDE.md imports it.

## Core engineering rules
- **Fit in.** Read neighbouring files first and copy their patterns: naming, folder layout, error handling, test style. Use the libraries already in the project.
- **Verify, don't invent.** Check package names, function signatures and config keys against the installed version (`package.json`, lockfile, `pyproject.toml`, and `node_modules`/site-packages source). If unsure, say so.
- **Simple first.** Write the most direct solution that meets the requirement. No speculative abstraction, no unused options. Delete dead code; don't comment it out.
- **Explicit errors.** Never swallow exceptions (`catch {}` / `except: pass`). Either handle the error meaningfully or let it propagate with context. Return typed results at boundaries.
- **Types are documentation.** Use strict typing (`strict` TS, type hints with a checker). Avoid `any` and `# type: ignore` unless you add a comment saying why.
- **Small units.** Functions do one thing. Files stay focused. Side effects (I/O, network, time, randomness) live at the edges so logic is testable.
- **Names over comments.** Comments explain *why*, not *what*. Keep docs and README in sync when behaviour changes.
- **Dependencies:** ask before adding one. Prefer well-maintained, widely used packages. Pin via the lockfile and never edit lockfiles by hand.
- **Config:** read config from environment variables validated at startup. Commit `.env.example`, never `.env`.

## Security rules

### Secrets
- Never put API keys, tokens, passwords, private keys or connection strings in source, tests, fixtures, logs, error messages or commit messages.
- Read secrets from environment variables (or a secret manager). Validate their presence at startup and fail fast.
- `.env*` files stay out of git, except `.env.example` with dummy values. If a secret was ever committed, treat it as leaked: rotate it. Removing it from history is not enough.
- Never expose server secrets to the browser. In Next.js, only `NEXT_PUBLIC_*` variables reach the client, so never prefix a secret with it.

### Input validation
- Treat everything from outside the process as untrusted: request bodies, query strings, headers, cookies, webhooks, files, environment and LLM output.
- Validate at the boundary with a schema (`zod` in TS, `pydantic` in Python). Check types, lengths, ranges and enums. Reject or strip unknown keys.
- File uploads: check size and MIME type (by content when possible), generate server-side names, and never use a user-supplied path (path traversal).

### Authentication & authorization
- Use the framework's or a proven library's auth. Don't write your own crypto, password hashing or session tokens. If you must hash, use argon2id or bcrypt.
- **Authorize every server action and API route.** Check that the current user may act on *this* resource (owner or role) on the server. Hiding a button is not authorization.
- Never trust client-sent `userId`, `role`, `price` or `isAdmin`. Derive them from the session or the database.
- Cookies: `HttpOnly`, `Secure`, `SameSite=Lax` (or `Strict`). Protect state-changing requests against CSRF.
- Verify webhook signatures (HMAC) with a constant-time comparison, and be idempotent.

### Injection & output
- SQL: parameterized queries or an ORM's query builder. Never interpolate strings.
- Shell: avoid it. If you can't, pass an args array (`execFile`, `subprocess.run([...])`) and never use `shell=True` with input.
- HTML: rely on framework escaping. Treat `dangerouslySetInnerHTML` and `v-html` as forbidden unless sanitized (DOMPurify).
- SSRF: never fetch user-supplied URLs server-side without an allowlist.
- Don't leak stack traces or internal errors to clients. Log them server-side without secrets or PII.

### Dependencies
- Before adding a package, check that it's maintained, widely used and has no open critical advisories. Check for typosquatting: confirm the exact name and publisher.
- Run `npm audit --omit=dev` / `pip-audit` after dependency changes. Keep the lockfile committed.
- Never run install scripts or binaries from untrusted sources. Don't `curl | sh`.

### AI-specific
- Treat LLM output and tool results as untrusted input: validate before executing, storing or rendering.
- Never put secrets in prompts. Don't let model output choose file paths, SQL or shell commands without validation.

## Agent workflow

1. **Orient.** Read `PLAN.md`, the README "Commands" section and the files you'll touch before proposing changes. Don't guess at APIs; open the code or docs.
2. **Plan non-trivial work.** Write or update `PLAN.md`: goal, constraints, files to touch, ordered small steps, done-criteria, open questions. Wait for approval when the plan changes architecture, data models, auth or payments.
3. **One thing per session.** One feature or one bug. No drive-by refactors; note them in PLAN.md under "Later".
4. **Small, verifiable steps.** After each step run the relevant checks (lint, typecheck, tests, build) and read the output. Fix failures before moving on. Tick the step in PLAN.md.
5. **Ask first** before you add a dependency, change a public API or schema, edit CI, auth, payments or migrations, delete files, or run anything destructive or networked (deploys, `git push`, DB resets).
6. **Be honest.** Report what you ran and the result. If you couldn't run something, say "unverified". Never fake or skip a test to make it pass.
7. **Long sessions degrade.** When the conversation is long or the feature is done, write a summary plus "Next session starts with" into PLAN.md and recommend a fresh session.

## Reusable workflows

- **plan-feature**: Plan a single feature before writing code. Writes or updates PLAN.md with goal, files, small steps and done-criteria. Use when starting a new feature or when the user asks for a plan.
- **record-decisions**: End-of-session step that appends the decisions made in this session (what, why, alternatives rejected) to the Decisions log in AGENTS.md. Use when the user wraps up a session or asks to record decisions.
- **review-changes**: Review the current uncommitted diff or branch for bugs, security issues, missing tests and rule violations before committing. Use when asked to review, check or audit changes.

## Decisions log

Durable project decisions, appended at the end of a session with `/record-decisions` (append-only, newest last).
Format: `- YYYY-MM-DD: <decision>. Why: <reason>. Rejected: <alternatives>.`

- 2026-10-16: Adopted KitQuarry Free Sampler v1.1.0; AGENTS.md is the single source of truth for all AI tools (CLAUDE.md imports it). Why: one file to maintain. Rejected: per-tool copies.
