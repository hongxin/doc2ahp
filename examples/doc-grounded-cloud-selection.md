# Example: Cloud Provider Selection (Document-Grounded Mode)

[中文](doc-grounded-cloud-selection_ZH.md)

> Scenario: A healthcare SaaS startup needs to choose a cloud provider for their new HIPAA-compliant patient data platform. Unlike the other examples that use Quick Analysis mode, this example demonstrates **Document-Grounded mode** — criteria are extracted from actual project documents, with full source traceability.

## Step 0: Decision Input Mode Selection

**Mode Selected**: A — Document-Grounded Analysis

The team provided the following materials:

| # | Source Document | Type | Key Content |
|---|----------------|------|-------------|
| D1 | `product_requirements.md` | Requirements doc | Feature requirements, compliance needs, expected user scale |
| D2 | `security_audit_checklist.pdf` | Compliance doc | HIPAA requirements, encryption standards, audit trail needs |
| D3 | `infra_budget_2026.xlsx` | Budget plan | Annual infrastructure budget of $180K, growth projections |
| D4 | AWS vs Azure vs GCP Healthcare Comparison (web search) | Web article | Feature-by-feature comparison of healthcare cloud offerings |
| D5 | Team skills survey results | Internal survey | 70% AWS experience, 20% GCP, 10% Azure |

### Criteria Extraction from Documents

After reading all 5 sources, the following candidate criteria were extracted:

| Extracted Criterion | Source | Evidence |
|--------------------|--------|----------|
| HIPAA BAA availability | D2, Section 2.1 | "Cloud provider MUST offer a signed Business Associate Agreement" |
| Data encryption (at rest + in transit) | D2, Section 3.4 | "AES-256 encryption at rest, TLS 1.3 in transit required" |
| Audit logging & access trails | D2, Section 4.2 | "All PHI access must be logged with immutable audit trail" |
| Auto-scaling for patient load spikes | D1, Section 5 | "System must handle 10x normal load during flu season" |
| Multi-region failover | D1, Section 6.3 | "RPO < 1 hour, RTO < 15 minutes for disaster recovery" |
| Annual cost within $180K budget | D3, Sheet "Projections" | "Year 1 infra budget: $180K, Year 2: $250K with growth" |
| Reserved instance / commitment discounts | D3, Sheet "Savings" | "Explore 1-year or 3-year commitments for cost savings" |
| Healthcare-specific AI/ML services | D1, Section 8 | "Future plan: integrate medical imaging AI and NLP for clinical notes" |
| FHIR API support | D1, Section 7.2 | "Must support HL7 FHIR R4 for interoperability" |
| Team's existing cloud skills | D5 | "70% of team is AWS-certified; 1 GCP expert; minimal Azure" |
| Managed Kubernetes offering | D1, Section 4.1 | "Microservices architecture, container orchestration required" |
| Compliance certification breadth | D4, Web search | "Compare SOC2, HITRUST, FedRAMP certifications across providers" |

**τ (tau) Relevance Filter Applied**:
- ~~"Serverless function cold start time"~~ — appeared only in D4 as a minor note, not relevant to the healthcare platform's architecture decision → **Filtered out**
- ~~"Edge computing availability"~~ — mentioned in D4 but no requirement in D1 or D2 → **Filtered out**

**12 criteria extracted → 10 retained after τ filter**

## Step 1: Decision Framework Construction

**Decision Goal**: Select the cloud provider best suited for a HIPAA-compliant healthcare SaaS platform

**Evaluation Hierarchy** (organized from the 10 extracted criteria):

```
Select the Best Cloud Provider for Healthcare SaaS
├── Compliance & Security [D2]
│   ├── HIPAA BAA & Certification Breadth [D2 §2.1, D4]
│   ├── Data Encryption Standards [D2 §3.4]
│   └── Audit Logging & Access Control [D2 §4.2]
├── Technical Fit [D1]
│   ├── Auto-scaling Capability [D1 §5]
│   ├── Multi-region Failover (RPO/RTO) [D1 §6.3]
│   └── Managed Kubernetes Quality [D1 §4.1]
├── Healthcare Ecosystem [D1, D4]
│   ├── Healthcare AI/ML Services [D1 §8]
│   └── FHIR API & Interoperability [D1 §7.2]
└── Cost & Team [D3, D5]
    ├── TCO within Budget Constraints [D3]
    └── Team Skill Match [D5]
```

