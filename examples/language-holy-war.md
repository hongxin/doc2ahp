# Example: Programming Language Selection for High-Concurrency Trading System

> **Key AHP Concept**: Leader Agent priority constraint & sensitivity analysis — a user-stated priority ("latency predictability is paramount") reshapes the weight distribution, and sensitivity analysis reveals the exact tipping point where the ranking flips.

[中文](language-holy-war_ZH.md)

> Scenario: A fintech startup is building a real-time trading engine. Their Python prototype handles 100 TPS, but they need to scale to 10,000+ TPS with sub-millisecond P99 latency. The 6-person team has diverse backgrounds (2 Python, 2 Java, 1 Go, 1 C++). Budget for rewrite: 4 months.

## Step 1: Decision Framework Construction

**Decision Goal**: Select the best programming language for rewriting a high-frequency trading engine with extreme latency and throughput requirements

**Evaluation Hierarchy**:

```
Select the Best Language for Trading Engine
├── Performance
│   ├── Raw Throughput (TPS ceiling)
│   ├── Latency Predictability (GC pauses, tail latency)
│   └── Memory Efficiency
├── Development Velocity
│   ├── Learning Curve (time for team to be productive)
│   ├── Time to MVP
│   └── Developer Tooling (IDE, debugger, profiler)
├── Ecosystem Fit
│   ├── Financial/Trading Libraries
│   ├── Concurrency Primitives
│   └── Network Stack Maturity
└── Talent & Long-term
    ├── Hiring Pool Size
    ├── Code Maintainability at Scale
    └── Community Momentum
```

**Alternatives**:
- **Rust** (with Tokio async runtime)
- **Go** (with goroutines + channels)
- **Java** (with Virtual Threads / Loom + Vert.x)

**User Priority Constraint**: Latency predictability is paramount — one GC pause during market peak can mean six-figure losses.

## Step 2: Multi-Perspective Evaluation

### Perspective 1: Systems Architect

| vs | Performance | Dev Velocity | Ecosystem Fit | Talent & Long-term |
|----|-------------|-------------|---------------|-------------------|
| Performance | 1 | 5 | 3 | 5 |
| Dev Velocity | 1/5 | 1 | 1/2 | 1 |
| Ecosystem Fit | 1/3 | 2 | 1 | 2 |
| Talent & Long-term | 1/5 | 1 | 1/2 | 1 |

### Perspective 2: Engineering Manager

| vs | Performance | Dev Velocity | Ecosystem Fit | Talent & Long-term |
|----|-------------|-------------|---------------|-------------------|
| Performance | 1 | 1 | 2 | 1 |
| Dev Velocity | 1 | 1 | 2 | 2 |
| Ecosystem Fit | 1/2 | 1/2 | 1 | 1 |
| Talent & Long-term | 1 | 1/2 | 1 | 1 |

### Perspective 3: Quant Developer

| vs | Performance | Dev Velocity | Ecosystem Fit | Talent & Long-term |
|----|-------------|-------------|---------------|-------------------|
| Performance | 1 | 3 | 2 | 7 |
| Dev Velocity | 1/3 | 1 | 1 | 3 |
| Ecosystem Fit | 1/2 | 1 | 1 | 3 |
| Talent & Long-term | 1/7 | 1/3 | 1/3 | 1 |

## Step 3: Consensus Aggregation

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Performance | 1.82 | 0.42 |
| Dev Velocity | 0.93 | 0.22 |
| Ecosystem Fit | 1.01 | 0.23 |
| Talent & Long-term | 0.56 | 0.13 |

**Weight Distribution** (with latency priority constraint applied):
```
Performance:       0.42 █████████████████████
Ecosystem Fit:     0.23 ███████████
Dev Velocity:      0.22 ███████████
Talent & Long-term: 0.13 ██████
```

## Step 4: Consistency Check

**Transitivity Verification**:
- Performance > Ecosystem Fit > Dev Velocity > Talent & Long-term ✓
- Performance > Dev Velocity ✓
- Performance > Talent & Long-term ✓
- Ecosystem Fit ≈ Dev Velocity (0.23 vs 0.22, within tolerance) ✓
- Passes consistency check ✓

## Step 5: Alternative Scoring

| Sub-criterion | Weight | Rust | Go | Java |
|---------------|--------|------|-----|------|
| Raw Throughput | 0.15 | 10 | 8 | 8 |
| Latency Predictability | 0.17 | 10 | 7 | 5 |
| Memory Efficiency | 0.10 | 10 | 7 | 6 |
| Learning Curve | 0.08 | 4 | 9 | 7 |
| Time to MVP | 0.07 | 5 | 9 | 7 |
| Developer Tooling | 0.07 | 7 | 7 | 9 |
| Financial Libraries | 0.09 | 5 | 6 | 9 |
| Concurrency Primitives | 0.08 | 9 | 9 | 8 |
| Network Stack | 0.06 | 8 | 8 | 9 |
| Hiring Pool | 0.05 | 4 | 7 | 9 |
| Code Maintainability | 0.04 | 9 | 7 | 7 |
| Community Momentum | 0.04 | 9 | 8 | 6 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **Rust** | **7.93** |
| **Go** | **7.62** |
| **Java** | **7.29** |

### Sensitivity Analysis

Scenario A — Reducing "Performance" weight from 0.42 to 0.25 (relaxed latency requirements):
- Go: 7.68 → **Rank 1**
- Rust: 7.15 → Rank 2
- Java: 7.42 → Rank 2

Scenario B — Increasing "Dev Velocity" weight from 0.22 to 0.35 (tighter deadline):
- Go: 7.85 → **Rank 1**
- Rust: 7.05 → Rank 3
- Java: 7.25 → Rank 2

**Key Finding**: Rust wins only when performance is the dominant concern. Go takes the lead in any scenario where development speed matters more. This is the critical trade-off.

## Step 6: Decision Report

# Decision Report: Trading Engine Language Selection

## Recommendation
**Rust** — Overall Score: 7.93 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | Rust | 7.93 | Zero-cost abstractions, no GC pauses, deterministic latency, best memory safety |
| 2 | Go | 7.62 | Fastest development speed, excellent concurrency model, easiest to hire for |
| 3 | Java | 7.29 | Richest financial ecosystem, mature tooling, but GC pauses are a real concern |

## Key Trade-offs
- **Rust vs Go (the critical 0.31-point gap)**: Rust guarantees zero GC pauses — crucial for trading. But Go's development velocity advantage means the team ships 40-60% faster. If latency tolerance is >5ms P99, Go is the better choice
- **Java's GC problem**: Even with ZGC/Shenandoah, Java cannot guarantee sub-millisecond P99 under sustained load. The financial library ecosystem is unmatched, but the latency tax is real
- **The Rust learning curve**: Expect 6-8 weeks before the team is productive. The borrow checker will cause frustration, but it catches concurrency bugs at compile time that would be production incidents in Go/Java

## Risk Assessment
- Rust's steep learning curve may push the 4-month timeline to 5-6 months
- Limited financial domain libraries in Rust mean more custom code
- If Rust hiring proves difficult, consider a hybrid: Rust for the hot path (matching engine), Go for everything else (order management, risk, API gateway)

## Recommendations
1. Adopt Rust for the core matching engine and order book
2. Use Go for peripheral services (API gateway, risk management, monitoring)
3. Invest 3 weeks in team Rust bootcamp before starting the rewrite
4. Establish coding conventions early — Rust's flexibility can lead to inconsistent codebases
5. Set up continuous benchmarking (criterion.rs) from day one to catch performance regressions
