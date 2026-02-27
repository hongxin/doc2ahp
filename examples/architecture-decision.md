# Example: Microservices vs Monolith Architecture Decision

> **Key AHP Concept**: Leader Agent priority constraint — the user's stated priority ("development efficiency first") acts as a constraint that boosts a criterion's weight, demonstrating how AHP incorporates stakeholder values into the mathematical framework.

[中文](architecture-decision_ZH.md)

> Scenario: An e-commerce platform's daily order volume has grown from 1K to 50K. The existing Django monolith is experiencing performance bottlenecks, and the team is considering an architectural upgrade.

## Step 1: Decision Framework Construction

**Decision Goal**: Select the architecture approach best suited to the current business growth stage

**Evaluation Hierarchy**:

```
Select the Best Architecture Approach
├── Scalability
│   ├── Horizontal Scaling Capability
│   └── Independent Deployment Capability
├── Development Efficiency
│   ├── Development Complexity
│   ├── Team Collaboration Efficiency
│   └── Time to Ship
├── Reliability
│   ├── Fault Isolation
│   └── Data Consistency
└── Operational Cost
    ├── Infrastructure Cost
    ├── Monitoring Complexity
    └── Ops Staffing Requirements
```

**Alternatives**:
- **A. Full Microservices**: Decompose into independent services by domain
- **B. Modular Monolith**: Keep the monolith but enforce strict modularity; critical modules can be independently deployed
- **C. Progressive Decomposition**: Modularize first, then gradually extract bottleneck modules into independent services

**User Priority Constraint**: Development efficiency first (startup stage, need rapid iteration)

## Step 2: Multi-Perspective Evaluation

### Perspective 1: Technical Architect

| vs | Scalability | Dev Efficiency | Reliability | Operational Cost |
|----|-------------|---------------|-------------|-----------------|
| Scalability | 1 | 1/2 | 2 | 3 |
| Dev Efficiency | 2 | 1 | 2 | 3 |
| Reliability | 1/2 | 1/2 | 1 | 2 |
| Operational Cost | 1/3 | 1/3 | 1/2 | 1 |

### Perspective 2: Ops Engineer

| vs | Scalability | Dev Efficiency | Reliability | Operational Cost |
|----|-------------|---------------|-------------|-----------------|
| Scalability | 1 | 1/2 | 1 | 1/2 |
| Dev Efficiency | 2 | 1 | 2 | 1 |
| Reliability | 1 | 1/2 | 1 | 1 |
| Operational Cost | 2 | 1 | 1 | 1 |

### Perspective 3: CTO

| vs | Scalability | Dev Efficiency | Reliability | Operational Cost |
|----|-------------|---------------|-------------|-----------------|
| Scalability | 1 | 1/3 | 2 | 2 |
| Dev Efficiency | 3 | 1 | 3 | 4 |
| Reliability | 1/2 | 1/3 | 1 | 1 |
| Operational Cost | 1/2 | 1/4 | 1 | 1 |

## Step 3: Consensus Aggregation

### Geometric Mean Matrix

| vs | Scalability | Dev Efficiency | Reliability | Operational Cost |
|----|-------------|---------------|-------------|-----------------|
| Scalability | 1 | 0.44 | 1.59 | 1.44 |
| Dev Efficiency | 2.29 | 1 | 2.29 | 2.29 |
| Reliability | 0.63 | 0.44 | 1 | 1.26 |
| Operational Cost | 0.69 | 0.44 | 0.79 | 1 |

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Scalability | 1.04 | 0.28 |
| Dev Efficiency | 1.87 | 0.38 × (constraint applied) |
| Reliability | 0.74 | 0.20 |
| Operational Cost | 0.65 | 0.14 |

**Weight Distribution** (with "development efficiency first" constraint applied, boosting by 1 scale level):

```
Development Efficiency: 0.38 ███████████████████
Scalability:            0.28 ██████████████
Reliability:            0.20 ██████████
Operational Cost:       0.14 ███████
```

## Step 4: Consistency Check

- Development Efficiency > Scalability > Reliability > Operational Cost ✓
- Development Efficiency > Reliability ✓ (transitivity satisfied)
- Scalability > Operational Cost ✓ (transitivity satisfied)
- Passes consistency check ✓

## Step 5: Alternative Scoring

| Sub-criterion | Weight | Full Microservices | Modular Monolith | Progressive Decomposition |
|---------------|--------|--------------------|------------------|--------------------------|
| Horizontal Scaling | 0.16 | 9 | 5 | 7 |
| Independent Deployment | 0.12 | 9 | 4 | 6 |
| Development Complexity | 0.14 | 4 | 8 | 7 |
| Team Collaboration | 0.12 | 7 | 6 | 7 |
| Time to Ship | 0.12 | 4 | 9 | 7 |
| Fault Isolation | 0.12 | 9 | 4 | 6 |
| Data Consistency | 0.08 | 5 | 9 | 7 |
| Infrastructure Cost | 0.05 | 4 | 8 | 6 |
| Monitoring Complexity | 0.05 | 3 | 8 | 6 |
| Ops Staffing | 0.04 | 3 | 8 | 6 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **Progressive Decomposition** | **6.62** |
| **Modular Monolith** | **6.52** |
| **Full Microservices** | **6.35** |

### Sensitivity Analysis

Increasing "Scalability" weight from 0.28 to 0.40 (assuming faster-than-expected business growth):
- Full Microservices: 6.62 → Rank 1
- Progressive Decomposition: 6.70 → Rank 1 (still leads)
- Modular Monolith: 5.98 → Rank 3

Progressive Decomposition maintains its lead in both scenarios — the conclusion is robust.

## Step 6: Decision Report

# Decision Report: Architecture Approach Selection

## Recommendation
**Progressive Decomposition** — Overall Score: 6.62 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | Progressive Decomposition | 6.62 | Balances short-term efficiency with long-term scalability, lowest risk |
| 2 | Modular Monolith | 6.52 | Fastest development, but clear scalability ceiling |
| 3 | Full Microservices | 6.35 | Strongest scalability, but excessive complexity at current stage |

## Key Trade-offs
- Full Microservices leads in scalability and fault isolation, but development complexity and operational costs are too high
- Modular Monolith offers the highest short-term efficiency, but may hit bottlenecks again when orders exceed 100K
- Progressive Decomposition combines the advantages of both, but requires the team to have clear module boundary design skills

## Risk Assessment
- Progressive Decomposition demands discipline: if module boundaries are poorly designed, subsequent decomposition costs will increase dramatically
- Need to identify modules most likely to become bottlenecks (order processing, inventory management) as first decomposition candidates

## Recommendations
1. Phase 1 (Months 1-2): Strictly modularize the existing Django monolith with clear module boundaries
2. Phase 2 (Months 3-4): Extract the order processing module as an independent service
3. Phase 3 (As needed): Progressively decompose other modules based on actual bottlenecks
4. Supporting infrastructure: Introduce API Gateway, service discovery, and distributed tracing
