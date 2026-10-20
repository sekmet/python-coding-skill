---
name: python-coding
description: Orchestrates Python coding skills for library, application, CLI, testing, packaging, documentation, security, performance, release, and repository hygiene work. Use for Python code writing, review, debugging, refactoring, project setup, tooling, tests, APIs, PyPI packaging, releases, docs, security audits, performance profiling, or open source maintenance. Loads the relevant specialized skill files from skills/ only when needed.
---

# Python Coding Skill Orchestrator

Use this as the entry point for Python work. It indexes the focused skills in
`skills/` and tells you which files to read before acting.

## Operating Rule

For every Python coding task:

1. Identify the user's goal and the affected surface area.
2. Read the smallest set of relevant `skills/*/SKILL.md` files below.
3. If a selected skill points to adjacent reference files or scripts, read or run
   only the ones needed for the current task.
4. Combine skills when the work crosses boundaries, such as adding a CLI with
   tests and packaging metadata.
5. Prefer the target repository's existing conventions over generic examples in
   these skills.

Do not load every subskill by default. The files under `skills/` are the source
of truth for detailed guidance.

## Skill Index

| Need | Read |
| --- | --- |
| Start or modernize a Python project; configure `pyproject.toml`, `uv`, `ruff`, `pytest`, pre-commit, CI, Makefile, or `src/` layout | `skills/project-setup/SKILL.md` |
| Improve code quality; add type hints; configure or fix `ruff`, `mypy`, Pythonic refactors, complexity, imports, formatting | `skills/code-quality/SKILL.md` |
| Write, repair, or expand tests; use pytest fixtures, parametrization, mocking, coverage, Hypothesis, or test CI | `skills/testing-strategy/SKILL.md` |
| Design public Python APIs; choose names, exceptions, deprecations, compatibility policy, or breaking-change strategy | `skills/api-design/SKILL.md` |
| Build or update command-line interfaces with Click, Typer, argparse, entry points, shell completion, progress bars, or CLI tests | `skills/cli-development/SKILL.md` |
| Package or publish libraries; build wheels/sdists; configure build backends, project metadata, optional deps, or PyPI trusted publishing | `skills/packaging/SKILL.md` |
| Plan or automate releases; manage versions, changelogs, tags, GitHub releases, release workflows, or deprecation windows | `skills/release-management/SKILL.md` |
| Write docs; improve README, docstrings, Sphinx, ReadTheDocs, API references, tutorials, or examples | `skills/documentation/SKILL.md` |
| Audit or fix security issues; use Bandit, pip-audit, Semgrep, detect-secrets; handle injection, secrets, crypto, deserialization, path traversal | `skills/security-audit/SKILL.md` |
| Profile or optimize runtime and memory; add benchmarks; use cProfile, PyInstrument, Memray, tracemalloc, pytest-benchmark | `skills/performance/SKILL.md` |
| Review a Python library across structure, packaging, code quality, tests, security, docs, API, and CI/CD | `skills/library-review/SKILL.md` |
| Set up contributor experience; create CONTRIBUTING, CODE_OF_CONDUCT, issue/PR templates, maintainer workflow, community automation | `skills/community/SKILL.md` |
| Keep the git repo clean; handle `.gitignore`, tracked junk, committed secrets, `git rm --cached`, secret rotation, history scrubbing | `skills/git-hygiene/SKILL.md` |

## Common Combinations

- **New package**: `project-setup` + `code-quality` + `testing-strategy` +
  `documentation`; add `packaging` if it will be distributed.
- **Public library feature**: `api-design` + `testing-strategy` +
  `documentation`; add `code-quality` for typing/refactor work.
- **CLI package**: `cli-development` + `packaging` + `testing-strategy`;
  add `documentation` for command usage docs.
- **Release readiness**: `library-review` first, then route findings to
  `testing-strategy`, `security-audit`, `packaging`, `documentation`, and
  `release-management` as needed.
- **Security cleanup**: `security-audit` + `git-hygiene` when secrets or
  unsafe tracked files are involved.
- **Performance work**: `performance` + `testing-strategy`; add
  `code-quality` only when refactors are needed to make the optimization safe.

## Task Workflow

1. Inspect the local project before making assumptions:
   `rg --files`, then read `pyproject.toml`, package modules, tests, and docs
   relevant to the request.
2. Load selected subskills from this index.
3. Make focused edits that match local style and tooling.
4. Run the narrowest meaningful verification available, such as `pytest`,
   `ruff check`, `ruff format --check`, `mypy`, `python -m build`,
   `pip-audit`, or the project's documented commands.
5. Report what changed and which verification passed or could not be run.

## Python Defaults

Use these defaults only when the target project does not already establish a
different standard:

- Prefer `src/` layout for libraries.
- Prefer `pyproject.toml` for project metadata and tool configuration.
- Prefer `ruff` for linting/formatting, `pytest` for tests, and `mypy` or
  project-selected static typing for type checking.
- Prefer type hints for public APIs and changed code.
- Prefer small, composable functions with explicit errors over broad catches or
  implicit `None` handling.
- Preserve backwards compatibility for public library APIs unless the user asks
  for a breaking change.
