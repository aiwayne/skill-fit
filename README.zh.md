# Agent Skills

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/aiwayne/agent-skills)](https://github.com/aiwayne/agent-skills/releases)

Wayne 的开源 Agent Skill 仓库，目标是把技能做成可复用、可验证、可协作的标准件。

## 当前可用技能

| Skill | 定位 | 安装命令 |
| --- | --- | --- |
| [`skill-fit`](skill-fit/README.md) | 安装决策引擎：回答“这个 skill 该不该装”并给出证据 | `npx skills add aiwayne/agent-skills@skill-fit` |

## 设计原则

- **先给强结论**：拒绝模糊建议
- **输出结构固定**：便于复核和自动化处理
- **边界清晰**：发现、判断、创建三段分离
- **最小评测集**：确保触发和不触发都可回归

## 仓库规范

每个 skill 至少包含：

- `SKILL.md`：前置触发描述 + 执行规范
- `README.md`：安装、场景、限制、示例
- `references/`：边界与交接规则
- `evals/`：触发/不触发/一致性测试样例

## 快速开始

```bash
npx skills add aiwayne/agent-skills@skill-fit
```

## 贡献说明

欢迎提 issue / PR。建议同时提供：

- 触发语境
- 期望输出结构
- 至少 1 条评测样例
