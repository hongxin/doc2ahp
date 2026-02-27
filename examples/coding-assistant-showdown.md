# Example: AI Coding Assistant Selection

[中文](coding-assistant-showdown_ZH.md)

> Scenario: A 30-person engineering team working on a complex microservices backend (Go, TypeScript, Python) wants to adopt an AI coding assistant to boost productivity. After a 2-week trial of all three tools, the team needs to make a decision. Budget: $30-50/developer/month. The CTO's directive: "Pick one, standardize, and measure the impact."

## Step 1: Decision Framework Construction

**Decision Goal**: Select the AI coding assistant that delivers the highest productivity impact for a polyglot backend engineering team

**Evaluation Hierarchy**:

```
Select the Best AI Coding Assistant
├── Code Intelligence
│   ├── Code Completion Quality (accuracy, relevance)
│   ├── Codebase-aware Context (repo understanding)
│   └── Multi-language Support (Go, TS, Python equally)
├── Workflow Integration
│   ├── IDE/Editor Fit (VS Code, JetBrains, Vim)
│   ├── Git & PR Workflow (review, commit messages)
│   └── Terminal & CLI Capabilities
├── Team Adoption
│   ├── Onboarding Friction (time to productive use)
│   ├── Consistency Across Skill Levels (junior vs senior benefit)
│   └── Knowledge Sharing (patterns, conventions)
└── Value
    ├── Pricing Model (per-seat, usage-based, enterprise)
    ├── Measurable Productivity Impact
    └── Privacy & Security (code data handling)
```

**Alternatives**:
- **GitHub Copilot** (Business plan, $19/user/month)
- **Cursor** (Pro plan, $20/user/month)
- **Claude Code** (Max plan, $100/user/month with broader Claude access)

## Step 2: Multi-Perspective Evaluation

### Perspective 1: Senior Backend Engineer (daily user)

| vs | Code Intelligence | Workflow Integration | Team Adoption | Value |
|----|-------------------|---------------------|---------------|-------|
| Code Intelligence | 1 | 2 | 3 | 2 |
| Workflow Integration | 1/2 | 1 | 2 | 1 |
| Team Adoption | 1/3 | 1/2 | 1 | 1/2 |
| Value | 1/2 | 1 | 2 | 1 |

### Perspective 2: Engineering Manager (team-level concerns)

| vs | Code Intelligence | Workflow Integration | Team Adoption | Value |
|----|-------------------|---------------------|---------------|-------|
| Code Intelligence | 1 | 1 | 1/2 | 1 |
| Workflow Integration | 1 | 1 | 1 | 1 |
| Team Adoption | 2 | 1 | 1 | 2 |
| Value | 1 | 1 | 1/2 | 1 |

### Perspective 3: CTO (strategic, ROI-focused)

| vs | Code Intelligence | Workflow Integration | Team Adoption | Value |
|----|-------------------|---------------------|---------------|-------|
| Code Intelligence | 1 | 1/2 | 1 | 1/3 |
| Workflow Integration | 2 | 1 | 2 | 1 |
| Team Adoption | 1 | 1/2 | 1 | 1/2 |
| Value | 3 | 1 | 2 | 1 |

## Step 3: Consensus Aggregation

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Code Intelligence | 1.00 | 0.24 |
| Workflow Integration | 1.10 | 0.27 |
| Team Adoption | 0.89 | 0.22 |
| Value | 1.05 | 0.27 |

**Weight Distribution**:
```
Workflow Integration: 0.27 █████████████
Value:                0.27 █████████████
Code Intelligence:    0.24 ████████████
Team Adoption:        0.22 ███████████
```

## Step 4: Consistency Check

**Transitivity Verification**:
- Workflow Integration ≈ Value > Code Intelligence > Team Adoption ✓
- Workflow Integration > Team Adoption ✓
- Value > Code Intelligence ✓
- All transitive relationships are consistent ✓

**Note**: The remarkably even weight distribution (0.22-0.27) reflects that all four criteria genuinely matter for this decision — there's no single dominant factor.

## Step 5: Alternative Scoring

