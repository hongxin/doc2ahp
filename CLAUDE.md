# Doc2AHP Project

## Overview
Doc2AHP is a Claude Code Skill that transforms the structured multi-criteria decision methodology from the "Doc2AHP" paper into a practical decision analysis tool for developers.

## Core Principles
- **Zero-dependency**: Pure Skill approach — the LLM itself serves as the AHP computation engine
- **Cognitive constraints**: ≤7 criteria per level, ≤3 depth levels (Miller's Law + paper's K_max/D_max)
- **Multi-perspective evaluation**: Simulates the paper's multi-Agent mechanism through role-switching

## Project Structure
- `skill/doc2ahp-decision/SKILL.md` — Core Skill file
- `docs/methodology.md` — Detailed methodology guide
- `paper/PAPER_SUMMARY.md` — Paper key points summary
- `examples/` — Usage examples

## Installation
Copy the `skill/doc2ahp-decision/` directory into your project's `.claude/skills/` directory.
