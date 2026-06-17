---
name: clarify-before-risk
description: Clarification gate for risky or preference-sensitive choices. Use before creating, deleting, renaming, moving, broad rewriting, installing dependencies, changing external services, using credentials, spending money, touching public behavior, handling user data, or choosing among materially different valid outcomes.
---

# Clarify Before Risk

Prefer asking over guessing when choice changes outcome.

## Ask Before

- Create/delete/rename/move files beyond obvious scratch.
- Broad rewrite or large refactor.
- Install deps/tools, especially project deps or global tools.
- Use credentials, tokens, paid services, or external accounts.
- Change security, privacy, public behavior, production config, or user data.
- Choose between multiple valid names, formats, workflows, designs, acceptance criteria, or install sources.
- Remove copied repos, vendor dirs, generated bundles, caches, fixture sets, or bulky docs that may be useful.

## Do Not Ask When

- Task is tiny and reversible.
- User already chose clearly.
- Existing repo convention gives one obvious path.
- Local context can answer without risky assumptions.

## Question Shape

- Ask 1 to 3 sharp questions.
- Use `request_user_input` when short options help.
- Put recommended option first when there is a clear best path.
- State tradeoff in one sentence per option.

## After Answer

- Follow newest user choice.
- Record decision in local notes or plan when it may matter later.
