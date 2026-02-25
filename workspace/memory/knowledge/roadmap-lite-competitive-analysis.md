# Roadmap Lite — Competitive Analysis
*Captured from Rob's screenshots — session Feb 2026*

---

## Product Overview
- Direct competitor to PropPath
- Dark UI, similar concept: BA inputs financial profile → builds property pipeline → shows output
- Target market: Same (investment-focused BAs in Australia)

---

## Screen 1: Financial Profile & Borrowing Power

### Borrowing Power Display
- **Prominent hero number: $1,561,747** (large green text at top)
- Subtitle: *"Calculated on the lower of Serviceability or 6x DTI cap."*
- **Key insight: DTI cap is built in and labelled prominently** — PropPath has no DTI check at all

### Input Fields (Financial Profile)
| Field | Default Value |
|-------|--------------|
| Applicant 1 Income | $150,000 |
| Applicant 2 Income | $120,000 |
| Other Income | $0 |
| Living Expenses (monthly) | $4,000 |
| Dependents | 0 |
| Credit Card Limits | $10,000 |
| Other Loans (monthly) | $0 |
| Cash Savings (Starting Capital) | $200,000 |

### Key Differences vs PropPath
- Roadmap Lite calculates borrowing power FROM income/expenses (proper serviceability model)
- PropPath's borrowing calculator is standalone, reverse-engineered from repayment amount — simpler but disconnected
- **Roadmap Lite labels DTI explicitly in the UI** — trust signal for savvy clients
- No "Annual Savings" field — they use income/expenses to derive capacity

---

## Screen 2: Property Pipeline

