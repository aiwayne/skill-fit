# Agent Skills

Open-source agent skills by Wayne.

This repository hosts production-ready skills with clear trigger rules, deterministic output formats, and practical evaluation sets.

## Available Skills

| Skill | Purpose | Install |
| --- | --- | --- |
| `skill-fit` | Decide whether a candidate skill should be installed for a specific role and usage context | `npx skills add aiwayne/agent-skills@skill-fit` |

## Why This Repo

- Ship skills as reusable building blocks, not one-off prompts
- Keep decision quality stable with explicit output templates
- Make skills auditable with reference docs and eval fixtures

## Skill Design Standard

Each skill in this repository should include:

- `SKILL.md` with strict frontmatter (`name`, `description`)
- `references/` for boundaries, policies, or domain docs
- `evals/` for minimal trigger/non-trigger regression checks

## Contributing

Issues and pull requests are welcome.
