# Doc2AHP Methodology: From Paper to Software Decision Practice

[中文](methodology_ZH.md)

## Overview

This document maps the academic methodology of the Doc2AHP paper (Wu, Zhou, Zhang & Chen, 2026; [arXiv:2601.16479](https://arxiv.org/abs/2601.16479)) to software engineering decision scenarios, providing methodological support for the Skill implementation.

## 1. Decision Scenario Classification

### 1.1 Technology Selection Decisions

**Scenario**: Choosing programming languages, frameworks, databases, cloud services, etc.
**Characteristics**: Alternatives are well-defined, evaluation dimensions are diverse
**Typical Criteria Hierarchy**:

```
Select the Best Technology
├── Technical Fit
│   ├── Feature Completeness
│   ├── Performance Characteristics
│   └── Ecosystem Maturity
├── Team Factors
│   ├── Learning Curve
│   ├── Existing Skill Match
│   └── Hiring Market
├── Engineering Quality
│   ├── Maintainability
│   ├── Testing Support
│   └── Documentation Quality
└── Business Factors
    ├── License Compliance
    ├── Total Cost of Ownership
    └── Vendor Lock-in Risk
```

### 1.2 Architecture Decisions

**Scenario**: Microservices vs monolith, event-driven vs request-response, SQL vs NoSQL, etc.
**Characteristics**: Far-reaching impact, difficult to reverse, requires multi-party trade-offs
**Typical Criteria Hierarchy**:

```
Select the Best Architecture Approach
├── Scalability
│   ├── Horizontal Scaling Capability
│   └── Data Partitioning Strategy
├── Reliability
│   ├── Fault Tolerance Mechanism
│   └── Data Consistency
├── Development Efficiency
│   ├── Development Complexity
│   ├── Deployment Complexity
│   └── Debugging Difficulty
└── Operational Cost
    ├── Infrastructure Cost
    └── Monitoring Complexity
```

### 1.3 Library/Tool Comparison

**Scenario**: React vs Vue, PostgreSQL vs MySQL, Jest vs Vitest, etc.
**Characteristics**: Alternatives have similar functionality, differences lie in the details
**Typical Criteria Hierarchy**:

```
Select the Best Library/Tool
├── Feature Match
│   ├── Core Feature Coverage
│   └── Extensibility
├── Developer Experience
│   ├── API Design
│   ├── Type Support
│   └── Error Message Quality
├── Community Ecosystem
│   ├── Community Activity
│   ├── Third-party Plugins
│   └── Long-term Maintenance Confidence
└── Integration Cost
    ├── Migration Difficulty
    └── Compatibility with Existing Stack
```

## 2. Decision Process in Detail: Step 0 + Six Steps

### Step 0: Decision Input Mode Selection

**Paper Mapping**: Document Input & Semantic Tree Construction — the "Doc" in Doc2AHP

The original paper's core innovation is transforming **unstructured documents** into structured AHP hierarchies through embedding and hierarchical clustering. Step 0 preserves this critical first stage by giving users an explicit choice about information sources.

**Two Modes**:

| Aspect | Mode A: Document-Grounded | Mode B: Quick Analysis |
|--------|--------------------------|----------------------|
| Input | User-provided documents, URLs, or web search results | User's verbal scenario description |
| Criteria extraction | From document content, with source traceability | From LLM's domain knowledge |
| Paper alignment | Faithful to the Doc2AHP pipeline | Simplified — skips the "Doc" stage |
| Traceability | Each criterion tagged with `[Source: doc, section]` | Criteria origin is implicit |
| Best for | High-stakes decisions, compliance-sensitive, team buy-in needed | Well-understood domains, rapid exploration, personal decisions |

**Mode A Information Sources**:
1. **Local files**: Requirements docs, tech specs, ADRs, meeting notes, benchmark reports
2. **Web URLs**: Comparison articles, official documentation, benchmark pages
3. **Web search**: Claude proactively searches for authoritative sources
4. **Hybrid**: Combine any of the above

**Mode A: τ (tau) Relevance Filter**:
After extracting candidate criteria from all documents, apply the relevance filter:
- Keep criteria that appear in multiple sources OR have strong relevance to the decision goal
- Filter out criteria that appear in only one source with weak relevance
- Document what was filtered and why

**When to recommend Mode A over Mode B**:
- Decision affects multiple stakeholders who need to understand the rationale
- Compliance or audit requirements demand traceable decision records
- The decision domain is specialized (healthcare, fintech, security) where general knowledge may be insufficient
- The team has existing research or analysis documents worth leveraging

See the [Document-Grounded Cloud Selection example](../examples/doc-grounded-cloud-selection.md) for a complete Mode A walkthrough.

### Step 1: Decision Framework Construction

**Paper Mapping**: Semantic Tree Construction (criteria organization stage)

**Operating Procedure**:

1. **Define the decision goal**: Describe the decision problem in one sentence
2. **Extract criteria**:
   - **Mode A**: Extract from documents processed in Step 0, tagging each criterion with its source reference
   - **Mode B**: Pull evaluation dimensions from project context, requirements docs, team discussions
3. **Build hierarchy**: Organize criteria as Goal → Main Criteria → Sub-criteria → Alternatives
4. **Cognitive constraint check**:
   - ≤ 7 criteria per level (Miller's Law)
   - ≤ 3 hierarchy depth levels (including goal level)
   - Self-check each criterion's relevance to the goal

**Criteria Extraction Heuristics**:
- Start from "what would make a user choose or reject this alternative"
- Reference existing ADR (Architecture Decision Records) templates
- Consider both short-term and long-term impacts

### Step 2: Multi-Perspective Evaluation

**Paper Mapping**: Multi-Agent Weighting Mechanism

**Operating Procedure**:

1. **Define evaluation perspectives** (recommended 3-5):

| Perspective | Focus Area |
|------------|------------|
| Technical Expert | Performance, architecture fit, technical debt |
| Business Analyst | ROI, market responsiveness, business value |
| Ops Engineer | Deployment complexity, monitoring, fault recovery |
| End User | Experience fluidity, feature completeness |
| Team Lead | Learning cost, team productivity, hiring |

2. **Independent pairwise comparisons**: Each perspective performs pairwise comparisons of main criteria

Pairwise comparison template (Saaty 1-9 scale):

```
Perspective: Technical Expert
Compare relative importance of main criteria:

| vs               | Technical Fit | Team Factors | Eng. Quality | Business Factors |
|------------------|--------------|-------------|-------------|-----------------|
| Technical Fit    | 1            | 3           | 2           | 5               |
| Team Factors     | 1/3          | 1           | 1/2         | 3               |
| Eng. Quality     | 1/2          | 2           | 1           | 4               |
| Business Factors | 1/5          | 1/3         | 1/4         | 1               |
```

**Saaty Scale Interpretation**:
- 1 = Equal importance
- 3 = Slightly more important (mild preference)
- 5 = Clearly more important (strong preference)
- 7 = Strongly more important (dominant)
- 9 = Extremely more important (overwhelming advantage)

### Step 3: Consensus Aggregation

**Paper Mapping**: Weighted Geometric Mean + Leader Agent

**Operating Procedure**:

1. **Geometric mean aggregation**: For each pairwise comparison value, take the geometric mean across all perspectives

```
Consensus value a_ij = (a_ij_perspective1 × a_ij_perspective2 × ... × a_ij_perspectiveK)^(1/K)
```

2. **Apply Leader constraints**: Adjust based on user-specified priorities

For example, if the user says "performance first":
- Identify criteria related to performance
- In the aggregated matrix, moderately increase the relative weight of that criterion
- Adjustment magnitude: 1-2 scale levels

3. **Weight calculation** (simplified LLSM):
- Compute the geometric mean of elements in each row
- Normalize to obtain final weights

### Step 4: Consistency Verification

**Paper Mapping**: Adaptive Consistency Optimization

**Operating Procedure**:

1. **Transitivity check**:
   - If A is more important than B (a_AB > 1), and B is more important than C (a_BC > 1)
   - Then A must be more important than C (a_AC > 1)
   - Violating this rule indicates inconsistency

2. **Inconsistency correction strategy**:
   - List all triples and check transitivity
   - For inconsistent comparisons, re-evaluate and adjust
   - Prioritize preserving high-confidence comparisons; adjust low-confidence ones

3. **Simplified consistency indicator**:
   - For LLM-executed scenarios, precise CR calculation is not required
   - Transitivity checks + reasonableness self-checks are sufficient
   - If obvious contradictions are found, flag and correct them

### Step 5: Alternative Scoring

**Paper Mapping**: Utility Scoring

**Operating Procedure**:

1. **Score per criterion**: Rate each alternative on each sub-criterion (1-10 scale)

```
| Sub-criterion       | Weight | Alt A | Alt B | Alt C |
|---------------------|--------|-------|-------|-------|
| Feature Completeness | 0.15  | 8     | 7     | 9     |
| Performance          | 0.12  | 9     | 6     | 7     |
| Learning Curve       | 0.10  | 5     | 8     | 6     |
| ...                  | ...   | ...   | ...   | ...   |
```

2. **Weighted aggregation**:

```
Alternative Score = Σ (criterion weight × alternative's score on that criterion)
```

3. **Sensitivity analysis** (optional):
   - Adjust key criterion weights by ±20% and observe whether rankings change
   - If rankings remain stable → conclusion is robust
   - If rankings change → flag that criterion as a "decision-critical factor"

### Step 6: Decision Report

**Paper Mapping**: Report Generation

**Output Format**:

```markdown
# Decision Report: [Decision Goal]

## Recommendation
**[Alternative Name]** — Overall Score: X.XX / 10

## Ranking
| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1    | Alt A      | 8.2   | ...         |
| 2    | Alt B      | 7.5   | ...         |
| 3    | Alt C      | 6.8   | ...         |

## Criteria Weight Distribution
[List each criterion and its final weight]

## Key Trade-offs
- Alt A leads in X but trails Alt B in Y
- If criterion Z's weight increases by 20%, the ranking changes to...

## Risk Assessment
[List main risks of the recommended alternative and mitigation strategies]

## Recommendations
[Clear action items, including next steps]
```

## 3. Theoretical Basis for Cognitive Constraints

### Miller's Law (7±2 Rule)

Human working memory capacity is approximately 7±2 information chunks. Therefore:
- Limiting criteria to ≤ 7 per level ensures decision-makers can consider all criteria simultaneously
- Alternatives should be ≤ 5; if more, pre-screen first

### Paper's K_max and D_max

- **K_max** (max branches per level): Paper experiments show 5-7 as the optimal range
- **D_max** (max depth): 3 levels (Goal–Criteria–Sub-criteria) is sufficient for the vast majority of scenarios

### Why More Detail Isn't Always Better

- Excessive depth → weights become overly diluted; tiny differences skew results
- Too many criteria → pairwise comparison matrices grow exponentially; consistency becomes hard to ensure
- Over-decomposition → decision-maker cognitive overload, which actually degrades decision quality

## 4. Applicability Boundaries

### Scenarios Where Doc2AHP Is Well-Suited

- 3+ clearly defined alternatives exist
- ≥ 3 evaluation dimensions with trade-off relationships between them
- Decision has significant impact scope (architecture-level, tech-stack-level)
- Need to explain decision rationale to team/stakeholders

### Scenarios Where Doc2AHP Is NOT Suited

- Simple comparison between only 2 options → use a direct pros/cons analysis
- Single-dimension decision (e.g., pure cost optimization) → compare directly
- Urgent decisions → use intuition + rapid validation
- Already have a clear preference and just need confirmation → do a pros/cons check
