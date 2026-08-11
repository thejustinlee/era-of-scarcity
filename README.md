# Era of Scarcity

Frameworks for the decisions that sit between AI governance and AI cost — inference placement, token economics, and data custody in the enterprise.

### → **[Read the live methodologies](https://thejustinlee.github.io/era-of-scarcity/)**

---

## What's here

### [WACT — Weighted Average Cost of Tokens](https://thejustinlee.github.io/era-of-scarcity/wact/)

Enterprise AI cost is usually modeled as a flat per-seat or per-token assumption. That understates it in some organizations and badly overstates it in others, because it ignores the thing that actually governs cost: which data classification tier each part of your workforce operates in, and what that tier permits.

WACT borrows the blending logic of Weighted Average Cost of Capital and applies it to token spend — weighted by workforce distribution across data tiers, with OpEx API pricing and CapEx-amortized infrastructure treated as distinct cost structures. The output is a single organization-specific figure rather than a vendor benchmark.

**In development:** an interactive calculator, and a data custody framework mapping classification tiers to permissible inference environments.

---

## Why this exists

Most published AI cost analysis is written either for developers, in per-token units that don't roll up to a budget, or for executives, in narrative that doesn't survive contact with a spreadsheet. Meanwhile governance and cost are typically owned by different teams who never model the same number.

These frameworks are an attempt at the middle: methodology precise enough that a CFO can check the arithmetic, framed around a constraint a CISO already recognizes.

They're written from the enterprise adoption surface rather than from the outside — which means friction gets named honestly, including friction that cuts against the infrastructure categories I work in.

---

## Using this

Every figure published here is derived, sourced, and dated. Rates move — model pricing changed materially between April and August 2026 — so the methodologies are expressed as formulas with refreshable inputs rather than fixed conclusions. Where an assumption is soft, it's labeled as soft.

Feel free to use, adapt, or cite these frameworks with attribution. If you find an error in the math or a flaw in the reasoning, open an issue — that's the most useful thing you could do with this repo.

**Not tax, legal, or investment advice.**

---

**Justin Lee** — Enterprise AI & Compute
[linkedin.com/in/justinsjlee](https://www.linkedin.com/in/justinsjlee/)
