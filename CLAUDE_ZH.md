# Doc2AHP Project

[English](CLAUDE.md)

## 项目概述
Doc2AHP 是一个 Claude Code Skill，将论文 "Doc2AHP" 的结构化多准则决策方法论转化为开发者可用的决策分析工具。

## 核心原则
- **零依赖**：纯 Skill 方案，LLM 自身作为 AHP 计算引擎
- **认知约束**：每层 ≤7 准则，深度 ≤3 层（Miller's Law + 论文 K_max/D_max）
- **多视角评估**：通过角色切换模拟论文的多 Agent 机制

## 项目结构
- `skill/doc2ahp-decision/SKILL.md` — 核心 Skill 文件
- `docs/methodology.md` — 方法论详解
- `paper/PAPER_SUMMARY.md` — 论文要点摘要
- `examples/` — 使用示例

## 安装方式
用户将 `skill/doc2ahp-decision/` 复制到项目的 `.claude/skills/` 目录即可。
