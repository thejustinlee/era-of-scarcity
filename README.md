# WACT
# Era of Scarcity

Frameworks and methodologies for enterprise AI infrastructure decisions — inference placement, token economics, and data governance.

**Live:** [thejustinlee.github.io/era-of-scarcity](https://thejustinlee.github.io/era-of-scarcity/)

---

## WACT — Weighted Average Cost of Tokens

A method for calculating true enterprise AI inference cost, weighted by workforce distribution across data classification tiers rather than a flat per-seat assumption. Adapted from the logic of Weighted Average Cost of Capital.

**[Read the methodology →](https://thejustinlee.github.io/era-of-scarcity/wact/)**

### The problem it solves

Enterprise AI cost modeling and AI data governance are typically owned by different teams and modeled separately. One optimizes token spend. The other governs where data is permitted to go. Neither produces a number the other can use.

Your data classification policy already determines which model tier and which deployment architecture each segment of your workforce is permitted to use. That constraint has a cost. WACT calculates it.

### Formula

**Step 1 — Per-tier cost**

```
Tier_n_Cost = (input_ratio × input_rate + output_ratio × output_rate)
              × tokens_per_employee
              × tier_employees
```

**Step 2 — Enterprise WACT**

```
        T1_Cost + T2_Cost + T3_Cost + T4_Cost + T5_Cost
WACT = ─────────────────────────────────────────────────
                    total_tokens (in millions)
```

### Tier model

| Tier | Classification | Ratio (in/out) | Workload character | Rate basis |
|------|---------------|----------------|-------------------|------------|
| 1 | Public | 30 / 70 | General queries, no context depth | OpEx — any provider |
| 2 | Internal | 30 / 70 | Operational comms, lightweight outputs | OpEx — any provider |
| 3 | Confidential | 30 / 70 | Knowledge work, deliverable generation | OpEx (conditional) or CapEx |
| 4 | Restricted | 50 / 50 | Agent / automation, SaaS orchestration | CapEx — open-weight only |
| 5 | Strictly Confidential | 70 / 30 | RAG-heavy — contracts, patents, code | CapEx — open-weight only |

Tiers 4 and 5 use a CapEx basis because frontier closed-weight models are not self-hostable. Where hyperscale cloud is not a permissible deployment, the available model set narrows to open-weight architectures running on owned infrastructure — and the cost structure shifts from per-token OpEx to amortized CapEx.

### CapEx derivation

```
                    Hardware_Cost
CapEx_Rate = ─────────────────────────────────────────────
             Useful_Life_sec × Utilization_Rate × Throughput
```

Reference inputs used in the worked example:

| Input | Value |
|-------|-------|
| 8× H100 cluster | ~$240,000 |
| Useful life | 2.5 years |
| Utilization rate | 50% |
| Throughput (cluster) | ~20,000 tok/sec |
| **Derived CapEx rate** | **~$0.30 / 1M tokens** |

Utilization is the most sensitive input in the model. Low utilization erases the cost advantage of owned infrastructure entirely.

### Worked example

A 10,000-employee organization on a financial services tier profile (30% T1/T2, 55% T3, 10% T4, 5% T5) at 500K tokens per employee per month:

| Tier | Employees | Blended rate | Monthly cost |
|------|-----------|--------------|--------------|
| T1/T2 | 3,000 | $3.80 | $5,700 |
| T3 | 5,500 | $11.40 | $31,350 |
| T4 | 1,000 | $0.30 | $152 |
| T5 | 500 | $0.30 | $76 |
| **Total** | **10,000** | — | **~$37,278** |

**Enterprise WACT: $7.46 / 1M tokens**

A law firm or biotech with a heavier T4/T5 population produces a materially lower figure — more of the workforce sits on near-zero CapEx-amortized cost instead of OpEx pricing.

### Rate reference

Published API rates per 1M tokens, verified 10 August 2026:

| Provider | Model | Input | Output | Blended @ 30/70 |
|----------|-------|-------|--------|-----------------|
| Anthropic | Claude Haiku 4.5 | $1.00 | $5.00 | $3.80 |
| Anthropic | Claude Sonnet 4.6 | $3.00 | $15.00 | $11.40 |
| Anthropic | Claude Opus 4.8 | $5.00 | $25.00 | $19.00 |
| OpenAI | GPT-5 Mini | $0.125 | $1.00 | $0.74 |
| OpenAI | GPT-5 | $0.625 | $5.00 | $3.69 |
| Google | Gemini 3 Pro | $2.00 | $12.00 | $9.00 |

Rates move. OpenAI reduced GPT-5 and GPT-5 Mini input pricing by roughly 50% between April and August 2026 while Anthropic and Google held flat. WACT is expressed as a formula rather than a fixed figure for exactly this reason — the blended rate is an input you refresh, not a constant.

Batch processing (50% discount) and prompt caching (up to 90% off cached input) reduce effective rates further and should be modeled separately where applicable.

---

## Assumptions and limitations

WACT is a framework, not a fixed answer. Accurate output requires your own inputs.

- **Workforce distribution** varies significantly by industry — retail skews T1/T2, law and biotech skew T4/T5
- **Token volume per employee** — 500K/month is a mid-range planning assumption, not a measured figure
- **Token ratios by tier** reflect typical workload archetypes, not a universal law
- **Hardware utilization** is the most sensitive CapEx input
- **Tax treatment** assumes a tax-paying U.S. entity; Section 179 and bonus depreciation treatment varies by structure
- **Model pricing** reflects publicly posted rates subject to change without notice

This is a financial planning framework, not tax or legal advice. Consult qualified counsel before applying depreciation treatment.

---

## Roadmap

- [ ] Interactive WACT calculator — configurable workforce distribution, token volume, and hardware assumptions
- [ ] Industry preset profiles for tier distribution
- [ ] Data custody framework page — inference placement by classification tier

---

## Author

**Justin Lee** — Enterprise AI & Compute

[LinkedIn](https://www.linkedin.com/in/justinsjlee/)
