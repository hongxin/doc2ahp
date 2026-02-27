# Doc2AHP Paper: Key Points Summary

> Paper: "Doc2AHP: Inferring Structured Multi-Criteria Decision Models via Semantic Trees with LLMs"
> Authors: Hongjia Wu, Shuai Zhou, Hongxin Zhang, Wei Chen
> arXiv: [2601.16479](https://arxiv.org/abs/2601.16479)

## Core Problem

Traditional AHP (Analytic Hierarchy Process) relies on domain experts to manually construct decision hierarchies and pairwise comparison matrices — a process that is costly, time-consuming, and difficult to scale. Doc2AHP proposes using LLMs to automate this process.

## Key Innovations

### 1. Semantic Tree Construction

Transforms unstructured documents into hierarchical decision structures:

```
Goal
├── Main Criterion C1
│   ├── Sub-criterion C1.1
│   └── Sub-criterion C1.2
├── Main Criterion C2
│   ├── Sub-criterion C2.1
│   └── Sub-criterion C2.2
└── Main Criterion C3
    └── Sub-criterion C3.1
```

**Method**: Document embedding → Hierarchical clustering → Recursive AHP hierarchy construction

**Constraint Parameters**:
- `K_max`: Maximum branches per level (cognitive load upper bound)
- `D_max`: Maximum hierarchy depth
- `τ` (tau): Relevance threshold for filtering irrelevant criteria

### 2. Multi-Agent Weighting Mechanism

- **K Expert Agents**: Each independently performs pairwise comparisons of criteria
- **Weighted Geometric Mean Aggregation**: Merges judgment matrices from multiple experts
- **Leader Agent**: Applies strategic priority constraints to ensure decision alignment

### 3. AHP Mathematical Foundation

#### Saaty Scale (1-9)

| Scale | Meaning |
|-------|---------|
| 1 | Equal importance |
| 3 | Slightly more important |
| 5 | Clearly more important |
| 7 | Strongly more important |
| 9 | Extremely more important |
| 2,4,6,8 | Intermediate values |

#### Pairwise Comparison Matrix

For n criteria, construct an n×n matrix A, where a_ij represents the importance of criterion i relative to criterion j:
- a_ij = 1/a_ji (reciprocity)
- a_ii = 1 (diagonal is 1)

#### Weight Calculation: LLSM (Logarithmic Least Squares Method)

Compared to the eigenvalue method, LLSM is better suited for LLM-generated comparison matrices:

```
w_i = (∏_{j=1}^{n} a_ij)^{1/n} / Σ_{k=1}^{n} (∏_{j=1}^{n} a_kj)^{1/n}
```

In other words: the geometric mean of each row's elements, normalized to produce weights.

#### Consistency Verification

- **Consistency Index CI** = (λ_max - n) / (n - 1)
- **Consistency Ratio CR** = CI / RI
- **Acceptance threshold**: CR < 0.1

| n | RI |
|---|-----|
| 3 | 0.58 |
| 4 | 0.90 |
| 5 | 1.12 |
| 6 | 1.24 |
| 7 | 1.32 |

### 4. Adaptive Consistency Optimization

When CR ≥ 0.1:
1. Locate the most inconsistent element
2. Adjust it to better satisfy transitivity (if A > B and B > C, then A > C)
3. Recompute until CR < 0.1

### 5. Decision Reasoning & Utility Computation

Final Score = Σ (Criterion Weight × Alternative's Score on that Criterion)

## Paper Pipeline Flow

```
Input Document
  → Text Chunking & Embedding
    → Hierarchical Clustering
      → Semantic Tree Construction (Criteria Extraction)
        → Multi-Agent Pairwise Comparisons
          → LLSM Weight Calculation
            → Consistency Verification & Optimization
              → Alternative Scoring
                → Decision Report
```

## Core Insights

1. **LLM serves as both information extractor and decision evaluator** — A single model accomplishes work that traditionally requires multiple experts
2. **Structured constraints eliminate hallucination** — AHP's mathematical framework (reciprocity, consistency checks) constrains the LLM to produce logically consistent judgments
3. **Multi-Agent mechanism increases robustness** — Multi-perspective evaluation reduces single-viewpoint bias
4. **Cognitive constraints align with human understanding** — K_max ≤ 7 corresponds to Miller's Law (7±2), ensuring results remain interpretable
