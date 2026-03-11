# Skill Fit

`skill-fit` is a decision skill for one practical question:

**Should this skill be installed for this person and this usage context?**

## Install

```bash
npx skills add aiwayne/agent-skills@skill-fit
```

## When to Use

Use `skill-fit` when users ask:

- "该不该装这个 skill"
- "这个 skill 适不适合我"
- "值不值得装"
- "适合什么场景 / 不适合什么人"

## What It Outputs

`skill-fit` always returns:

- one hard decision: `RECOMMEND_INSTALL` / `OPTIONAL_INSTALL` / `DO_NOT_INSTALL`
- usage scene tags
- value tags
- suitable user tags
- unsuitable user tags
- install threshold
- no-install fallback

## Decision Model

The decision is based on five factors:

1. frequency of repeated usage
2. workflow complexity
3. collaboration and standardization pressure
4. setup and learning overhead
5. substitution quality from native capabilities

## Scope Boundary

- `find-skills` discovers candidate skills
- `skill-fit` judges install suitability
- `skill-creator` creates or improves skills

See `references/scope-and-handoff.md` for full handoff rules.

## Quality Guardrails

- no ambiguous output class
- no "it depends" without a final recommendation
- at least two measurable evidence points in every recommendation

## Evaluation

Minimal trigger/non-trigger fixtures are in `evals/evals.json`.
