# Example: Database Selection for Social App at Scale

[中文](database-selection_ZH.md)

> Scenario: A startup is building a social media platform (a niche community app combining short-form content + real-time messaging + recommendations). The MVP has 50K users on a single PostgreSQL instance. Series A just closed — the target is 10M users within 18 months. The 12-person engineering team needs to choose the primary database to scale into. The CEO's mandate: "Never let the feed feel slow."

## Step 1: Decision Framework Construction

**Decision Goal**: Select the most suitable primary database for a social app scaling from 50K to 10M users

**Evaluation Hierarchy**:

```
Select the Best Database for Social App
├── Data Model Fit
│   ├── Schema Flexibility (evolving features)
│   ├── Relationship Queries (social graph, followers, likes)
│   └── Full-text Search Capability
├── Scalability
│   ├── Horizontal Write Scaling
│   ├── Read Performance (feed generation, timeline)
│   └── Data Volume Handling (projected 50TB+ in 2 years)
├── Operational Excellence
│   ├── Backup & Disaster Recovery
│   ├── Monitoring & Debugging Tooling
│   └── Managed Service Quality (cloud offerings)
└── Team & Cost
    ├── Learning Curve (team knows PostgreSQL)
    ├── Community & Documentation
    └── Infrastructure Cost at Scale
```

**Alternatives**:
- **PostgreSQL + Citus** (horizontal sharding extension for PostgreSQL)
- **MongoDB** (document store with native sharding)
- **TiDB** (MySQL-compatible distributed NewSQL)

## Step 2: Multi-Perspective Evaluation

### Perspective 1: Backend Architect

| vs | Data Model Fit | Scalability | Operational Excellence | Team & Cost |
|----|---------------|-------------|----------------------|-------------|
| Data Model Fit | 1 | 1/2 | 2 | 2 |
| Scalability | 2 | 1 | 3 | 4 |
| Operational Excellence | 1/2 | 1/3 | 1 | 2 |
| Team & Cost | 1/2 | 1/4 | 1/2 | 1 |

### Perspective 2: SRE / Ops Lead

| vs | Data Model Fit | Scalability | Operational Excellence | Team & Cost |
|----|---------------|-------------|----------------------|-------------|
| Data Model Fit | 1 | 1/2 | 1/3 | 1 |
| Scalability | 2 | 1 | 1 | 2 |
| Operational Excellence | 3 | 1 | 1 | 3 |
| Team & Cost | 1 | 1/2 | 1/3 | 1 |

### Perspective 3: Product Engineer

| vs | Data Model Fit | Scalability | Operational Excellence | Team & Cost |
|----|---------------|-------------|----------------------|-------------|
| Data Model Fit | 1 | 2 | 2 | 1 |
| Scalability | 1/2 | 1 | 1 | 1/2 |
| Operational Excellence | 1/2 | 1 | 1 | 1 |
| Team & Cost | 1 | 2 | 1 | 1 |

## Step 3: Consensus Aggregation

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Data Model Fit | 0.93 | 0.22 |
| Scalability | 1.26 | 0.32 |
| Operational Excellence | 1.10 | 0.27 |
| Team & Cost | 0.78 | 0.19 |

**Weight Distribution**:
```
Scalability:              0.32 ████████████████
Operational Excellence:   0.27 █████████████
Data Model Fit:           0.22 ███████████
Team & Cost:              0.19 █████████
```

## Step 4: Consistency Check

**Transitivity Verification**:
- Scalability > Operational Excellence > Data Model Fit > Team & Cost ✓
- Scalability > Data Model Fit ✓
- Operational Excellence > Team & Cost ✓
- All transitive relationships are consistent ✓

## Step 5: Alternative Scoring

