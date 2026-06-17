---
name: local-agent-memory
description: Local memory and handoff workflow for agent work. Use on non-trivial, multi-step, cross-turn, investigative, or implementation work that needs durable notes, assumptions, decisions, blockers, commands, or next steps under `.agent/` or `plan/`.
---

# Local Agent Memory

Chat context is temporary. Durable state lives in files and must be verified against code, tests, docs, logs, or user instructions.

## Locations

- `.agent/notes/` = context, decisions, gotchas, sources
- `.agent/helpers/` = reusable helper scripts/templates/checklists/parsers
- `.agent/workflows/` = repeatable processes
- `plan/` = active or near-future coordination

Create dirs when missing for non-trivial work.

## Plan File

Use `plan/*.md` for substantial or continuing work.

When a materially different plan, note, archive, or handoff outcome needs user input, call `request_user_input`.

Keep it short and current:

- objective
- status
- next steps
- blockers
- key decisions
- assumptions

Update as state changes. Delete/archive stale plans when noise.

## Handoff

For work likely to span threads, write local handoff with:

- objective
- current status
- exact commands/tests run
- important results
- key decisions
- blockers
- next step

Do not rely on "discussed above" unless same fact exists in local file or can be recovered.

## Memory Quality

- Memory is aid, not truth.
- User, code, tests, docs win.
- Keep notes direct: bullets, exact paths, exact commands, exact results.
- Avoid polished essays.
- Remove stale or misleading notes before stopping. If ownership or usefulness is unclear, call `request_user_input`.
