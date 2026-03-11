# Skill Fit

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/aiwayne/skill-fit)](https://github.com/aiwayne/skill-fit/releases)

Open-source decision skill for one practical question:

**Should this skill be installed for this person and this usage context?**

## Install

```bash
npx skills add aiwayne/skill-fit
```

## What It Returns

- hard decision: `RECOMMEND_INSTALL` / `OPTIONAL_INSTALL` / `DO_NOT_INSTALL`
- usage scene tags
- value tags
- suitable user tags
- unsuitable user tags
- install threshold
- no-install fallback

## Skill Package Layout

- `SKILL.md`
- `agents/openai.yaml`
- `references/scope-and-handoff.md`
- `evals/evals.json`

## Chinese Translation

`skill-fit` 是一个“安装决策 skill”，只回答一个关键问题：

**这个 skill 对这个人、在这个使用场景下，到底该不该装？**

### 安装命令

```bash
npx skills add aiwayne/skill-fit
```

### 输出内容

- 强结论：`RECOMMEND_INSTALL` / `OPTIONAL_INSTALL` / `DO_NOT_INSTALL`
- 使用场景标签
- 价值标签
- 适用人群标签
- 不适合人群标签
- 安装门槛
- 不安装时替代方案

### 仓库结构

- `SKILL.md`
- `agents/openai.yaml`
- `references/scope-and-handoff.md`
- `evals/evals.json`
