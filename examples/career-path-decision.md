# Example: Senior Developer Career Path Decision

[中文](career-path-decision_ZH.md)

> Scenario: A 32-year-old senior backend developer with 8 years of experience at a major tech company. Solid savings (2 years of runway), no mortgage pressure. Technically strong but feeling plateaued — passed over for Staff promotion twice. Has a side project with 2K GitHub stars and a growing newsletter (5K subscribers). Three paths diverge ahead.

## Step 1: Decision Framework Construction

**Decision Goal**: Choose the career path that maximizes long-term fulfillment and growth for a senior developer at a crossroads

**Evaluation Hierarchy**:

```
Choose the Best Career Path
├── Financial Outcomes
│   ├── Income Stability
│   ├── Upside Potential (equity, passive income)
│   └── Financial Risk Level
├── Personal Growth
│   ├── Technical Depth
│   ├── Breadth of Skills (business, leadership, communication)
│   └── Speed of Learning
├── Lifestyle Quality
│   ├── Work-Life Balance
│   ├── Autonomy & Freedom
│   └── Geographic Flexibility
└── Career Impact
    ├── Industry Influence & Reputation
    ├── Network Expansion
    └── Long-term Optionality (doors opened)
```

**Alternatives**:
- **A. Stay at Big Tech**: Push for Staff Engineer again, leverage internal mobility
- **B. Join Early-stage Startup**: CTO/co-founder role at a Series A startup in the AI space
- **C. Go Independent**: Freelance consulting + open source + info products (courses, newsletter)

**User Priority Constraint**: Personal growth matters most — "I'd rather earn less and grow faster than stay comfortable and stagnate."

## Step 2: Multi-Perspective Evaluation

### Perspective 1: The Pragmatist (Inner Voice of Security)

| vs | Financial Outcomes | Personal Growth | Lifestyle Quality | Career Impact |
|----|-------------------|----------------|------------------|---------------|
| Financial Outcomes | 1 | 2 | 3 | 3 |
| Personal Growth | 1/2 | 1 | 2 | 2 |
| Lifestyle Quality | 1/3 | 1/2 | 1 | 1 |
| Career Impact | 1/3 | 1/2 | 1 | 1 |

### Perspective 2: The Ambitious Self (Inner Voice of Growth)

| vs | Financial Outcomes | Personal Growth | Lifestyle Quality | Career Impact |
|----|-------------------|----------------|------------------|---------------|
| Financial Outcomes | 1 | 1/3 | 1 | 1/2 |
| Personal Growth | 3 | 1 | 3 | 2 |
| Lifestyle Quality | 1 | 1/3 | 1 | 1/2 |
| Career Impact | 2 | 1/2 | 2 | 1 |

### Perspective 3: The Mentor (Experienced Senior Who's Been There)

| vs | Financial Outcomes | Personal Growth | Lifestyle Quality | Career Impact |
|----|-------------------|----------------|------------------|---------------|
| Financial Outcomes | 1 | 1/2 | 1 | 1/3 |
| Personal Growth | 2 | 1 | 2 | 1 |
| Lifestyle Quality | 1 | 1/2 | 1 | 1/2 |
| Career Impact | 3 | 1 | 2 | 1 |

### Perspective 4: The Life Partner (Significant Other's Perspective)

| vs | Financial Outcomes | Personal Growth | Lifestyle Quality | Career Impact |
|----|-------------------|----------------|------------------|---------------|
| Financial Outcomes | 1 | 1 | 1/2 | 2 |
| Personal Growth | 1 | 1 | 1/2 | 2 |
| Lifestyle Quality | 2 | 2 | 1 | 3 |
| Career Impact | 1/2 | 1/2 | 1/3 | 1 |

## Step 3: Consensus Aggregation

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Financial Outcomes | 0.87 | 0.20 |
| Personal Growth | 1.41 | 0.33 |
| Lifestyle Quality | 0.96 | 0.22 |
| Career Impact | 1.04 | 0.25 |

**Weight Distribution** (with "personal growth first" constraint applied, boosting by 1 level):
```
Personal Growth:    0.33 ████████████████
Career Impact:      0.25 ████████████
Lifestyle Quality:  0.22 ███████████
Financial Outcomes: 0.20 ██████████
```