### Property Defaults
- All 6 properties: $650k purchase price, MODERATE growth tag
- Weekly Rent: $688 (yield ≈ 5.5% on $650k)
- **Deposit: 20%** — consistent 80% LVR default (vs PropPath's 88% LVR = 12% deposit)
- Cash Contribution: $0

### Pipeline Layout
| Property | Date | Price | Growth Tag |
|----------|------|-------|------------|
| Property 1 | Feb 2026 | $650k | MODERATE |
| Property 2 | Aug 2027 | $650k | MODERATE |
| Property 3 | Jul 2028 | $650k | MODERATE |
| Property 4 | Mar 2029 | $650k | MODERATE |
| Property 5 | Jan 2031 | $650k | MODERATE |
| Property 6 | Jan 2034 | $650k | MODERATE |

### Property Tabs
- DETAILS | BUYING COSTS | ASSUMPTIONS | EXPENSES
- Simple 4-tab structure (PropPath has same tabs but more granular data)

### Buying Costs Tab
| Item | Value |
|------|-------|
| Stamp Duty | $26,000 |
| Buyer's Agent Fee | $0 |
| Other Buying Costs | $3,000 |
| **Total Buying Costs** | **$29,000** |

*Much simpler than PropPath — no engagement fee, no conditional holding deposit, no building/pest inspection, no conveyancing line items*

### Expenses Tab (Annual)
| Item | Value |
|------|-------|
| Council Rates (p.a.) | $1,800 |
| Insurance (p.a.) | $1,200 |
| Maintenance (p.a.) | $600 |
| Management Fee | 6.0% |

**Critical: NO vacancy rate field visible** — same gap as PropPath (vacancy = 0)
*PropPath has vacancyRate in defaults set to 0 for most types — same problem*

### Assumptions Tab
- **Capital Growth Profile: MODERATE = "15% p.a. (Years 1-4), then 10% p.a."**
- Interest Rate: 5.9%

---

## 🚨 Critical Finding: Growth Rate Comparison

| Tier | Roadmap Lite | PropPath "High" (tiered) |
|------|-------------|--------------------------|
| Year 1 | 15% p.a. | 12.5% p.a. |
| Years 2-3 | 15% p.a. | 10% p.a. |
| Year 4 | 15% p.a. | 7.5% p.a. |
| Year 5+ | 10% p.a. | 6% p.a. |

**Roadmap Lite's MODERATE is MORE aggressive than PropPath's HIGH.**
- Roadmap Lite Moderate: 15% for 4 years, then 10%
- PropPath High: 12.5% → 10% → 7.5% → 6% (tiered down)

This means PropPath is already more conservative on growth than the competitor's "middle" tier.
This is both a risk (RL's numbers look better) and an opportunity (PropPath numbers are more defensible).

---

## Screen 3: Dashboard Output

### Plan Status Banner
- "✅ PLAN FEASIBLE — All properties purchased successfully."
- PropPath equivalent: guardrail system (deposit/borrowing/serviceability tests)
- Roadmap Lite presents this as a YES/NO at the top — clean and decisive

### Performance at Deadline (Feb 2036) KPI Strip
| Metric | Value |
|--------|-------|
| VALUE | $8,960,740 |
| EQUITY | $5,041,341 |
| GROSS CF | $299,818 |
| NET CF | $26,704 |
| LVR | 43.7% |

*5 metrics in a horizontal strip — PropPath shows 3 (Portfolio Value, Total Equity, Annual Cashflow)*
*Roadmap Lite adds GROSS CF and LVR explicitly — worth considering*

### Charts
- **Asset Growth**: Stacked area chart, yellow = asset value, red = debt, steps up with each purchase
- **Cashflow Analysis**: Blue dotted = gross cashflow, green = net cashflow
- Both charts side by side (2-column layout)
- No break-even line shown — PropPath's cashflow bar chart with break-even IS BETTER

### Retirement Scenario
- Snapshot Time slider + Sell-off slider
- Shows: VALUE / DEBT / EQUITY / NET CASHFLOW / LIQUIDITY / SERVICEABILITY
- Same 6-metric grid as PropPath
- **Serviceability shown as $280,601** — this is the remaining serviceability buffer (good transparency)
- PropPath shows same metrics but labels it differently

---

## Key Gaps in Roadmap Lite vs PropPath

| Feature | Roadmap Lite | PropPath |
|---------|-------------|---------|
| Property type variety | Generic "Property 1-6" | Named types (Units, Houses, Duplexes, etc.) |
| Break-even visualisation | ❌ No | ✅ Yes (bar chart with line) |
| Scenario A vs B comparison | ❌ No | ✅ Yes |
| Events (income changes, life events) | ❌ No | ✅ Yes |
| Per-property performance modal | ❌ No | ✅ Yes (ROI, equity growth chart) |
| Cash-on-cash return | ❌ No | ✅ Yes |
| Tiered growth by property year | ❌ No (flat 15%/10%) | ✅ Yes |
| Next Buy Window callout | ❌ No | ❌ No (opportunity for both) |

## Where Roadmap Lite Beats PropPath

| Feature | Roadmap Lite | PropPath |
|---------|-------------|---------|
| DTI check (6x APRA) | ✅ Built-in, labelled | ❌ Missing |
| Borrowing power from income | ✅ Full serviceability model | ❌ Reverse repayment only |
| 20% LVR default | ✅ Sensible default | ❌ 88% LVR (12% deposit) is aggressive |
| "Plan Feasible" banner | ✅ Clear YES/NO | ❌ Guardrails buried |
| Gross CF shown separately | ✅ Yes | ❌ Only net shown |
| Interest rate | 5.9% | 6.5% (higher = more conservative ✅) |

---

## Numbers Audit: PropPath Red Items Confirmed Against Competitor

### 1. LVR Default
- Roadmap Lite: **20% deposit (80% LVR)**
- PropPath: **12% deposit (88% LVR)** ← needs changing to 80%

### 2. Vacancy Rate
- Roadmap Lite: **Not shown (0% assumed)**
- PropPath: **0% on most types** ← both wrong, but at least equal
- Industry standard: 2-4% depending on property type

### 3. DTI Check
- Roadmap Lite: **"Lower of Serviceability or 6x DTI"** — prominent
- PropPath: **No DTI check** ← red item, confirmed must fix

### 4. Growth Rate Sanity
- Roadmap Lite Moderate: 15%/10% (aggressive)
- PropPath High: 12.5%→6% (actually more conservative)
- PropPath is defensible here — but should label growth assumptions more visibly

---

## Product Strategy Notes

1. PropPath's output is actually richer and more nuanced than Roadmap Lite
2. Roadmap Lite's financial inputs are more rigorous (income-based serviceability)
3. PropPath wins on: visualisation, property variety, scenario comparison, events
4. Roadmap Lite wins on: financial rigor (DTI), simplicity of input, "Plan Feasible" clarity
5. The dark UI of Roadmap Lite doesn't look as client-presentable as PropPath's clean light design

**Bottom line: PropPath is better for presentation. Roadmap Lite is more financially rigorous. Fix the DTI + LVR gaps and PropPath is strictly superior.**
