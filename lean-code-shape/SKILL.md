---
name: lean-code-shape
description: Lean coding rules for research/unreleased work. Use when writing, reviewing, refactoring, or debugging code where the user wants minimal scope, no speculative abstractions, no defensive compatibility layers, surgical edits, and simple verified implementation.
---

# Lean Code Shape

Default assumption: workspace is research/unreleased unless user says production.

## Rules

- Build only what task needs.
- Trust validated boundaries. Do not re-check hot-loop data.
- Do not add defensive code for impossible states.
- Avoid broad `try/catch`. Crash loud.
- Do not add fallback, compatibility layer, migration guard, or feature flag unless asked.
- Do not add wrapper/pass-through function unless it removes real duplication.
- Do not duplicate types/interfaces.
- Use derived state when it makes code simpler or more correct.
- Prefer one clear pass over many micro-passes.
- Before edit, ask: is this reachable and needed? If no, omit.
- After edit, simplify own code once.

## Edit Discipline

- Keep diff tied to request.
- Match local style.
- Do not reformat or refactor adjacent code.
- Clean only unused imports/vars/helpers caused by your change.
- Mention unrelated problems separately.

## Verification

- Pick narrow useful check before final.
- Prefer targeted test/typecheck/lint/build/smoke based on change risk.
- If no check runs, state why.
