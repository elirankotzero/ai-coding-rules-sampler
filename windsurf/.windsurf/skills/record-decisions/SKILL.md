---
name: record-decisions
description: End-of-session step that appends the decisions made in this session (what, why, alternatives rejected) to the Decisions log in AGENTS.md. Use when the user wraps up a session or asks to record decisions.
argument-hint: "[optional topic or note]"
triggers:
  - user
---
Record this session's durable decisions in the **Decisions log** at the end of the root `AGENTS.md`. AGENTS.md is the single source of truth every tool reads, so future sessions (any agent) inherit them.

Extra note from the user: the user's request

1. **Collect** the decisions made this session that a future session must respect: architecture or library choices, conventions, things deliberately *not* done, and gotchas discovered. Skip routine edits and anything already obvious from the code.
2. **Show the user** the proposed entries and wait for a yes before writing.
3. **Append only.** Add new entries under `## Decisions log`, newest last, in this format:
   `- YYYY-MM-DD: <decision>. Why: <reason>. Rejected: <alternatives, if any>.`
   Never rewrite or delete existing entries. If a new decision supersedes an old one, add a new entry that says `Supersedes <date> entry about <topic>`.
4. **Keep it lean.** One line per decision. If the log passes ~40 entries, propose moving older ones to `docs/decisions.md` and leaving a pointer, but only with the user's approval.
5. **Update PLAN.md** with "Next session starts with: …" if there is unfinished work.
6. Don't commit. Mention that `/commit-work` can do it.
