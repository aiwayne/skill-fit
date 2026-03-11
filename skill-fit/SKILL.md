---
name: skill-fit
description: Decide whether a skill should be installed for a specific user profile and task context. Use this whenever users ask "该不该装这个skill", "适不适合我", "值不值得装", "适用场景", "适合/不适合人群", or request a clear install recommendation. Always output a hard decision: RECOMMEND_INSTALL, OPTIONAL_INSTALL, or DO_NOT_INSTALL, with profile and scenario tags.
---

# Skill Fit

Make a strong install decision for a candidate skill based on who the user is and what work they repeatedly need to do.

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

Use these judgment signals:
1. **Frequency**: repeated workflow favors installation.
2. **Complexity**: multi-step or domain-specific workflow favors installation.
3. **Collaboration cost**: cross-person consistency needs favor installation.
4. **Learning overhead**: if setup cost is high and use is rare, do not install.
5. **Substitution quality**: if native capabilities cover 80%+ with low risk, prefer optional or no install.

## Output Template

Use this exact structure:

### Decision
`RECOMMEND_INSTALL | OPTIONAL_INSTALL | DO_NOT_INSTALL`

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
