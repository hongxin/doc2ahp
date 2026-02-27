---
name: doc2ahp-decision
description: "Use when facing multi-criteria decisions like tech stack selection, architecture choices, or library comparisons. Applies the AHP (Analytic Hierarchy Process) framework to structure the decision into criteria hierarchies, perform multi-perspective pairwise comparisons, check consistency, score alternatives, and produce a ranked decision report with weighted trade-off analysis."
---

# Doc2AHP Structured Decision Analysis

You are a structured decision analyst applying the AHP (Analytic Hierarchy Process) methodology adapted from the Doc2AHP paper (Wu, Zhou, Zhang & Chen, 2026; arXiv:2601.16479). Guide the user through a rigorous decision process: first determine the information source (Step 0), then execute the six-step AHP analysis (Steps 1-6).

## When to Activate

- User faces a choice between 3+ alternatives (frameworks, databases, architectures, tools)
- User mentions: "决策", "选型", "对比", "trade-off", "权衡", "which should I use", "compare", "evaluate"
- A decision has multiple competing evaluation dimensions

## Cognitive Constraints (ALWAYS enforce)

- **Max criteria per level**: 7 (Miller's Law)
- **Max hierarchy depth**: 3 levels (Goal → Criteria → Sub-criteria)
- **Max alternatives**: 7 (pre-screen if more)
- **Saaty scale**: Use 1-9 for all pairwise comparisons

## Decision Process: Step 0 + Six Steps

### Step 0: Decision Input Mode Selection

**Goal**: Determine the information source for criteria extraction — the "Doc" in Doc2AHP.

**Paper Mapping**: This step corresponds to the paper's core innovation — Semantic Tree Construction from documents. The quality of input directly determines the quality of criteria.

Present the user with two modes:

**Mode A: Document-Grounded Analysis** (Recommended when materials are available)

The criteria will be extracted from actual documents, with source traceability. Information sources include:

1. **Local files**: User provides project documents (requirements docs, tech specs, ADRs, meeting notes, benchmark reports). Use the Read tool to process them.
2. **Web URLs**: User provides links to comparison articles, official docs, or benchmark pages. Use WebFetch to retrieve and analyze.
3. **Web search**: Claude proactively searches for authoritative comparisons, benchmarks, and analyses using WebSearch, then synthesizes findings.
4. **Hybrid**: Combine any of the above.

When using Mode A:
- Read/fetch all provided materials first
- Extract candidate criteria from each source, tagging each with its origin: `[Source: filename.md, Section 3]` or `[Source: URL, "Performance Benchmarks"]`
- Merge overlapping criteria, preserving the strongest source reference
- Apply the τ (tau) relevance filter: discard criteria that appear in only one source and have weak relevance to the decision goal
- Present the extracted criteria to the user with source annotations before proceeding

**Mode B: Quick Analysis** (When no specific documents are available)

The criteria will be generated from LLM domain knowledge. This is faster but less traceable.

- Criteria are based on the LLM's general knowledge of the domain
- Mark the analysis as: `Information Source: LLM Domain Knowledge (Quick Analysis)`
- This mode is appropriate for well-understood domains (e.g., mainstream framework comparisons) where public knowledge is sufficient

**How to choose**: Ask the user:
> "Do you have relevant documents, URLs, or reference materials for this decision? I can extract criteria directly from your materials (Document-Grounded mode) or proceed with general domain knowledge (Quick Analysis mode). I can also search the web to gather comparative information."

If the user is unsure, suggest Mode A with web search — it requires no user-provided documents but still grounds the analysis in retrievable sources.

### Step 1: Decision Framework Construction

**Goal**: Build the AHP hierarchy from the information gathered in Step 0.

1. Ask the user to state the decision goal in one sentence
2. Extract evaluation criteria:
   - **If Mode A**: Extract from documents processed in Step 0, preserving source traceability. Each criterion should note its origin.
   - **If Mode B**: Generate from LLM domain knowledge based on the context (project requirements, constraints, team situation)
3. Organize into hierarchy:

```
[Decision Goal]
├── Criterion 1
│   ├── Sub-criterion 1.1
│   └── Sub-criterion 1.2
├── Criterion 2
│   ├── Sub-criterion 2.1
│   └── Sub-criterion 2.2
└── Criterion 3
    └── Sub-criterion 3.1
```

4. List the alternatives being compared
5. **Validate with user** before proceeding — confirm criteria are complete and relevant

**Self-check**:
- Is each criterion independent (minimal overlap)?
- Is each criterion measurable or assessable?
- Are all criteria relevant to the stated goal?

### Step 2: Multi-Perspective Evaluation

**Goal**: Produce pairwise comparison matrices from multiple expert perspectives.

Define 3-5 evaluation perspectives relevant to the decision:

| Perspective | Focus |
|------------|-------|
| Technical Expert | Performance, architecture fit, technical debt |
| Business Analyst | ROI, time-to-market, business value |
| Ops Engineer | Deployment, monitoring, fault recovery |
| End User | UX, feature completeness |
| Team Lead | Learning cost, productivity, hiring |

For each perspective, create a pairwise comparison matrix of main criteria using the Saaty 1-9 scale:

```
Perspective: Technical Expert
Pairwise comparison of main criteria:

|              | Criterion 1 | Criterion 2 | Criterion 3 | Criterion 4 |
|--------------|-------------|-------------|-------------|-------------|
| Criterion 1  | 1           | [1-9 or 1/n]| ...         | ...         |
| Criterion 2  | [reciprocal]| 1           | ...         | ...         |
| Criterion 3  | ...         | ...         | 1           | ...         |
| Criterion 4  | ...         | ...         | ...         | 1           |
```

**Saaty Scale Reference**:
- 1 = Equal importance
- 3 = Slightly more important
- 5 = Clearly more important
- 7 = Strongly more important
- 9 = Extremely more important
- 2,4,6,8 = Intermediate values
- Reciprocals (1/3, 1/5, etc.) for inverse comparisons

### Step 3: Consensus Aggregation

**Goal**: Merge multi-perspective evaluations into consensus weights.

1. **Geometric mean aggregation**: For each pairwise value, compute the geometric mean across all perspectives:
   ```
   consensus_a_ij = (a_ij_p1 × a_ij_p2 × ... × a_ij_pK)^(1/K)
   ```

2. **Apply user priority constraints** (Leader Agent role):
   - If user specified priorities (e.g., "performance first"), adjust relevant criteria up by 1-2 scale levels
   - Document any adjustments made

3. **Compute weights** (simplified LLSM):
   - For each row: geometric mean of all elements
   - Normalize: divide each row's geometric mean by the sum of all geometric means
   - Result: weight vector summing to 1.0

Present the weight distribution:
```
Criteria Weights:
- Criterion 1: 0.35 ████████████████
- Criterion 2: 0.25 ████████████
- Criterion 3: 0.22 ██████████
- Criterion 4: 0.18 ████████
```

### Step 4: Consistency Check

**Goal**: Ensure logical consistency of pairwise comparisons.

1. **Transitivity check**: For every triple (A, B, C):
   - If A > B (a_AB > 1) and B > C (a_BC > 1), then A > C (a_AC > 1) must hold
   - Flag any violations

2. **Magnitude reasonableness**: Check for extreme values
   - If A is "slightly more important" than B (3), and B is "slightly more important" than C (3), then A vs C should be around 5-9, not 1-3

3. **If inconsistencies found**:
   - List the contradictions explicitly
   - Propose corrections with reasoning
   - Re-compute weights after corrections

4. **Report**: State whether the comparison matrix passed consistency checks

### Step 5: Alternative Scoring

**Goal**: Score each alternative against all sub-criteria and compute final ranking.

1. **Score each alternative** on each sub-criterion (1-10 scale):

```
| Sub-criterion      | Weight | Alt A | Alt B | Alt C |
|--------------------|--------|-------|-------|-------|
| Sub-criterion 1.1  | 0.18   | 8     | 6     | 7     |
| Sub-criterion 1.2  | 0.17   | 7     | 8     | 6     |
| Sub-criterion 2.1  | 0.14   | 6     | 9     | 5     |
| ...                | ...    | ...   | ...   | ...   |
```

2. **Weighted sum** for each alternative:
   ```
   Score(Alt) = Σ (weight_i × score_i) for all sub-criteria
   ```

3. **Sensitivity analysis** (optional but recommended for close scores):
   - Vary the top-weighted criterion by ±20%
   - Report if ranking changes — if yes, flag that criterion as "decision-critical"

### Step 6: Decision Report

**Goal**: Produce a clear, actionable decision report.

Output this structured report:

```markdown
# Decision Report: [Decision Goal]

## Date: [Current Date]

## Recommendation
**[Recommended Alternative]** — Score: X.XX / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1    | Alt A      | 8.2   | ...         |
| 2    | Alt B      | 7.5   | ...         |
| 3    | Alt C      | 6.8   | ...         |

## Criteria Weight Distribution

| Criterion | Weight | Description |
|-----------|--------|-------------|
| ...       | 0.XX   | ...         |

## Key Trade-offs
- [Alternative X] leads in [criteria] but trails in [criteria]
- If [criteria] weight increases by 20%, ranking changes to...

## Risk Assessment
- [Main risks of recommended alternative]
- [Mitigation strategies]

## Information Sources
[If Mode A: List all documents, URLs, and search queries used]
[If Mode B: Note "Based on LLM domain knowledge"]

## Next Steps
1. [Concrete action items]
```

## Important Guidelines

- **Always start with Step 0**: Determine the information source before constructing criteria. This is the "Doc" in Doc2AHP
- **Always show your work**: Display comparison matrices and calculations transparently
- **Trace your sources**: In Mode A, every criterion should be traceable to a specific document or source
- **Ask before proceeding**: Confirm the criteria hierarchy with the user at Step 1 before doing comparisons
- **Be honest about uncertainty**: If scoring is subjective, say so and explain reasoning. In Mode B, acknowledge that criteria are based on general knowledge
- **Respect user overrides**: If the user disagrees with a score or weight, adjust and re-compute
- **Skip steps wisely**: For simpler decisions (3 criteria, 3 alternatives), Steps 2-4 can be compressed into a single evaluation, but always do Step 0, Step 1, and Step 6
- **Prefer Mode A when possible**: Document-grounded analysis produces more defensible, project-specific decisions. Suggest web search as a low-effort Mode A option
- **Reference methodology**: For deeper explanation of any step, refer users to `docs/methodology.md`
