# Repository Guidelines

## Project Structure & Module Organization
- `skills/` holds the unified SuperNavigator skills (OS layer + App layer) as the primary source of truth.
- `navigator-main/` contains the upstream Navigator layer, docs, scripts, and small TypeScript utilities under `navigator-main/src/`.
- `superpowers-main/` contains the upstream Superpowers layer, tests, hooks, and support docs.
- `docs/`, `examples/`, and `templates/` provide repo-level documentation and starter templates.
- `ARCHITECTURE.md` and `CHANGELOG.md` capture system design and release history.

Skill layout follows `skills/<layer>/<group>/<skill-name>/SKILL.md` with supporting `functions/`, `templates/`, and `examples/` folders.

## Build, Test, and Development Commands
There is no compiled build step; most work is Markdown, shell scripts, and Python utilities.
- `superpowers-main/tests/claude-code/run-skill-tests.sh` runs Claude Code skill tests (requires `claude` CLI).
- `superpowers-main/tests/opencode/run-tests.sh` runs OpenCode plugin tests (requires `opencode`).
- `superpowers-main/tests/skill-triggering/run-all.sh` runs quick prompt-trigger checks.
- `navigator-main/tests/test-monitor.sh` (and `test-recovery.sh`, `test-retry-logic.sh`) run Navigator shell checks.

## Coding Style & Naming Conventions
- Use kebab-case for skill names and directories (e.g., `nav-start`, `test-driven-development`).
- `SKILL.md` files include YAML frontmatter (`name`, `description`, `allowed-tools`, `version`) followed by Markdown instructions.
- Indentation: Python uses 4 spaces; TypeScript/JavaScript and JSON use 2 spaces; shell scripts typically use 4-space indentation and `set -euo pipefail`.
- Prefer small, focused functions and keep Markdown headings consistent and shallow.

## Testing Guidelines
- Tests are shell-based; add new ones under `superpowers-main/tests/...` as `test-<skill-name>.sh`.
- Run a single Claude Code test with `superpowers-main/tests/claude-code/run-skill-tests.sh --test test-<skill>.sh`.
- Integration tests are slower and require local CLIs; there is no enforced coverage target.

## Commit & Pull Request Guidelines
- Git history is minimal and inconsistent (`Initial commit`, `new`), so no strict convention exists. Use a short, imperative summary (optional scope), e.g., `Add nav-task template sync`.
- PRs should state which layer is affected (OS vs App), list tests run (or "not run"), and note any template or docs updates. Screenshots are only needed for UI examples.

## Configuration Notes
- `.agent/` content is generated in consumer projects during initialization; avoid adding it to this repository.
