---
name: skill-fit
description: 安装决策技能。用于判断“这个 skill 该不该装、适不适合我、值不值得装”，并必须给出明确结论（RECOMMEND_INSTALL / OPTIONAL_INSTALL / DO_NOT_INSTALL）、使用场景标签、价值标签、适用与不适合人群标签。Also use for English requests asking whether a skill should be installed for a specific role and usage context.
---

# Skill Fit

Make a strong install decision for a candidate skill based on who the user is and what work they repeatedly need to do.

## Language Policy (Very Important)

Output language must follow user language:

- If user input is Chinese, respond in Chinese first.
- If user input is English, respond in English.
- If user mixes Chinese and English, prefer Chinese unless user explicitly asks for English.

For Chinese responses:
- Prefer Chinese decision labels: `建议安装` / `可选安装` / `不建议安装`
- You may append the English class in parentheses when needed:
  - `建议安装 (RECOMMEND_INSTALL)`
  - `可选安装 (OPTIONAL_INSTALL)`
  - `不建议安装 (DO_NOT_INSTALL)`
- Prefer Chinese field titles and explanations.
- Avoid unnecessary English terms when clear Chinese exists.

## Mandatory Pre-Read (Critical)

Before giving any install decision, always complete a "read-first" pass on the target skill.

If user provides a skill URL or repository:
1. Read the linked `SKILL.md` (or equivalent primary docs) first.
2. Extract and summarize:
   - target use cases
   - suitable users
   - unsuitable users / anti-patterns
   - core problems solved
   - setup or dependency requirements
3. Cite concrete evidence from the source content in your reasoning.
4. Only then output the final install decision.

If URL content is inaccessible (auth/network/private repo):
- explicitly say "信息不足，无法完成解读"
- request one of:
  - raw `SKILL.md` text
  - a public mirror link
  - key sections pasted by the user
- do not skip directly to a hard install decision without source evidence.

Read `references/scope-and-handoff.md` before producing a final recommendation.

## Input Contract

Collect these fields first. If key fields are missing, ask for them before judging.

Required:
- candidate skill (`name`, `url`, or package id)
- user profile (role, team type, skill maturity)
- usage scenario (single task vs repeated workflow, frequency)

Optional but useful:
- current pain point (time, quality drift, coordination cost)
- environment limits (tools, permissions, platform)

## Decision Rules

Always produce one and only one of:
- `RECOMMEND_INSTALL`
- `OPTIONAL_INSTALL`
- `DO_NOT_INSTALL`

Never output "it depends" without a final decision.

Do not output a final decision before pre-read evidence is collected, unless user explicitly says "按你已知信息先粗评".

Use these judgment signals:
1. **Frequency**: repeated workflow favors installation.
2. **Complexity**: multi-step or domain-specific workflow favors installation.
3. **Collaboration cost**: cross-person consistency needs favor installation.
4. **Learning overhead**: if setup cost is high and use is rare, do not install.
5. **Substitution quality**: if native capabilities cover 80%+ with low risk, prefer optional or no install.

## Output Template

Use this exact structure:

### Skill Read Summary
- skill primary intent
- best-fit scenarios
- suitable users
- unsuitable users
- core problems solved
- evidence source (URL/path + short quote/summary)

### Decision
`建议安装 | 可选安装 | 不建议安装`
or
`建议安装 (RECOMMEND_INSTALL) | 可选安装 (OPTIONAL_INSTALL) | 不建议安装 (DO_NOT_INSTALL)`

### Why (Evidence)
- Evidence 1 (measurable)
- Evidence 2 (measurable)

### Usage Scene Tags
- tag-1
- tag-2
- tag-3

### Value Tags
- efficiency_gain
- consistency_gain
- risk_reduction

### Suitable User Tags
- role + maturity + team context

### Unsuitable User Tags
- role + anti-pattern scenario

### Install Threshold
- Minimum condition to justify installation

### No-Install Fallback
- Practical fallback workflow without installing this skill

## Tagging Guide

Prefer concise, reusable tags:
- Scene: `high_frequency_repetition`, `cross_team_standardization`, `complex_multistep_workflow`, `low_frequency_oneoff`
- Value: `efficiency_gain`, `consistency_gain`, `risk_reduction`, `handoff_clarity`
- Profile: `pm_newbie`, `designer_pro`, `devops_team`, `solo_builder`

## Integration Notes

If the user asks to "find + decide" in one request:
1. call discovery first (via `find-skills`)
2. then evaluate top candidate(s) with this skill

If no candidate skill exists:
- state "no candidate"
- recommend using `skill-creator` to build custom capability
