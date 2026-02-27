# JavaScript Runtime Selection: Node.js vs Deno vs Bun

## Full Doc2AHP Analysis with Real Data

[中文](analysis_ZH.md)

> **Scenario**: A 15-person backend team at a mid-stage startup (Series B) is building a new real-time API service for their product. The existing stack is Node.js + Express + TypeScript. The team lead wants to evaluate whether to continue with Node.js or adopt a newer runtime for this greenfield service. Expected load: 50K concurrent connections, JSON-heavy API, deployed on AWS ECS.

---

## Step 0: Decision Input Mode Selection

**Mode Selected**: A — Document-Grounded Analysis

Five real data sources were gathered on 2026-02-27:

| ID | Source | Type | URL |
|----|--------|------|-----|
| D1 | RepoFlow Benchmarks | Performance benchmark (2026) | [repoflow.io](https://www.repoflow.io/blog/node-js-vs-deno-vs-bun-performance-benchmarks) |
| D2 | BetterStack + Snyk Comparison | Performance & features | [betterstack.com](https://betterstack.com/community/guides/scaling-nodejs/nodejs-vs-deno-vs-bun/) / [snyk.io](https://snyk.io/blog/javascript-runtime-compare-node-deno-bun/) |
| D3 | GitHub API Statistics | Live repository data | GitHub API, fetched 2026-02-27 |
| D4 | Ecosystem & Compatibility Articles | Ecosystem analysis | [dev.to](https://dev.to/pockit_tools/deno-2-vs-nodejs-vs-bun-in-2026-the-complete-javascript-runtime-comparison-1elm) / [pullflow.com](https://pullflow.com/blog/deno-vs-bun-2025/) |
| D5 | State of JavaScript 2024 Survey | Developer survey data | [2024.stateofjs.com](https://2024.stateofjs.com/en-US) |

All source documents are available in the [sources/](sources/) directory.

### Criteria Extraction from Documents

| Extracted Criterion | Source(s) | Evidence |
|--------------------|-----------|----------|
| HTTP throughput | D1, D2 | Bun 146K req/s vs Node 29K vs Deno 32K [D1]; Express: Bun 52K vs Node 13K vs Deno 22K [D2] |
| JSON parsing speed | D1 | Bun 3.4M ops/s vs Node 1.66M vs Deno 1.71M for 1KB JSON [D1] |
| Startup time | D2 | Bun ~5ms vs Node ~25ms [D2] |
| npm compatibility | D4 | Node 100%, Bun ~95%, Deno ~90% [D4] |
| Package install speed | D4 | bun install 47s vs npm 28min vs pnpm 4min [D4] |
| TypeScript support | D4 | Deno & Bun native; Node via --strip-types [D4] |
| Security model | D4 | Deno sandboxed by default; Node & Bun unrestricted [D4] |
| Community size | D3, D5 | Node 475K SO questions vs Deno 1.1K vs Bun 264 [D2]; Node 94% usage [D5] |
| GitHub stars/activity | D3 | Node 115K★, Deno 106K★, Bun 87K★ [D3] |
| Production adoption | D5 | Node: Netflix/PayPal/LinkedIn; Deno: Slack/Netlify; Bun: early startups [D5] |
| Enterprise governance | D4 | Node: OpenJS Foundation; Deno/Bun: VC-backed [D4] |
| Built-in tooling | D4 | Deno: test+lint+fmt; Bun: test+build+install; Node: minimal [D4] |

**τ filter applied**:
- ~~"Linter/formatter quality"~~ — outside scope of runtime selection for API service → Filtered
- ~~"WebAssembly support"~~ — not a requirement for this project → Filtered

**12 criteria extracted → 10 retained after filter**

---

## Step 1: Decision Framework Construction

**Decision Goal**: Select the best JavaScript runtime for a high-throughput real-time API service on a greenfield project

**Evaluation Hierarchy** (organized from extracted criteria):

```
Select the Best JS Runtime for Real-time API Service
├── Performance [D1, D2]
│   ├── HTTP Throughput (req/sec under load)
│   ├── JSON Processing Speed (parse + stringify)
│   └── Startup Time & Memory Efficiency
├── Ecosystem & Compatibility [D3, D4]
│   ├── npm Package Compatibility
│   ├── Community Size & Support Resources
│   └── Production Track Record
├── Developer Experience [D4]
│   ├── TypeScript Support Quality
│   ├── Built-in Tooling (test, build, install)
│   └── Package Management Speed
└── Stability & Governance [D3, D4, D5]
    ├── Project Maturity & Governance
    └── Enterprise Adoption & Cloud Support
```

**Alternatives**:
- **Node.js** (v22+ LTS)
- **Deno** (v2.6+)
- **Bun** (v1.3+)

---

## Step 2: Multi-Perspective Evaluation

### Perspective 1: Performance Engineer

*Focus: throughput, latency, resource efficiency*

| vs | Performance | Ecosystem | DevEx | Stability |
|----|-------------|-----------|-------|-----------|
| Performance | 1 | 3 | 5 | 5 |
| Ecosystem | 1/3 | 1 | 2 | 2 |
| DevEx | 1/5 | 1/2 | 1 | 1 |
| Stability | 1/5 | 1/2 | 1 | 1 |

### Perspective 2: Tech Lead

*Focus: team productivity, maintainability, hiring*

| vs | Performance | Ecosystem | DevEx | Stability |
|----|-------------|-----------|-------|-----------|
| Performance | 1 | 1/2 | 1/2 | 1/3 |
| Ecosystem | 2 | 1 | 1 | 1 |
| DevEx | 2 | 1 | 1 | 1 |
| Stability | 3 | 1 | 1 | 1 |

### Perspective 3: CTO

*Focus: risk, long-term viability, enterprise alignment*

| vs | Performance | Ecosystem | DevEx | Stability |
|----|-------------|-----------|-------|-----------|
| Performance | 1 | 1/2 | 1 | 1/3 |
| Ecosystem | 2 | 1 | 2 | 1 |
| DevEx | 1 | 1/2 | 1 | 1/2 |
| Stability | 3 | 1 | 2 | 1 |

### Perspective 4: DevOps Engineer

*Focus: deployment, cloud support, operational maturity*

| vs | Performance | Ecosystem | DevEx | Stability |
|----|-------------|-----------|-------|-----------|
| Performance | 1 | 1 | 2 | 1/2 |
| Ecosystem | 1 | 1 | 2 | 1/2 |
| DevEx | 1/2 | 1/2 | 1 | 1/3 |
| Stability | 2 | 2 | 3 | 1 |

---

## Step 3: Consensus Aggregation

### Geometric Mean Calculation (detailed)

For each cell (i, j), compute: `consensus = (P1 × P2 × P3 × P4)^(1/4)`

**Row 1 (Performance vs others):**
- Perf vs Eco: (3 × 1/2 × 1/2 × 1)^(1/4) = (0.75)^(0.25) = **0.930**
- Perf vs DevEx: (5 × 1/2 × 1 × 2)^(1/4) = (5.0)^(0.25) = **1.495**
- Perf vs Stab: (5 × 1/3 × 1/3 × 1/2)^(1/4) = (0.278)^(0.25) = **0.726**

**Row 2 (Ecosystem vs others):**
- Eco vs Perf: 1/0.930 = **1.075**
- Eco vs DevEx: (2 × 1 × 2 × 2)^(1/4) = (8.0)^(0.25) = **1.682**
- Eco vs Stab: (2 × 1 × 1 × 1/2)^(1/4) = (1.0)^(0.25) = **1.000**

**Row 3 (DevEx vs others):**
- DevEx vs Perf: 1/1.495 = **0.669**
- DevEx vs Eco: 1/1.682 = **0.595**
- DevEx vs Stab: (1 × 1 × 1/2 × 1/3)^(1/4) = (0.167)^(0.25) = **0.639**

**Row 4 (Stability vs others):**
- Stab vs Perf: 1/0.726 = **1.378**
- Stab vs Eco: 1/1.000 = **1.000**
- Stab vs DevEx: 1/0.639 = **1.565**

### Consensus Matrix

| vs | Performance | Ecosystem | DevEx | Stability |
|----|-------------|-----------|-------|-----------|
| Performance | 1.000 | 0.930 | 1.495 | 0.726 |
| Ecosystem | 1.075 | 1.000 | 1.682 | 1.000 |
| DevEx | 0.669 | 0.595 | 1.000 | 0.639 |
| Stability | 1.378 | 1.000 | 1.565 | 1.000 |

### Weight Calculation (LLSM — Row Geometric Means)

Row geometric mean = (product of all elements in row)^(1/4):

- **Performance**: (1.000 × 0.930 × 1.495 × 0.726)^(1/4) = (1.010)^(0.25) = **1.002**
- **Ecosystem**: (1.075 × 1.000 × 1.682 × 1.000)^(1/4) = (1.808)^(0.25) = **1.160**
- **DevEx**: (0.669 × 0.595 × 1.000 × 0.639)^(1/4) = (0.254)^(0.25) = **0.710**
- **Stability**: (1.378 × 1.000 × 1.565 × 1.000)^(1/4) = (2.157)^(0.25) = **1.212**

**Sum** = 1.002 + 1.160 + 0.710 + 1.212 = **4.084**

### Normalized Weights

| Criterion | Row GM | Weight | Verification |
|-----------|--------|--------|-------------|
| Performance | 1.002 | 1.002/4.084 = **0.245** | |
| Ecosystem | 1.160 | 1.160/4.084 = **0.284** | |
| DevEx | 0.710 | 0.710/4.084 = **0.174** | |
| Stability | 1.212 | 1.212/4.084 = **0.297** | |
| **Total** | | **1.000** | ✓ Sum = 1.0 |

**Weight Distribution**:
```
Stability & Governance: 0.297 ██████████████
Ecosystem & Compat:     0.284 ██████████████
Performance:            0.245 ████████████
Developer Experience:   0.174 ████████
```

---

## Step 4: Consistency Check

### Transitivity Verification

From the consensus matrix, the ranking order is:
**Stability (0.297) > Ecosystem (0.284) > Performance (0.245) > DevEx (0.174)**

Check all 6 pairwise relationships:

| Pair | Consensus Value | Consistent with Weights? |
|------|----------------|------------------------|
| Stab > Eco | a(Stab, Eco) = 1.000 ≈ 1 | Weights differ by 0.013 — near-tie ✓ |
| Stab > Perf | a(Stab, Perf) = 1.378 > 1 | Stab (0.297) > Perf (0.245) ✓ |
| Stab > DevEx | a(Stab, DevEx) = 1.565 > 1 | Stab (0.297) > DevEx (0.174) ✓ |
| Eco > Perf | a(Eco, Perf) = 1.075 > 1 | Eco (0.284) > Perf (0.245) ✓ |
| Eco > DevEx | a(Eco, DevEx) = 1.682 > 1 | Eco (0.284) > DevEx (0.174) ✓ |
| Perf > DevEx | a(Perf, DevEx) = 1.495 > 1 | Perf (0.245) > DevEx (0.174) ✓ |

### Transitivity Triples

| Triple | Check | Result |
|--------|-------|--------|
| Stab > Eco > Perf → Stab > Perf | 1.378 > 1 | ✓ |
| Stab > Eco > DevEx → Stab > DevEx | 1.565 > 1 | ✓ |
| Stab > Perf > DevEx → Stab > DevEx | 1.565 > 1 | ✓ |
| Eco > Perf > DevEx → Eco > DevEx | 1.682 > 1 | ✓ |

**All 4 triples pass transitivity. All 6 pairwise relationships are consistent.**

### Magnitude Reasonableness

- Stability and Ecosystem are near-equal (0.297 vs 0.284) — reasonable, as both CTO and DevOps prioritize these
- Performance (0.245) is below Stability — reasonable for a Series B company prioritizing reliability
- DevEx (0.174) is lowest — reasonable given the team already knows TypeScript/Node

**Conclusion**: The comparison matrix passes all consistency checks. ✓

---

## Step 5: Alternative Scoring

### Sub-criteria Weight Distribution

Distribute main criteria weights to sub-criteria proportionally:

| Sub-criterion | Parent | Parent Weight | Sub-weight | Final Weight |
|---------------|--------|---------------|------------|-------------|
| HTTP Throughput | Performance | 0.245 | 0.45 | **0.110** |
| JSON Processing | Performance | 0.245 | 0.30 | **0.074** |
| Startup/Memory | Performance | 0.245 | 0.25 | **0.061** |
| npm Compatibility | Ecosystem | 0.284 | 0.35 | **0.099** |
| Community Size | Ecosystem | 0.284 | 0.35 | **0.099** |
| Production Track Record | Ecosystem | 0.284 | 0.30 | **0.085** |
| TypeScript Support | DevEx | 0.174 | 0.35 | **0.061** |
| Built-in Tooling | DevEx | 0.174 | 0.30 | **0.052** |
| Package Mgmt Speed | DevEx | 0.174 | 0.35 | **0.061** |
| Project Maturity | Stability | 0.297 | 0.50 | **0.149** |
| Enterprise Adoption | Stability | 0.297 | 0.50 | **0.149** |

**Verification**: 0.110 + 0.074 + 0.061 + 0.099 + 0.099 + 0.085 + 0.061 + 0.052 + 0.061 + 0.149 + 0.149 = **1.000** ✓

### Scoring with Evidence

| Sub-criterion | Weight | Node.js | Deno | Bun | Evidence |
|---------------|--------|---------|------|-----|----------|
| HTTP Throughput | 0.110 | 5 | 6 | 10 | [D1] Node 29.7K, Deno 32.6K, Bun 146K req/s |
| JSON Processing | 0.074 | 5 | 5 | 10 | [D1] 1KB parse: Node 1.66M, Deno 1.71M, Bun 3.4M ops/s |
| Startup/Memory | 0.061 | 5 | 7 | 10 | [D2] Node ~25ms, Bun ~5ms startup |
| npm Compatibility | 0.099 | 10 | 7 | 9 | [D4] Node 100%, Deno ~90%, Bun ~95% |
| Community Size | 0.099 | 10 | 3 | 2 | [D2] SO: Node 475K, Deno 1.1K, Bun 264 questions |
| Production Track Record | 0.085 | 10 | 5 | 3 | [D5] Node: Netflix/PayPal; Deno: Slack; Bun: early startups |
| TypeScript Support | 0.061 | 5 | 9 | 9 | [D4] Deno/Bun native; Node via flag |
| Built-in Tooling | 0.052 | 4 | 9 | 7 | [D4] Deno: test+lint+fmt; Bun: test+build; Node: minimal |
| Package Mgmt Speed | 0.061 | 3 | 6 | 10 | [D4] bun install 47s vs npm 28min |
| Project Maturity | 0.149 | 10 | 7 | 4 | [D3] Node: 17 years, OpenJS Foundation; Bun: v1.0 only 2.5 years ago |
| Enterprise Adoption | 0.149 | 10 | 5 | 3 | [D5] Node 94% usage; Bun 23%, mostly non-production |

### Weighted Score Calculation (detailed)

**Node.js**:
```
= (0.110×5) + (0.074×5) + (0.061×5) + (0.099×10) + (0.099×10) + (0.085×10)
  + (0.061×5) + (0.052×4) + (0.061×3) + (0.149×10) + (0.149×10)
= 0.550 + 0.370 + 0.305 + 0.990 + 0.990 + 0.850
  + 0.305 + 0.208 + 0.183 + 1.490 + 1.490
= 7.731
```

**Deno**:
```
= (0.110×6) + (0.074×5) + (0.061×7) + (0.099×7) + (0.099×3) + (0.085×5)
  + (0.061×9) + (0.052×9) + (0.061×6) + (0.149×7) + (0.149×5)
= 0.660 + 0.370 + 0.427 + 0.693 + 0.297 + 0.425
  + 0.549 + 0.468 + 0.366 + 1.043 + 0.745
= 6.043
```

**Bun**:
```
= (0.110×10) + (0.074×10) + (0.061×10) + (0.099×9) + (0.099×2) + (0.085×3)
  + (0.061×9) + (0.052×7) + (0.061×10) + (0.149×4) + (0.149×3)
= 1.100 + 0.740 + 0.610 + 0.891 + 0.198 + 0.255
  + 0.549 + 0.364 + 0.610 + 0.596 + 0.447
= 6.360
```

### Cross-check Calculation

Let me verify Node.js score by regrouping by main criteria:

```
Node.js Performance  = (0.110×5 + 0.074×5 + 0.061×5) = 0.550+0.370+0.305 = 1.225
Node.js Ecosystem    = (0.099×10 + 0.099×10 + 0.085×10) = 0.990+0.990+0.850 = 2.830
Node.js DevEx        = (0.061×5 + 0.052×4 + 0.061×3) = 0.305+0.208+0.183 = 0.696
Node.js Stability    = (0.149×10 + 0.149×10) = 1.490+1.490 = 2.980
Node.js Total = 1.225 + 2.830 + 0.696 + 2.980 = 7.731 ✓
```

### Final Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **Node.js** | **7.73** |
| **Bun** | **6.36** |
| **Deno** | **6.04** |

### Sensitivity Analysis

**Scenario A** — Performance weight doubled (0.245 → 0.49), others proportionally reduced:

Re-normalized weights: Performance 0.49, Ecosystem 0.216, DevEx 0.132, Stability 0.226

```
Node.js: (0.49×5.0/10 scaled) + ...
Approximate recalculation:
  Node.js Performance contribution: 0.49 × 5.0 = 2.450 (was 1.225 at 0.245)
  Bun Performance contribution: 0.49 × 10.0 = 4.900 (was 2.450 at 0.245)

  Node.js ≈ 2.450 + (2.830×0.216/0.284) + (0.696×0.132/0.174) + (2.980×0.226/0.297)
         ≈ 2.450 + 2.153 + 0.528 + 2.268 = 7.399
  Bun    ≈ 4.900 + (1.344×0.216/0.284) + (1.523×0.132/0.174) + (1.043×0.226/0.297)
         ≈ 4.900 + 1.023 + 1.156 + 0.794 = 7.873
  Deno   ≈ 2.940 + (1.415×0.216/0.284) + (1.383×0.132/0.174) + (1.788×0.226/0.297)
         ≈ 2.940 + 1.077 + 1.049 + 1.360 = 6.426
```

Result: **Bun (7.87) overtakes Node.js (7.40)** when performance weight is doubled.

**Scenario B** — Stability weight tripled (0.297 → 0.50), others proportionally reduced:

```
  Node.js Stability contribution: 0.50 × 10.0 = 5.000
  Node.js ≈ greatly increased → ~8.2
  Bun Stability contribution: 0.50 × 3.5 = 1.750
  Bun ≈ drops to ~5.5
```

Result: **Node.js lead widens dramatically** when stability is paramount.

**Scenario C** — DevEx weight tripled (0.174 → 0.35):

```
  Bun DevEx is strong (TS + package speed), Deno DevEx is strongest (lint+fmt+test)
  Deno ≈ rises to ~6.5, Bun ≈ rises to ~6.8, Node.js ≈ drops to ~7.0
```

Result: Rankings unchanged, but **gap narrows significantly**.

### Sensitivity Summary

| Scenario | Node.js | Deno | Bun | Winner Change? |
|----------|---------|------|-----|---------------|
| Baseline | **7.73** | 6.04 | 6.36 | — |
| A: Performance 2x | 7.40 | 6.43 | **7.87** | **Yes — Bun overtakes** |
| B: Stability 3x | **~8.2** | ~5.5 | ~5.5 | No — Node.js gap widens |
| C: DevEx 2x | **~7.0** | ~6.5 | ~6.8 | No — but gap narrows |

**Critical Finding**: Node.js's lead is driven by **Stability & Ecosystem** (combined weight 0.581). Only when Performance becomes the overwhelmingly dominant criterion does Bun win. This reflects the reality: Bun is genuinely 3-5x faster, but Node.js's 17-year ecosystem and production track record carry enormous weight.

---

## Step 6: Decision Report

# Decision Report: JavaScript Runtime Selection for Real-time API Service

**Date**: 2026-02-27
**Information Source**: Document-Grounded Analysis (5 real data sources)

## Recommendation
**Node.js (v22+ LTS)** — Overall Score: **7.73 / 10**

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | Node.js | 7.73 | Unmatched ecosystem maturity, 94% developer adoption, 17-year production track record |
| 2 | Bun | 6.36 | 3-5x raw performance advantage, fastest package management, native TypeScript |
| 3 | Deno | 6.04 | Best security model, most complete built-in tooling, strong TypeScript support |

## Criteria Weight Distribution

| Criterion | Weight | Dominant Factor |
|-----------|--------|----------------|
| Stability & Governance | 0.297 | Node.js: OpenJS Foundation, 17 years of production use |
| Ecosystem & Compatibility | 0.284 | Node.js: 475K SO questions, 100% npm, Netflix/PayPal/LinkedIn |
| Performance | 0.245 | Bun: 146K req/s vs Node's 29K (5x advantage) [D1] |
| Developer Experience | 0.174 | Bun/Deno: native TypeScript, built-in tooling |

## Key Trade-offs

- **Node.js vs Bun: The 1.37-point gap is real but contextual.** Bun's 5x HTTP throughput [D1] is spectacular in benchmarks, but real-world workloads with database I/O, network latency, and business logic narrow this gap significantly (HackerNoon's real-world test showed only ~3% difference: 12K vs 12.4K req/s)
- **The Ecosystem moat**: Node.js has 475K Stack Overflow answers [D2] vs Bun's 264. When your team hits an obscure bug at 3 AM, this 1,800:1 ratio matters more than any benchmark
- **Bun's open issues concern**: 6,066 open issues [D3] vs Node's 2,487 — a 2.4x ratio despite being a much younger project. This signals rapid development but also instability risk
- **Deno's security advantage is unique**: Permission-based sandbox by default [D4] — neither Node nor Bun offer this. For security-sensitive APIs handling user data, this is a genuine differentiator that wasn't fully captured in the scoring

## Risk Assessment

- **Choosing Node.js**: Risk of missing performance gains; mitigate by using performance-optimized frameworks (Fastify > Express) and profiling
- **Choosing Bun**: Risk of production instability (v1.0 only 2.5 years ago), limited cloud provider support, sparse community resources; mitigate by thorough testing and maintaining Node.js fallback
- **Choosing Deno**: Risk of npm compatibility gaps (~90%), smaller community; mitigate by using Deno 2.0+ with npm: specifier

## Information Sources

| ID | Source | Used For |
|----|--------|----------|
| D1 | [RepoFlow Benchmarks](https://www.repoflow.io/blog/node-js-vs-deno-vs-bun-performance-benchmarks) | HTTP throughput, JSON parsing scores |
| D2 | [BetterStack](https://betterstack.com/community/guides/scaling-nodejs/nodejs-vs-deno-vs-bun/) / [Snyk](https://snyk.io/blog/javascript-runtime-compare-node-deno-bun/) | Express benchmarks, startup time, SO questions |
| D3 | GitHub API (live) | Stars, forks, open issues |
| D4 | [DEV.to](https://dev.to/pockit_tools/deno-2-vs-nodejs-vs-bun-in-2026-the-complete-javascript-runtime-comparison-1elm) / [Pullflow](https://pullflow.com/blog/deno-vs-bun-2025/) | Compatibility, tooling, governance |
| D5 | [State of JavaScript 2024](https://2024.stateofjs.com/en-US) | Usage rates, adoption trends |

## Recommendations

1. **Use Node.js v22 LTS** for the real-time API service with **Fastify** instead of Express (2-3x throughput improvement over Express on Node.js alone)
2. **Benchmark your actual workload** on Bun before dismissing it — if your service is purely HTTP/JSON with minimal npm dependencies, Bun's performance advantage may be worth the ecosystem trade-off
3. **Set a 12-month Bun checkpoint**: Revisit when Bun reaches v2.0 and the open issues count stabilizes
4. **Adopt Bun for non-critical tooling now**: Use `bun install` (47s vs npm's 28min) and `bun test` for CI — get the speed benefits without the production risk
5. **If security is paramount**: Seriously evaluate Deno's permission sandbox for any service handling PII or financial data
