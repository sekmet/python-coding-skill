# Python Coding Skill

This repository contains a Codex skill for Python coding work.

The root [`SKILL.md`](SKILL.md) is the entry point. It acts as an orchestrator:
when a Python task comes in, Codex uses the root skill to choose the smallest
relevant specialized skill files under [`skills/`](skills/) instead of loading
every guide at once.

The skill is useful for Python code writing, review, debugging, refactoring,
project setup, tests, API design, CLIs, packaging, releases, documentation,
security audits, performance work, and repository hygiene.

## Layout

```text
python-coding/
├── SKILL.md                    # Root orchestrator skill
└── skills/
    ├── api-design/
    ├── cli-development/
    ├── code-quality/
    ├── community/
    ├── documentation/
    ├── git-hygiene/
    ├── library-review/
    ├── packaging/
    ├── performance/
    ├── project-setup/
    ├── release-management/
    ├── security-audit/
    └── testing-strategy/
```

## Installation

Install this repository as one skill directory so Codex can discover the root
`SKILL.md` and route to the nested skills.

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -r <YOUR-PATH>/python-coding \
  "${CODEX_HOME:-$HOME/.codex}/skills/python-coding"
```

For project-local use, copy it into a project's skill directory instead:

```bash
mkdir -p .codex/skills
cp -r <YOUR-PATH>/python-coding .codex/skills/python-coding
```

## How It Works

Ask Codex to do Python work normally. The root skill triggers broadly for Python
coding and then loads one or more focused subskills only when needed.

Examples:

- "Set up a new Python package with pytest and ruff" routes to
  `skills/project-setup/SKILL.md`, then may load `skills/testing-strategy/SKILL.md`
  and `skills/code-quality/SKILL.md`.
- "Add a Click CLI and package entry point" routes to
  `skills/cli-development/SKILL.md` and `skills/packaging/SKILL.md`.
- "Audit this repo for committed secrets" routes to
  `skills/git-hygiene/SKILL.md` and may load `skills/security-audit/SKILL.md`.
- "Prepare this library for release" routes through
  `skills/library-review/SKILL.md`, then into release, packaging, docs, testing,
  or security skills as needed.

## Available Subskills

| Area | File | Use For |
| --- | --- | --- |
| Project setup | `skills/project-setup/SKILL.md` | `pyproject.toml`, `src/` layout, `uv`, ruff, pytest, pre-commit, CI, Makefile |
| Code quality | `skills/code-quality/SKILL.md` | Ruff, mypy, type hints, imports, formatting, refactoring, Pythonic idioms |
| Testing | `skills/testing-strategy/SKILL.md` | Pytest, fixtures, parametrization, mocking, coverage, Hypothesis |
| API design | `skills/api-design/SKILL.md` | Public APIs, naming, errors, deprecations, compatibility, breaking changes |
| CLI development | `skills/cli-development/SKILL.md` | Click, Typer, argparse, command groups, entry points, CLI testing |
| Packaging | `skills/packaging/SKILL.md` | Build backends, wheels, sdists, project metadata, PyPI publishing |
| Releases | `skills/release-management/SKILL.md` | Versioning, changelogs, release workflows, tags, deprecations |
| Documentation | `skills/documentation/SKILL.md` | README, docstrings, Sphinx, ReadTheDocs, tutorials, API references |
| Security | `skills/security-audit/SKILL.md` | Bandit, pip-audit, Semgrep, detect-secrets, injection, secrets, crypto |
| Performance | `skills/performance/SKILL.md` | Profiling, memory analysis, benchmarking, performance regression tests |
| Library review | `skills/library-review/SKILL.md` | End-to-end review across structure, packaging, code, tests, security, docs, API, CI |
| Community | `skills/community/SKILL.md` | CONTRIBUTING, CODE_OF_CONDUCT, issue/PR templates, contributor workflow |
| Git hygiene | `skills/git-hygiene/SKILL.md` | `.gitignore`, tracked junk, committed secrets, `git rm --cached`, history cleanup |

## Common Skill Combinations

- New package: project setup, code quality, testing, documentation, and packaging.
- Public library feature: API design, testing, documentation, and code quality.
- CLI package: CLI development, packaging, testing, and documentation.
- Release readiness: library review, then release management, packaging,
  testing, docs, security, or code quality as findings require.
- Security cleanup: security audit plus git hygiene.
- Performance work: performance plus testing, with code quality when refactoring
  is needed.

## Validation

Validate the skill folder after changes:

```bash
python <HOME-PATH>/.codex/skills/.system/skill-creator/scripts/quick_validate.py \
  <YOUR-PATH>/python-coding
```

Expected result:

```text
Skill is valid!
```

## License

MIT License. See [`LICENSE`](LICENSE) for details.
