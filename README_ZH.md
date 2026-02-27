# Doc2AHP

**将学术决策理论转化为开发者的实用工具**

[English](README.md)

Doc2AHP 是一个 Claude Code Skill，基于论文 *"Doc2AHP: Inferring Structured Multi-Criteria Decision Models via Semantic Trees with LLMs"* 的核心原理，为开发者提供结构化多准则决策分析能力。

## 解决什么问题？

技术选型、架构决策、库对比——这些决策往往：
- 涉及多个相互冲突的评估维度
- 依赖个人直觉而非系统分析
- 缺乏可追溯的决策过程记录

Doc2AHP 通过 AHP（层次分析法）框架，将模糊的"感觉"转化为可量化、可追溯的结构化决策。

## 快速开始

### 安装

将 `skill/doc2ahp-decision/` 目录复制到你项目的 `.claude/skills/` 下：

```bash
# 在你的项目根目录
mkdir -p .claude/skills
cp -r path/to/doc2ahp/skill/doc2ahp-decision .claude/skills/
```

### 使用

在 Claude Code 中描述你的决策场景，Skill 会自动引导你完成六步决策流程：

1. **框架构建** — 明确目标、提取准则、构建层次
2. **多视角评估** — 从技术、业务、运维等角度独立评估
3. **共识聚合** — 合并多视角为共识权重
4. **一致性校验** — 确保判断逻辑一致
5. **方案评分** — 加权评分得出排名
6. **决策报告** — 输出结构化可存档的报告

## 示例

| 场景 | 文件 |
|-----|------|
| 前端框架选型 | [examples/tech-stack-selection_ZH.md](examples/tech-stack-selection_ZH.md) |
| 架构方案决策 | [examples/architecture-decision_ZH.md](examples/architecture-decision_ZH.md) |
| 状态管理库对比 | [examples/library-comparison_ZH.md](examples/library-comparison_ZH.md) |
| AI 大模型 API 选型 | [examples/ai-model-selection_ZH.md](examples/ai-model-selection_ZH.md) |
| 高并发交易系统语言之争 | [examples/language-holy-war_ZH.md](examples/language-holy-war_ZH.md) |
| 资深开发者职业路径决策 | [examples/career-path-decision_ZH.md](examples/career-path-decision_ZH.md) |
| 千万用户社交 App 数据库选型 | [examples/database-selection_ZH.md](examples/database-selection_ZH.md) |
| AI 编程助手大乱斗 | [examples/coding-assistant-showdown_ZH.md](examples/coding-assistant-showdown_ZH.md) |

## 核心理念

- **零依赖**：纯 Skill 方案，LLM 自身作为 AHP 计算引擎
- **认知约束**：每层 ≤7 准则，深度 ≤3 层，基于 Miller's Law
- **多视角评估**：模拟论文的多 Agent 机制，减少单一视角偏差
- **一致性检验**：通过传递性检查确保逻辑自洽

## 项目结构

```
doc2ahp/
├── skill/doc2ahp-decision/   # Claude Code Skill（核心）
├── docs/methodology_ZH.md     # 方法论详解
├── paper/PAPER_SUMMARY_ZH.md  # 论文要点摘要
└── examples/                  # 使用示例
```

## 适用场景

**适合**：3+ 备选方案、多维度权衡、架构级决策、需要向团队解释理由

**不适合**：二选一简单对比、单一维度决策、紧急决策

## 深入了解

- [方法论详解](docs/methodology_ZH.md) — 论文方法到实践的完整映射
- [论文摘要](paper/PAPER_SUMMARY_ZH.md) — Doc2AHP 论文核心要点

## Citation

如果本项目的 Skill / 方法论 / 示例对你的工作有帮助，请引用原始论文：

```bibtex
@article{Wu2026Doc2AHP,
    author    = {Hongjia Wu and Shuai Zhou and Hongxin Zhang and Wei Chen},
    title     = {Doc2AHP: Inferring Structured Multi-Criteria Decision Models via Semantic Trees with LLMs},
    journal   = {arXiv preprint arXiv:2601.16479},
    year      = {2026},
    doi       = {10.48550/arXiv.2601.16479}
}
```

## License

[MIT](LICENSE)