## Step 4: Consistency Check

**Transitivity Verification**:
- Personal Growth > Career Impact > Lifestyle Quality > Financial Outcomes ✓
- Personal Growth > Lifestyle Quality ✓
- Career Impact > Financial Outcomes ✓
- All transitive relationships are consistent ✓

**Interesting Note**: Financial Outcomes ranks last — this is consistent with the user's stated priority ("I'd rather earn less and grow faster"). The model correctly captured this constraint.

## Step 5: Alternative Scoring

| Sub-criterion | Weight | Big Tech | Startup CTO | Independent |
|---------------|--------|----------|-------------|-------------|
| Income Stability | 0.08 | 10 | 5 | 4 |
| Upside Potential | 0.07 | 4 | 9 | 7 |
| Financial Risk | 0.05 | 9 | 4 | 5 |
| Technical Depth | 0.12 | 7 | 8 | 6 |
| Breadth of Skills | 0.11 | 4 | 9 | 9 |
| Speed of Learning | 0.10 | 4 | 9 | 8 |
| Work-Life Balance | 0.08 | 7 | 3 | 8 |
| Autonomy & Freedom | 0.07 | 3 | 6 | 10 |
| Geographic Flexibility | 0.07 | 5 | 4 | 10 |
| Industry Influence | 0.09 | 5 | 7 | 8 |
| Network Expansion | 0.08 | 6 | 9 | 7 |
| Long-term Optionality | 0.08 | 5 | 8 | 9 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **Startup CTO** | **6.98** |
| **Independent** | **7.38** |
| **Big Tech** | **5.52** |

### Sensitivity Analysis

Scenario A — Financial Outcomes weight increased to 0.35 (e.g., planning to buy a house):
- Big Tech: 6.52 → **Rank 1**
- Startup CTO: 6.60 → Rank 1 (near tie)
- Independent: 6.48 → Rank 3

Scenario B — Career Impact weight increased to 0.40 (reputation-driven):
- Independent: 7.65 → **Rank 1** (gap widens)
- Startup CTO: 7.12 → Rank 2
- Big Tech: 5.25 → Rank 3

**Key Finding**: Going Independent is surprisingly robust — it only loses when financial stability becomes the dominant concern. The Startup path has high variance: incredible growth but at the cost of lifestyle.

## Step 6: Decision Report

# Decision Report: Career Path Selection

## Recommendation
**Go Independent** — Overall Score: 7.38 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | Go Independent | 7.38 | Maximum autonomy, broadest skill growth, best long-term optionality |
| 2 | Startup CTO | 6.98 | Fastest growth in leadership & breadth, strongest network expansion, highest financial upside |
| 3 | Stay at Big Tech | 5.52 | Most stable income, lowest risk, but limited growth at current plateau |

## Key Trade-offs
- **Independent vs Startup CTO (the 0.40-point gap)**: Both score high on growth, but Independent wins on lifestyle and optionality. The Startup path offers faster, more intense growth but demands 60-70 hour weeks and carries real financial risk
- **The Big Tech trap**: High income stability scores (10/10) cannot compensate for consistently low growth and autonomy scores. Staying is the "safe" choice, but for someone already plateaued, it may be the riskiest long-term decision
- **The hidden advantage of Independent**: It's the only path that's fully reversible. You can always go back to Big Tech or join a startup later. The reverse isn't true

## Risk Assessment
- Going Independent requires strong self-discipline; without external structure, productivity may drop initially
- Income will be volatile for the first 12-18 months; the 2-year savings runway provides adequate buffer
- The existing side project (2K stars) and newsletter (5K subs) provide a meaningful head start — this isn't starting from zero
- Risk of isolation; deliberately schedule co-working, conferences, and community engagement

## Recommendations
1. Give notice and transition over 1-2 months; leave on good terms for potential boomerang option
2. Month 1-3: Establish freelance consulting pipeline using existing network (target: 3 retainer clients)
3. Month 1-6: Grow the open source project and newsletter as the long-term leverage play
4. Month 6+: Launch first info product (course or book) based on newsletter audience feedback
5. Set a 12-month checkpoint: if monthly income hasn't reached 60% of previous salary, reassess
6. Join an indie hackers community or mastermind group for accountability and support
