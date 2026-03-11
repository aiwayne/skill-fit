# Skill Fit

`skill-fit` is a decision skill for one practical question:

**Should this skill be installed for this person and this usage context?**

## Install

```bash
npx skills add aiwayne/agent-skills@skill-fit
```

## Decision Classes

- `RECOMMEND_INSTALL`: clear expected upside, recurring value, acceptable setup cost
- `OPTIONAL_INSTALL`: situational value, useful but not mandatory
- `DO_NOT_INSTALL`: low frequency or low complexity where setup overhead is not justified

## Language Behavior

- If user asks in Chinese, `skill-fit` should answer in Chinese by default.
- If user asks in English, `skill-fit` should answer in English.
- For Chinese output, prefer Chinese decision labels:
  - `建议安装` / `可选安装` / `不建议安装`
  - Optional compatibility form: Chinese + enum in parentheses.

## Read-First Requirement (Critical)

Before recommendation, `skill-fit` must first read the target skill docs when a URL/repo is provided.

It must summarize:

- target use cases
- suitable and unsuitable users
- core problems solved
- setup/dependency constraints

Then it can give the install decision.

If source docs are inaccessible (private repo/auth/network), it must return "信息不足，无法完成解读" and ask for `SKILL.md` text or a readable link.

## When to Use

Use `skill-fit` when users ask:

- "该不该装这个 skill"
- "这个 skill 适不适合我"
- "值不值得装"
- "适合什么场景 / 不适合什么人"

## What It Outputs

`skill-fit` always returns:

- skill read summary with source evidence
- one hard decision: `RECOMMEND_INSTALL` / `OPTIONAL_INSTALL` / `DO_NOT_INSTALL`
- usage scene tags
- value tags
- suitable user tags
- unsuitable user tags
- install threshold
- no-install fallback

## Output Example

```markdown
### Decision
RECOMMEND_INSTALL

### Why (Evidence)
- Team runs this workflow 3-5 times per week.
- Current process has multi-role handoff with repeated quality drift.

### Usage Scene Tags
- high_frequency_repetition
- cross_team_standardization
- complex_multistep_workflow

### Value Tags
- efficiency_gain
- consistency_gain
- risk_reduction

### Suitable User Tags
- pm_team_lead
- ops_manager_multi_team

### Unsuitable User Tags
- solo_builder_oneoff

### Install Threshold
- Weekly usage >= 2 and at least 2 collaborators involved.

### No-Install Fallback
- Keep native workflow and use a lightweight checklist template.
```

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
