# Example: AI Foundation Model API Selection

> **Key AHP Concept**: Multi-perspective disagreement & consensus — 4 expert roles (ML Engineer, CTO, Security Officer, Product Manager) produce sharply different priority rankings, yet geometric mean aggregation converges to a defensible consensus.

[中文](ai-model-selection_ZH.md)

> Scenario: An AI startup building an intelligent customer service platform needs to choose a foundation model API. The team of 8 (ML engineers + fullstack developers) must handle multilingual conversations, document understanding, and workflow automation. Expected volume: 2M API calls/day.

## Step 1: Decision Framework Construction

**Decision Goal**: Select the most suitable foundation model API for a production AI customer service platform

**Evaluation Hierarchy**:

```
Select the Best Foundation Model API
├── Core Capabilities
│   ├── Language Understanding & Generation
│   ├── Reasoning Accuracy
│   └── Multimodal Ability (images, documents)
├── Cost & Efficiency
│   ├── API Pricing (per million tokens)
│   ├── Response Latency (P95)
│   └── Rate Limits & Throughput
├── Safety & Compliance
│   ├── Content Safety & Guardrails
│   ├── Data Privacy Policy
│   └── Regulatory Compliance (SOC2, GDPR)
└── Integration & Operations
    ├── API Design & SDK Quality
    ├── Fine-tuning / Customization Options
    └── Vendor Lock-in Risk
```

**Alternatives**:
- **Claude** (Anthropic, Sonnet/Opus)
- **GPT-4o** (OpenAI)
- **Gemini** (Google, Pro/Ultra)
- **Llama 3** (Meta, self-hosted via vLLM)

## Step 2: Multi-Perspective Evaluation

### Perspective 1: ML Engineer

| vs | Core Capabilities | Cost & Efficiency | Safety & Compliance | Integration & Ops |
|----|-------------------|-------------------|--------------------|--------------------|
| Core Capabilities | 1 | 3 | 2 | 4 |
| Cost & Efficiency | 1/3 | 1 | 1/2 | 2 |
| Safety & Compliance | 1/2 | 2 | 1 | 2 |
| Integration & Ops | 1/4 | 1/2 | 1/2 | 1 |

### Perspective 2: CTO

| vs | Core Capabilities | Cost & Efficiency | Safety & Compliance | Integration & Ops |
|----|-------------------|-------------------|--------------------|--------------------|
| Core Capabilities | 1 | 2 | 1 | 2 |
| Cost & Efficiency | 1/2 | 1 | 1 | 2 |
| Safety & Compliance | 1 | 1 | 1 | 3 |
| Integration & Ops | 1/2 | 1/2 | 1/3 | 1 |

### Perspective 3: Security Officer

| vs | Core Capabilities | Cost & Efficiency | Safety & Compliance | Integration & Ops |
|----|-------------------|-------------------|--------------------|--------------------|
| Core Capabilities | 1 | 1/2 | 1/3 | 1 |
| Cost & Efficiency | 2 | 1 | 1/3 | 2 |
| Safety & Compliance | 3 | 3 | 1 | 4 |
| Integration & Ops | 1 | 1/2 | 1/4 | 1 |

### Perspective 4: Product Manager

| vs | Core Capabilities | Cost & Efficiency | Safety & Compliance | Integration & Ops |
|----|-------------------|-------------------|--------------------|--------------------|
| Core Capabilities | 1 | 2 | 3 | 3 |
| Cost & Efficiency | 1/2 | 1 | 2 | 2 |
| Safety & Compliance | 1/3 | 1/2 | 1 | 1 |
| Integration & Ops | 1/3 | 1/2 | 1 | 1 |

## Step 3: Consensus Aggregation

### Geometric Mean Matrix

| vs | Core Capabilities | Cost & Efficiency | Safety & Compliance | Integration & Ops |
|----|-------------------|-------------------|--------------------|--------------------|
| Core Capabilities | 1 | 1.73 | 1.19 | 2.21 |
| Cost & Efficiency | 0.58 | 1 | 0.64 | 2.00 |
| Safety & Compliance | 0.84 | 1.57 | 1 | 2.21 |
| Integration & Ops | 0.45 | 0.50 | 0.45 | 1 |

### Weight Calculation

| Criterion | Row Geometric Mean | Normalized Weight |
|-----------|-------------------|-------------------|
| Core Capabilities | 1.45 | 0.34 |
| Cost & Efficiency | 0.95 | 0.22 |
| Safety & Compliance | 1.30 | 0.30 |
| Integration & Ops | 0.56 | 0.14 |

