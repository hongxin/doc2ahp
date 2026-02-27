# Doc2AHP

**Turning academic decision theory into a practical tool for developers**

[中文](README_ZH.md)

Doc2AHP is a Claude Code Skill that brings structured multi-criteria decision analysis to software engineering, based on the principles from the paper *"Doc2AHP: Inferring Structured Multi-Criteria Decision Models via Semantic Trees with LLMs"*.

## The Problem

Tech stack selection, architecture decisions, library comparisons — these decisions often:
- Involve multiple conflicting evaluation dimensions
- Rely on gut feeling rather than systematic analysis
- Lack traceable decision records

Doc2AHP uses the AHP (Analytic Hierarchy Process) framework to transform vague "feelings" into quantifiable, traceable, structured decisions.

## Two Input Modes

Doc2AHP supports two ways to begin a decision analysis:

- **Mode A: Document-Grounded** — Extract criteria from actual documents (requirements docs, tech specs, web search results) with full source traceability. Faithful to the paper's "Doc → AHP" pipeline. [See example](examples/doc-grounded-cloud-selection.md)
- **Mode B: Quick Analysis** — Generate criteria from LLM domain knowledge for rapid exploration. Faster, but less traceable.

## Quick Start

### Installation

Copy the `skill/doc2ahp-decision/` directory into your project's `.claude/skills/`:

```bash
# In your project root
mkdir -p .claude/skills
cp -r path/to/doc2ahp/skill/doc2ahp-decision .claude/skills/
```

### Usage

Describe your decision scenario in Claude Code. The skill will guide you through the decision process:

0. **Input Mode Selection** — Choose Document-Grounded or Quick Analysis mode
1. **Framework Construction** — Define goal, extract criteria, build hierarchy
2. **Multi-Perspective Evaluation** — Evaluate from technical, business, ops perspectives
3. **Consensus Aggregation** — Merge perspectives into consensus weights
4. **Consistency Check** — Ensure logical consistency of judgments
5. **Alternative Scoring** — Weighted scoring to produce rankings
6. **Decision Report** — Structured, archivable report output

## Examples

| Scenario | File |
|----------|------|
| Frontend Framework Selection | [examples/tech-stack-selection.md](examples/tech-stack-selection.md) |
| Architecture Decision | [examples/architecture-decision.md](examples/architecture-decision.md) |
| State Management Library Comparison | [examples/library-comparison.md](examples/library-comparison.md) |
| AI Foundation Model API Selection | [examples/ai-model-selection.md](examples/ai-model-selection.md) |
| Programming Language for Trading System | [examples/language-holy-war.md](examples/language-holy-war.md) |
| Senior Developer Career Path | [examples/career-path-decision.md](examples/career-path-decision.md) |
| Database for Social App at Scale | [examples/database-selection.md](examples/database-selection.md) |
| AI Coding Assistant Showdown | [examples/coding-assistant-showdown.md](examples/coding-assistant-showdown.md) |
| Cloud Provider Selection (Document-Grounded Mode) | [examples/doc-grounded-cloud-selection.md](examples/doc-grounded-cloud-selection.md) |
| JS Runtime Selection (Real Data, Full Calculation) | [examples/js-runtime-selection/](examples/js-runtime-selection/) |

## Core Principles

- **Zero Dependencies**: Pure Skill approach — the LLM itself is the AHP computation engine
- **Cognitive Constraints**: Max 7 criteria per level, max 3 depth levels (Miller's Law)
- **Multi-Perspective Evaluation**: Simulates the paper's multi-agent mechanism to reduce single-viewpoint bias
- **Consistency Verification**: Transitivity checks ensure logical coherence

## Project Structure

```
doc2ahp/
├── skill/doc2ahp-decision/   # Claude Code Skill (core)
├── docs/methodology.md        # Detailed methodology
├── paper/PAPER_SUMMARY.md     # Paper summary
└── examples/                  # Usage examples
```

## When to Use

**Good fit**: 3+ alternatives, multi-dimensional trade-offs, architecture-level decisions, need to explain rationale to team

**Not ideal**: Simple A/B choices, single-dimension decisions, urgent decisions

## Learn More

- [Methodology](docs/methodology.md) — Full mapping from paper to practice
- [Paper Summary](paper/PAPER_SUMMARY.md) — Core concepts from the Doc2AHP paper

## Citation

If the skill / methodology / examples in this project help your work, please cite the original paper:

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