Note: Each criterion is tagged with its source document for traceability.

**Alternatives**:
- **AWS** (Amazon Web Services)
- **Azure** (Microsoft Azure)
- **GCP** (Google Cloud Platform)

**User Priority Constraint**: Compliance is non-negotiable — "We cannot launch without HIPAA compliance on day one." [D2, Executive Summary]

## Steps 2-3: Evaluation & Aggregation (Condensed)

Combining evaluations from four perspectives: Cloud Architect, CISO (Security), Healthcare Domain Expert, and CFO:

**Consensus Weights** (with compliance priority constraint applied):

```
Compliance & Security: 0.38 ███████████████████
Technical Fit:         0.27 █████████████
Healthcare Ecosystem:  0.20 ██████████
Cost & Team:           0.15 ███████
```

(The "compliance non-negotiable" constraint boosted Compliance & Security by 2 scale levels)

## Step 4: Consistency Check

- Compliance & Security > Technical Fit > Healthcare Ecosystem > Cost & Team ✓
- Compliance & Security > Healthcare Ecosystem ✓ (transitivity satisfied)
- Technical Fit > Cost & Team ✓ (transitivity satisfied)
- Passes consistency check ✓

## Step 5: Alternative Scoring

Each score is grounded in document evidence where available:

| Sub-criterion | Weight | AWS | Azure | GCP | Scoring Basis |
|---------------|--------|-----|-------|-----|---------------|
| HIPAA BAA & Certifications | 0.15 | 9 | 9 | 8 | [D4] AWS & Azure have HITRUST; GCP lacks HITRUST |
| Data Encryption Standards | 0.12 | 9 | 9 | 9 | [D2 §3.4] All three meet AES-256 + TLS 1.3 |
| Audit Logging & Access | 0.11 | 9 | 8 | 7 | [D4] AWS CloudTrail most mature; GCP audit logs improving |
| Auto-scaling | 0.10 | 9 | 8 | 9 | [D1 §5] AWS & GCP auto-scaling equally strong |
| Multi-region Failover | 0.09 | 9 | 8 | 8 | [D1 §6.3] AWS has most regions; all meet RPO/RTO targets |
| Managed Kubernetes | 0.08 | 8 | 7 | 9 | [D1 §4.1] GKE widely considered best managed K8s |
| Healthcare AI/ML | 0.11 | 8 | 9 | 8 | [D1 §8] Azure has healthcare-specific AI models (Med-PaLM via GCP is close) |
| FHIR API Support | 0.09 | 8 | 9 | 8 | [D1 §7.2] Azure FHIR Server is most mature; AWS HealthLake competitive |
| TCO within Budget | 0.08 | 7 | 7 | 8 | [D3] GCP sustained-use discounts best for predictable workloads |
| Team Skill Match | 0.07 | 9 | 4 | 6 | [D5] 70% team is AWS-certified |

### Weighted Scores

| Alternative | Weighted Total Score |
|-------------|---------------------|
| **AWS** | **8.47** |
| **Azure** | **7.88** |
| **GCP** | **7.85** |

### Sensitivity Analysis

Scenario A — Reducing "Team Skill Match" weight from 0.07 to 0.02 (willing to retrain):
- AWS: 8.28 → Rank 1
- Azure: 7.92 → Rank 2
- GCP: 7.90 → Rank 3

Scenario B — Increasing "Healthcare Ecosystem" weight from 0.20 to 0.35 (future AI/ML roadmap critical):
- Azure: 8.15 → **Rank 1** (healthcare AI advantage shines)
- AWS: 8.10 → Rank 2 (near tie)
- GCP: 7.88 → Rank 3