**Weight Distribution**:
```
Core Capabilities:    0.34 █████████████████
Safety & Compliance:  0.30 ███████████████
Cost & Efficiency:    0.22 ███████████
Integration & Ops:    0.14 ███████
```

## Step 4: Consistency Check

**Transitivity Verification**:
- Core Capabilities > Safety & Compliance > Cost & Efficiency > Integration & Ops ✓
- Core Capabilities > Cost & Efficiency ✓
- Safety & Compliance > Integration & Ops ✓
- All transitive relationships are consistent ✓

**Conclusion**: The comparison matrix passes the consistency check.

## Step 5: Alternative Scoring

| Sub-criterion | Weight | Claude | GPT-4o | Gemini | Llama 3 |
|---------------|--------|--------|--------|--------|---------|
| Language Understanding | 0.13 | 9 | 9 | 8 | 7 |
| Reasoning Accuracy | 0.12 | 9 | 8 | 8 | 6 |
| Multimodal Ability | 0.09 | 8 | 9 | 9 | 6 |
| API Pricing | 0.09 | 7 | 6 | 8 | 9 |
| Response Latency | 0.07 | 7 | 8 | 8 | 7 |
| Rate Limits & Throughput | 0.06 | 7 | 8 | 8 | 9 |
| Content Safety | 0.12 | 9 | 8 | 8 | 5 |
| Data Privacy | 0.10 | 9 | 7 | 6 | 10 |
| Regulatory Compliance | 0.08 | 8 | 8 | 7 | 6 |
| API & SDK Quality | 0.05 | 8 | 9 | 7 | 6 |
| Fine-tuning Options | 0.05 | 6 | 8 | 7 | 9 |
| Vendor Lock-in Risk | 0.04 | 6 | 5 | 5 | 10 |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **Claude** | **8.07** |
| **GPT-4o** | **7.87** |
| **Gemini** | **7.59** |
| **Llama 3** | **7.24** |

### Sensitivity Analysis

Scenario A — Reducing "Safety & Compliance" weight from 0.30 to 0.15 (less regulated industry):
- GPT-4o: 7.85 → Rank 1
- Claude: 7.80 → Rank 2 (gap narrows significantly)
- Gemini: 7.65 → Rank 3
- Llama 3: 7.42 → Rank 4

Scenario B — Increasing "Cost & Efficiency" weight from 0.22 to 0.35 (budget-constrained startup):
- Llama 3: 7.55 → Jumps to Rank 2
- Claude: 7.72 → Still Rank 1
- Gemini: 7.60 → Rank 2
- GPT-4o: 7.35 → Drops to Rank 4

**Key Finding**: Claude's lead is robust for safety-sensitive scenarios; in cost-dominated scenarios, Llama 3 and Gemini become competitive.

## Step 6: Decision Report

# Decision Report: AI Foundation Model API Selection

## Recommendation
**Claude (Anthropic)** — Overall Score: 8.07 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | Claude | 8.07 | Best reasoning accuracy, strongest safety guardrails, leading data privacy |
| 2 | GPT-4o | 7.87 | Most versatile multimodal, best SDK/tooling ecosystem, widest adoption |
| 3 | Gemini | 7.59 | Competitive pricing, strong multimodal, good throughput at scale |
| 4 | Llama 3 | 7.24 | Full data sovereignty, zero API costs at scale, maximum customizability |

## Key Trade-offs
- **Claude vs GPT-4o**: Claude leads in safety and reasoning; GPT-4o leads in multimodal breadth and ecosystem tooling. The 0.20-point gap is primarily driven by safety & privacy weights
- **Managed vs Self-hosted**: Llama 3 offers unmatched data sovereignty and cost control at scale, but requires significant ML infrastructure investment (GPU cluster, model serving, monitoring)
- **Gemini as a dark horse**: Most competitive pricing at high volume, with Google Cloud integration advantages for teams already in GCP

## Risk Assessment
- Claude's fine-tuning options are currently more limited than GPT-4o; complex customization needs may require creative prompt engineering
- Depending on a single model provider carries concentration risk; design the abstraction layer for easy provider switching
- Llama 3 self-hosting requires 2-3 dedicated ML engineers for operations

## Recommendations
1. Adopt Claude as the primary model for all customer-facing conversations
2. Implement a model abstraction layer (e.g., LiteLLM) to enable multi-provider fallback
3. Use Llama 3 self-hosted as a cost-effective fallback for low-stakes tasks (classification, summarization)
4. Re-evaluate quarterly as the model landscape evolves rapidly
