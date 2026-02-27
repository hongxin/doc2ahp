# Example: Web Application Tech Stack Selection

> Scenario: A startup team of 5 needs to choose a frontend framework for a new project. The team's primary experience is in React and Vue.

## Step 1: Decision Framework Construction

**Decision Goal**: Select the most suitable frontend framework for a new SaaS product

**Evaluation Hierarchy**:

```
Select the Best Frontend Framework
├── Technical Capability
│   ├── Performance (first paint, runtime)
│   ├── Ecosystem (component libraries, toolchain)
│   └── TypeScript Support
├── Team Efficiency
│   ├── Learning Curve
│   ├── Development Speed
│   └── Existing Skill Match
├── Long-term Maintainability
│   ├── Community Activity
│   ├── Large-scale Project Suitability
│   └── Backward Compatibility
└── Business Factors
    ├── Hiring Difficulty
    └── Enterprise Adoption Rate
```

**Alternatives**:
- **React** (v19+)
- **Vue** (v3+)
- **Svelte** (v5+)

## Step 2: Multi-Perspective Evaluation

### Perspective 1: Technical Expert

| vs | Technical Capability | Team Efficiency | Long-term Maintainability | Business Factors |
|----|---------------------|-----------------|--------------------------|-----------------|
| Technical Capability | 1 | 2 | 3 | 5 |
| Team Efficiency | 1/2 | 1 | 2 | 4 |
| Long-term Maintainability | 1/3 | 1/2 | 1 | 3 |
| Business Factors | 1/5 | 1/4 | 1/3 | 1 |

### Perspective 2: Team Lead

| vs | Technical Capability | Team Efficiency | Long-term Maintainability | Business Factors |
|----|---------------------|-----------------|--------------------------|-----------------|
| Technical Capability | 1 | 1/3 | 1 | 2 |
| Team Efficiency | 3 | 1 | 3 | 5 |
| Long-term Maintainability | 1 | 1/3 | 1 | 3 |
| Business Factors | 1/2 | 1/5 | 1/3 | 1 |

### Perspective 3: Product Manager

| vs | Technical Capability | Team Efficiency | Long-term Maintainability | Business Factors |
|----|---------------------|-----------------|--------------------------|-----------------|
| Technical Capability | 1 | 1/2 | 2 | 1 |
| Team Efficiency | 2 | 1 | 3 | 2 |
| Long-term Maintainability | 1/2 | 1/3 | 1 | 1/2 |
| Business Factors | 1 | 1/2 | 2 | 1 |

## Step 3: Consensus Aggregation

### Geometric Mean Matrix

| vs | Technical Capability | Team Efficiency | Long-term Maintainability | Business Factors |
|----|---------------------|-----------------|--------------------------|-----------------|
| Technical Capability | 1 | 0.87 | 1.82 | 2.15 |
| Team Efficiency | 1.14 | 1 | 2.62 | 3.42 |
| Long-term Maintainability | 0.55 | 0.38 | 1 | 1.65 |
| Business Factors | 0.47 | 0.29 | 0.61 | 1 |

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Technical Capability | 1.34 | 0.30 |
| Team Efficiency | 1.85 | 0.41 |
| Long-term Maintainability | 0.77 | 0.17 |
| Business Factors | 0.52 | 0.12 |

**Weight Distribution**:
```
Team Efficiency:          0.41 ████████████████████
Technical Capability:     0.30 ███████████████
Long-term Maintainability: 0.17 ████████
Business Factors:         0.12 ██████
```

## Step 4: Consistency Check

**Transitivity Verification**:
- Team Efficiency > Technical Capability > Long-term Maintainability > Business Factors ✓
- Team Efficiency > Long-term Maintainability ✓
- Technical Capability > Business Factors ✓
- All transitive relationships are consistent ✓

**Conclusion**: The comparison matrix passes the consistency check.

## Step 5: Alternative Scoring

| Sub-criterion | Weight | React | Vue | Svelte |
|---------------|--------|-------|-----|--------|
| Performance | 0.10 | 7 | 7 | 9 |
| Ecosystem | 0.12 | 9 | 8 | 6 |
| TypeScript Support | 0.08 | 9 | 8 | 8 |
| Learning Curve | 0.14 | 6 | 8 | 7 |
| Development Speed | 0.14 | 7 | 8 | 8 |
| Existing Skill Match | 0.13 | 8 | 8 | 4 |
| Community Activity | 0.07 | 9 | 8 | 7 |
| Large-scale Project Suitability | 0.06 | 9 | 7 | 6 |
| Backward Compatibility | 0.04 | 7 | 8 | 6 |
| Hiring Difficulty | 0.06 | 9 | 7 | 5 |
| Enterprise Adoption Rate | 0.06 | 9 | 7 | 4 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **React** | **7.72** |
| **Vue** | **7.58** |
| **Svelte** | **6.43** |

### Sensitivity Analysis

Adjusting "Existing Skill Match" weight from 0.13 to 0.05 (reducing team skill influence):
- React: 7.52 → Rank 1
- Vue: 7.38 → Rank 2
- Svelte: 6.75 → Rank 3 (improved but still third)

Rankings remain stable — the decision is robust.

## Step 6: Decision Report

# Decision Report: Frontend Framework Selection

## Recommendation
**React** — Overall Score: 7.72 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | React | 7.72 | Most complete ecosystem, strong team skill match, extensive enterprise validation |
| 2 | Vue | 7.58 | Gentle learning curve, fast development speed, newcomer-friendly |
| 3 | Svelte | 6.43 | Best performance, great DX, but lacks ecosystem maturity and team skill match |

## Key Trade-offs
- The gap between React and Vue is only 0.14 points; the core difference lies in **ecosystem** and **enterprise adoption rate**
- Svelte leads in performance but is constrained by **team skill match** and **ecosystem maturity**
- If the team is willing to invest in learning, Vue is a highly competitive alternative

## Risk Assessment
- React's API evolves rapidly (Hooks → Server Components), requiring continuous upskilling
- If the team's React experience is limited, initial development speed may lag behind Vue

## Recommendations
1. Choose React as the primary framework
2. Adopt Next.js as the meta-framework for best practices
3. Allocate 2 weeks of team training to ensure React best practices are established
