# Agent Skills

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/aiwayne/agent-skills)](https://github.com/aiwayne/agent-skills/releases)

Open-source, production-ready agent skills by Wayne.

This repository follows a practical standard: each skill must be triggerable, testable, and explainable.

## Available Skills

| Skill | Positioning | Install |
| --- | --- | --- |
| [`skill-fit`](skill-fit/README.md) | Installation decision engine. Answers "should I install this skill?" with hard classification and evidence | `npx skills add aiwayne/agent-skills@skill-fit` |

## Design Principles

- **Strong decision first**: avoid ambiguous recommendations
- **Explicit output contract**: stable structure, easy downstream parsing
- **Boundary-aware workflow**: discovery, decision, and creation are separated
- **Minimal eval fixtures**: regression checks for trigger and non-trigger cases

## Repository Contract

Each skill should include:

- `SKILL.md` with strict frontmatter (`name`, `description`)
- `README.md` with install, scope, examples, and limitations
- `references/` for handoff rules or domain constraints
- `evals/` for trigger/non-trigger and consistency checks

## Quick Start

```bash
# install skill-fit
npx skills add aiwayne/agent-skills@skill-fit
```

## Contributing

Issues and pull requests are welcome. Please include:

- clear trigger context
- expected output format
- at least one eval fixture