| Sub-criterion | Weight | Copilot | Cursor | Claude Code |
|---------------|--------|---------|--------|-------------|
| Code Completion Quality | 0.09 | 7 | 9 | 8 |
| Codebase-aware Context | 0.08 | 6 | 8 | 9 |
| Multi-language Support | 0.07 | 8 | 8 | 8 |
| IDE/Editor Fit | 0.10 | 9 | 8 | 6 |
| Git & PR Workflow | 0.09 | 7 | 7 | 9 |
| Terminal & CLI | 0.08 | 4 | 5 | 10 |
| Onboarding Friction | 0.08 | 9 | 8 | 6 |
| Cross-skill-level Benefit | 0.07 | 7 | 8 | 8 |
| Knowledge Sharing | 0.07 | 5 | 6 | 8 |
| Pricing Model | 0.10 | 9 | 9 | 5 |
| Productivity Impact | 0.09 | 7 | 8 | 9 |
| Privacy & Security | 0.08 | 7 | 6 | 8 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **Claude Code** | **7.68** |
| **Cursor** | **7.50** |
| **Copilot** | **7.02** |

### Sensitivity Analysis

Scenario A — Increasing "Value" weight from 0.27 to 0.40 (strict budget):
- Copilot: 7.22 → **Rank 1** (pricing advantage dominates)
- Cursor: 7.30 → Rank 1 (near tie)
- Claude Code: 6.95 → Rank 3 (premium pricing hurts)

Scenario B — Increasing "Workflow Integration" weight from 0.27 to 0.40 (workflow-centric team):
- Claude Code: 7.92 → **Rank 1** (CLI and Git workflow advantages shine)
- Cursor: 7.35 → Rank 2
- Copilot: 6.85 → Rank 3

Scenario C — Increasing "Code Intelligence" weight to 0.40 (quality-over-cost):
- Cursor: 7.82 → **Rank 1** (completion quality advantage)
- Claude Code: 7.65 → Rank 2
- Copilot: 6.88 → Rank 3

**Key Finding**: This is a genuinely close three-way race. Claude Code wins on deep codebase understanding and workflow integration; Cursor wins on raw completion quality; Copilot wins on price and IDE ubiquity. The "right" choice depends heavily on team workflow style.

## Step 6: Decision Report

# Decision Report: AI Coding Assistant Selection

## Recommendation
**Claude Code** — Overall Score: 7.68 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | Claude Code | 7.68 | Deepest codebase understanding, best terminal/CLI workflow, strongest Git integration |
| 2 | Cursor | 7.50 | Best inline completion quality, excellent editor experience, strong code context |
| 3 | Copilot | 7.02 | Most affordable, widest IDE support, lowest onboarding friction |

## Key Trade-offs
- **Claude Code vs Cursor (0.18-point gap)**: Claude Code excels at complex, multi-file tasks and terminal-native workflows. Cursor excels at the "in-editor flow" — inline completions while typing. Teams that live in the terminal will prefer Claude Code; teams that live in the editor will prefer Cursor
- **The pricing elephant**: Claude Code at $100/user/month is 5x Copilot's price. For 30 engineers, that's $3,000/month vs $570/month. The productivity impact must justify the premium. Trial data suggests Claude Code saves 45-60 min/developer/day vs 20-30 min for Copilot — the ROI math works, but it's a bigger commitment
- **Copilot's silent advantage**: Nearly zero onboarding friction. It works in every IDE, feels invisible, and every developer has heard of it. Don't underestimate the value of "it just works" for team-wide adoption

## Risk Assessment
- Claude Code's terminal-first paradigm may not suit developers who prefer a fully visual IDE experience
- Cursor's code context features are excellent but require configuration for monorepo setups
- Copilot's tab-completion model may lead to accepting low-quality suggestions under time pressure
- All three tools raise code privacy concerns; review each provider's data retention and training policies

## Recommendations
1. Adopt Claude Code as the primary AI assistant for backend engineers who work with complex, multi-service codebases
2. Allow Cursor as an alternative for frontend engineers and those who prefer in-editor completion
3. Run a 30-day measured trial: track PR throughput, cycle time, and developer satisfaction surveys
4. Establish team guidelines for AI-assisted code: review all AI-generated code as you would a junior developer's PR
5. Re-evaluate in 6 months — this market evolves faster than any other developer tool category
