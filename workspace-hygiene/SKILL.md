---
name: workspace-hygiene
description: Workspace cleanup and search-signal discipline. Use before stopping non-trivial work, after creating scratch artifacts, logs, generated files, cloned/copied repos, docs trees, caches, or test outputs, and when search results are polluted by temporary or bulky context.
---

# Workspace Hygiene

Goal: keep workspace searchable and useful.

## Artifact Locations

Prefer predictable locations:

- `.agent/notes/` for durable notes
- `.agent/helpers/` for reusable helper scripts
- `.agent/workflows/` for repeatable process
- `plan/` for active coordination
- project temp/cache dirs for disposable outputs

## Before Stopping

- Remove agent-created scratch files no longer useful.
- Remove stale logs/test outputs unless evidence.
- Update or delete stale plans.
- Keep only files that explain state, reproduce result, or are needed by user.

## Delete Rules

- Delete obvious agent-created scratch directly.
- Call `request_user_input` before deleting broad sets, user-owned files, source files, configs, or unclear ownership.
- If unsure whether artifact is evidence or noise, call `request_user_input` with keep, delete, or archive choices.

## Bulky Context

If copied/cloned repo, vendor tree, docs tree, generated bundle, cache, fixture set, or large data dir only exists as working context and pollutes search:

- call `request_user_input` to choose remove, archive, or exclude from search.
- prefer removing/excluding bulk noise when future search improves.

## Search

- Ignore known noisy artifact dirs/files when irrelevant.
- Prefer targeted `rg` patterns over broad dumps.
- Keep handoff files current; stale memory can mislead more than no memory.