| Sub-criterion | Weight | PostgreSQL + Citus | MongoDB | TiDB |
|---------------|--------|-------------------|---------|------|
| Schema Flexibility | 0.08 | 6 | 9 | 7 |
| Relationship Queries | 0.08 | 9 | 5 | 8 |
| Full-text Search | 0.06 | 7 | 7 | 5 |
| Horizontal Write Scaling | 0.12 | 7 | 8 | 9 |
| Read Performance | 0.11 | 8 | 7 | 8 |
| Data Volume Handling | 0.09 | 7 | 8 | 9 |
| Backup & Recovery | 0.10 | 9 | 7 | 7 |
| Monitoring & Debugging | 0.09 | 9 | 7 | 7 |
| Managed Service Quality | 0.08 | 8 | 9 | 6 |
| Learning Curve | 0.07 | 9 | 6 | 8 |
| Community & Docs | 0.06 | 9 | 8 | 6 |
| Infra Cost at Scale | 0.06 | 7 | 6 | 5 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **PostgreSQL + Citus** | **7.75** |
| **MongoDB** | **7.16** |
| **TiDB** | **7.26** |

### Sensitivity Analysis

Scenario A — Increasing "Scalability" weight from 0.32 to 0.50 (hyper-growth scenario):
- TiDB: 7.58 → **Rank 1**
- PostgreSQL + Citus: 7.42 → Rank 2
- MongoDB: 7.20 → Rank 3

Scenario B — Increasing "Team & Cost" weight from 0.19 to 0.35 (budget-constrained):
- PostgreSQL + Citus: 8.05 → **Rank 1** (gap widens)
- MongoDB: 6.98 → Rank 3
- TiDB: 7.02 → Rank 2

**Key Finding**: PostgreSQL + Citus is the most robust choice across scenarios. TiDB only overtakes under extreme scalability pressure (50x growth). The team's existing PostgreSQL expertise is a significant, tangible advantage.

## Step 6: Decision Report

# Decision Report: Database Selection for Social App

## Recommendation
**PostgreSQL + Citus** — Overall Score: 7.75 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | PostgreSQL + Citus | 7.75 | Leverages team expertise, best relational queries for social graph, mature operational tooling |
| 2 | TiDB | 7.26 | Best horizontal scaling, MySQL compatibility, strong for write-heavy workloads |
| 3 | MongoDB | 7.16 | Maximum schema flexibility, easiest to start with, excellent managed service (Atlas) |

## Key Trade-offs
- **PostgreSQL + Citus vs TiDB**: PostgreSQL wins on operational maturity and team familiarity; TiDB wins on automatic horizontal scaling. The 0.49-point gap narrows significantly in hyper-growth scenarios
- **The social graph factor**: Relationship-heavy queries (followers, mutual friends, like counts) are where PostgreSQL's relational model shines. MongoDB's document model makes these queries awkward and expensive at scale
- **MongoDB's schema flexibility advantage** is real for rapidly iterating features, but the trade-off is weaker JOIN performance for the social graph, which is the app's core data structure
- **TiDB's hidden cost**: While TiDB scales beautifully, the operational expertise required for a distributed NewSQL system is significant, and the managed service options are less mature than PostgreSQL or MongoDB

## Risk Assessment
- Citus sharding requires careful shard key design upfront; a bad distribution key leads to hotspots and expensive re-sharding later
- PostgreSQL full-text search is adequate but not best-in-class; plan to add Elasticsearch/Meilisearch when search becomes a core feature
- At 10M+ users, even Citus may need to be complemented with a caching layer (Redis) and a dedicated feed service

## Recommendations
1. Migrate from single PostgreSQL to PostgreSQL + Citus, sharding by user_id
2. Add Redis as a caching layer for hot data (timelines, session data, counters)
3. Implement read replicas for analytics and recommendation queries
4. Plan for a dedicated search service (Meilisearch or Elasticsearch) at the 1M user milestone
5. Monitor query latency distribution weekly; set alerting at P95 > 100ms
6. Re-evaluate TiDB at 10M users if write scaling becomes the primary bottleneck
