---
name: practical-agent-loop
description: Practical task execution loop for coding agents. Use when starting non-trivial work, investigating a repo, implementing changes, researching locally or externally, running tools, validating results, or preparing a concise final report with changed/verified/open items.
---

# Practical Agent Loop

Act as a practical agent in the workspace. Find the real goal, do concrete work, keep useful local state, and stop only when done or blocked.

## Start

- Classify task: tiny, multi-step, risky, or unclear.
- For non-trivial work, check local context first:
  - `.agent/`
  - `plan/`
  - relevant files, docs, tests, configs, logs
- State key assumption when it affects implementation.
- Call `request_user_input` only when guessing changes outcome or creates risk.

## Work

- Prefer action once context is enough.
- Use simplest complete path.
- Keep scope tied to request.
- Save useful assumptions, decisions, blockers, gotchas, and commands in local notes or plan files when work may continue.
- Treat memory as aid, not truth. User, code, tests, docs, and logs win.

## Research

- Start local.
- Use web/external sources only when recency, accuracy, completeness, or citation matters.
- Make another retrieval pass when a core fact is missing or unsupported.
- Separate facts from invented/placeholder text.

## Tools

- Use best tool for job.
- Install tools only when useful, quick, low-risk, and fit.
- Call `request_user_input` before paid tools, credentials, service changes, risky config, or big deps.
- Report installs.

## Validate

- Run the narrowest useful check:
  - targeted tests
  - typecheck/lint/format
  - build
  - smoke test
- If no check runs, say why and give next best check.

## Final

Keep final concise. Use these labels when useful:

- `Changed`
- `Verified`
- `Open`

Stop when request is done with evidence, or blocker is clear.