**Key Finding**: AWS leads robustly in the baseline scenario. Azure overtakes only when healthcare-specific ecosystem becomes the dominant factor. The team's AWS expertise (70%) provides a strong practical advantage that's hard to ignore.

## Step 6: Decision Report

# Decision Report: Cloud Provider Selection for Healthcare SaaS

## Recommendation
**AWS** — Overall Score: 8.47 / 10

## Ranking

| Rank | Alternative | Score | Key Strength |
|------|------------|-------|-------------|
| 1 | AWS | 8.47 | Most mature HIPAA tooling, strongest team match, broadest compliance certifications |
| 2 | Azure | 7.88 | Best healthcare-specific ecosystem (FHIR, health AI), strong enterprise compliance |
| 3 | GCP | 7.85 | Best managed Kubernetes, competitive pricing, but thinnest healthcare-specific offering |

## Criteria Weight Distribution

| Criterion | Weight | Source Document |
|-----------|--------|----------------|
| Compliance & Security | 0.38 | D2: security_audit_checklist.pdf |
| Technical Fit | 0.27 | D1: product_requirements.md |
| Healthcare Ecosystem | 0.20 | D1: product_requirements.md, D4: web search |
| Cost & Team | 0.15 | D3: infra_budget_2026.xlsx, D5: team survey |

## Key Trade-offs
- **AWS vs Azure**: AWS leads on compliance maturity and team fit; Azure leads on healthcare-specific AI/ML services. If the AI roadmap (D1 §8) accelerates, Azure becomes more attractive
- **GCP's K8s advantage**: GKE is technically superior, but the team would need significant retraining [D5], and GCP's healthcare compliance portfolio is thinner [D4]
- **The team skill factor**: 70% AWS certification [D5] translates to faster time-to-market and fewer operational incidents during the critical launch phase

## Risk Assessment
- AWS's healthcare AI services lag behind Azure; plan to evaluate Azure AI Health Insights for the Phase 2 ML roadmap [D1 §8]
- HIPAA compliance requires ongoing vigilance — schedule quarterly compliance reviews regardless of provider choice [D2]
- Budget projections [D3] show Year 2 costs rising to $250K; negotiate reserved instance pricing early

## Information Sources
| Source | Description | Used In |
|--------|-------------|---------|
| D1: product_requirements.md | Product feature requirements and scale targets | Criteria extraction, scoring |
| D2: security_audit_checklist.pdf | HIPAA compliance requirements | Compliance criteria, priority constraint |
| D3: infra_budget_2026.xlsx | Infrastructure budget and projections | Cost criteria, budget constraints |
| D4: Web search results | Healthcare cloud provider comparison articles | Certification comparison, scoring |
| D5: Team skills survey | Team cloud experience distribution | Team skill match scoring |

## Recommendations
1. Choose AWS as the primary cloud provider
2. Set up AWS HIPAA-eligible services and sign BAA within Week 1
3. Deploy on EKS (Elastic Kubernetes Service) with multi-AZ configuration
4. Reserve 1-year compute instances to stay within the $180K Year 1 budget [D3]
5. Evaluate Azure AI Health Insights as a cross-cloud service for Phase 2 ML features [D1 §8]
6. Schedule a cloud provider reassessment at Month 12 with updated requirements

---

## What Makes This Example Different?

This example uses **Document-Grounded mode (Mode A)** instead of Quick Analysis mode. Key differences:

| Aspect | Quick Analysis (Mode B) | Document-Grounded (Mode A, this example) |
|--------|------------------------|------------------------------------------|
| Criteria source | LLM's general knowledge | Extracted from actual project documents |
| Traceability | None — "based on domain knowledge" | Every criterion tagged with `[Source: Doc, Section]` |
| τ filter | Not applicable | Applied — 2 irrelevant criteria filtered out |
| Scoring basis | LLM's assessment | Grounded in document evidence where available |
| Decision report | General recommendations | Source-referenced recommendations linked to specific documents |
| Reproducibility | Depends on LLM | Auditable — anyone can verify criteria against source docs |
