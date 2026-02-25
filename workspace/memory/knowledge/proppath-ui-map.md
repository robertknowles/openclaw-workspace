# PropPath UI → Code Map
*Written: Post frontend screenshot tour*

This document maps every visible screen/component from the dashboard screenshots to its source file and key data fields. Use this before making any code changes.

---

## Screen 1 — Client Details Card
**Screenshot:** Bottom panel with 3-column slider layout  
**Component:** `src/components/ClientDetailsCard.tsx`  
**Hook:** `src/hooks/useInvestmentProfile.ts`

### What the BA sees:
| Column | Fields |
|--------|--------|
| Investment Goals | Investment Horizon (12 years), Equity Goal ($1.5M), Cashflow Goal (Annual) ($50k) |
| Personal Details | Deposit Pool ($120k), Borrowing Capacity ($900k), Annual Savings ($24k) |
| Current Portfolio | Current Value ($1.0M), Current Debt ($750k), Use Existing Equity toggle |

**Collapsed header shows:** `$120k deposit | $900k capacity | $24k/yr savings`  
**Advanced Settings** → opens `AdvancedSettingsModal.tsx`  
**Calculate Borrowing Capacity** → opens `BorrowingCalculatorModal.tsx`

### Key audit note:
- Borrowing Capacity ($900k) is **manually entered by the BA** — it is NOT calculated automatically
- The Borrowing Calculator is a standalone helper tool; its result does NOT auto-populate the Borrowing Capacity slider
- **RED ISSUE: No APRA 3% buffer, no DTI check** happens here

---

## Screen 2 — Borrowing Calculator Modal
**Screenshot:** "How much can I borrow?" popup  
**Component:** `src/components/BorrowingCalculatorModal.tsx`  
**Utility:** `src/utils/calculateBorrowingCapacity.ts`

### What the BA sees:
- Inputs: Affordable Repayment ($2,000), Repayment Frequency (Monthly), Interest Rate (6.04%)
- Inputs: Length of Loan (25 years), Fees ($10), Fees Frequency (Monthly)
- Output: **Estimated Borrowing Capacity = $307,693**
- Breakdown: Total Repayments $600k, Total Interest $289k, Total Fees $3k
- Disclaimer: "estimates only..."

### Key audit note:
- This is an **informational calculator only** — result is NOT fed back to the profile
- No APRA 3% serviceability buffer applied (should be: rate used = 6.04% + 3% = 9.04%)
- **RED ISSUE:** With buffer, result would be ~$230k not $307k — potentially misleading

---

## Screen 3 — Investment Timeline (Wealth view)
**Screenshot:** Main chart area, "Wealth" tab selected  
**Component:** `src/components/InvestmentTimeline.tsx`  
**Chart sub-component:** `src/components/PortfolioGrowthChart.tsx` (likely)

### What the BA sees:
- **KPI bar:** Projection Summary Year 12 | Portfolio Value $2.8M | Total Equity $1.5M/$1.5M ✅ | Annual Cashflow $27.2k/$50k
- **Chart:** Area chart with green fill (wealth curve), darker line (equity), from 2025–2036
- **Property pins:** Avatar icons at 2025 and 2027 (Apt purchase years)
- **Wealth/Cashflow toggle:** Two tabs, currently on Wealth
- **Data table below chart:**
  - BUY: Apt (2025), Apt (2027)
  - AVAIL (available funds): $120k → grows to $934k by 2036
  - LVR: 78% → drops to 48% by 2036
  - DEBT: $1M flat across all years
  - SERVICE: $51k (2025) → $118k (2036)

### Key mapping:
- `AVAIL` row = deposit pool + savings accumulation − purchases used
- `SERVICE` row = annual loan repayments
- Property icons are rendered from `PurchaseEventCard.tsx`
- Timeline progress bar in `InvestmentTimeline.tsx` → `TimelineProgressBar` component

---

## Screen 4 — Investment Timeline (Cashflow view)
**Screenshot:** Same chart, "Cashflow" tab selected  
**Component:** `src/components/InvestmentTimeline.tsx` + `src/components/CashflowChart.tsx`

### What the BA sees:
- Bar chart: Red bars (negative cashflow) 2025–2032, green bars (positive) 2033–2036
- "Break-even" dashed line at $0
- **Data table:**
  - INCOME: $64.5k (2025) → $157k (2036) — rental income
  - EXPEN: $20.3k (2025) → $41.2k (2036) — expenses
  - LOANS: $68.8k flat — interest/repayments
  - NET: -$24.6k (2025) → +$27.2k (2036)

### Key audit note:
- **INCOME growing from $64.5k in 2025 on a $350k apartment** looks very high
- $350k × 6.1% yield = $21.4k/year… but $64.5k suggests existing portfolio income included
- Existing portfolio: $1M value, $750k debt — the BA's existing properties contribute income here
- This is correct architecture — existing portfolio IS included in cashflow

---

## Screen 5 — Scenario Comparison (A vs B)
**Screenshot:** Scenario A (active) + Scenario B side by side  
**Component:** `src/components/Dashboard.tsx` + scenario management logic  
**Button:** `src/components/AddScenarioButton.tsx`

### What the BA sees:
- **Scenario A (Active):** Same as above — 2 apartments, $2.8M portfolio, $1.5M equity, $27.2k cashflow at Year 12
- **Scenario B (empty):** No properties added yet — all $0, "Year 15" projection, flat $50k/yr "available" line only
- Scenario B shows AVAIL growing from $50k → $134k (this is just the annual savings accumulating without any purchases)

### Key mapping:
- `+ Add a second scenario` button opens a new blank scenario panel
- Scenarios are independently calculated — same client profile, different property timelines

---

## Screen 6 — Retirement Scenario
**Screenshot:** Collapsible panel at bottom  
**Component:** `src/components/RetirementSnapshot.tsx`

### What the BA sees:
- Collapsed header: `10y 0m | 0% sell-off | $1.4M equity`
- **Snapshot Time slider:** 10 years (the point in time to snapshot the portfolio)
- **Sell-Off Portfolio slider:** 0% (what % of portfolio to sell to pay down debt)
- **Portfolio Snapshot table:**
  - VALUE: $2.7M
  - DEBT: $1.4M (red)
  - EQUITY: $1.4M (green)
  - CASHFLOW: $21k (green)
  - LIQUIDITY: $0 (yellow — no cash from sell-off since 0%)
  - SERVICE: $106k (green — annual loan repayments)

### Key mapping:
- Two sliders drive the retirement scenario
- Sell-off % reduces debt and boosts liquidity but reduces income
- This IS the sell-down retirement feature confirmed ✅

---

## Screen 7 — Per-Property Detail Modal
**Screenshot:** "Units / Apartments · 2025 H1" popup  
**Component:** `src/components/PropertyDetailModal.tsx` (read-only view)  
**Also:** `src/components/PerPropertyTracking.tsx`

### What the BA sees:
- **Top KPI cards:** Value at Year 12 = $816K | Equity = $508K | Projection = 12 Years
- **Second row:** Cash Invested = $121K | ROI (Annualized) = 35.0% | Cash-on-Cash = -1.1%
- **Equity Growth Over Time chart:** Blue line (value), green line (equity), red dashed (loan balance)
- Tooltip: "Expenses shown include 3% annual inflation adjustment. Year 1 values match your inputs..."
- **Property Cashflow Analysis bar chart:** Rental Income (green), Expenses (yellow), Loan Interest (pink), Net Cashflow (teal)

### Key mapping:
- This is the per-property drill-down
- "H1" suffix = first half of year (likely purchase timing)
- Cash-on-Cash = -1.1% confirms slightly negative early cashflow (consistent with NET row in timeline)

---

## Screen 8 — Property Timeline (Left Rail)
**Screenshot:** Collapsible left panel showing property list by year  
**Component:** `src/components/PropertyBlocksPanel.tsx`

### What the BA sees:
- **"+ Add to Timeline 2"** button (2 properties currently in timeline)
- **2025** — Units / Apartments, $350k (expanded, 4 sub-tabs: PROPERTY | LOAN | ASSUMPTIONS | COSTS)
  - PROPERTY tab: Purchase Price $350k, Valuation at Purchase $350k, Weekly Rent $471, Deposit 12.0%, State VIC
- **2027** — Units / Apartments, $350k (collapsed)

### Key mapping:
- Property cards → `PropertyBlockCard` / `PropertyBlockCardV2` within `PropertyBlocksPanel.tsx`
- The 4-tab detail edit → `PropertyDetailModal.tsx` (inline edit, not a popup here)
- Purchase Price slider, Valuation, Weekly Rent, Deposit %, State dropdown are all live-edit
- **LOAN tab** → `interestRate`, `lvr`, `loanProduct` (IO/PI), `loanTerm`
- **ASSUMPTIONS tab** → `growthAssumption`, `minimumYield`, growth rates
- **COSTS tab** → all one-off purchase costs

### Key audit note:
- **Deposit shows 12.0%** — this is LVR-derived (100% - 88% LVR = 12%)
- **RED ISSUE:** Default LVR = 88% should be 80% → deposit would show 20%

---

## Screen 9 — Add to Timeline Modal (Properties tab)
**Screenshot:** Property template picker  
**Component:** `src/components/AddToTimelineModal.tsx`

### What the BA sees:
**Property Templates:**
| Template | Price | Yield | State |
|----------|-------|-------|-------|
| Units / Apartments | $400,000 | 6.1% | Victoria |
| Villas / Townhouses | $500,000 | 4.6% | Queensland |
| Houses (Regional) | $450,000 | 5.4% | New South Wales |
| Duplexes | $550,000 | 7.0% | Queensland |
| Small Blocks (3-4 Units) | $700,000 | 5.5% | New South Wales |
| Metro Houses | $650,000 | 5.4% | Victoria |
| Larger Blocks (10-20 Units) | $3,500,000 | 7.0% | New South Wales |

- `+ Add Custom Property` → opens `CustomBlockModal.tsx`
- Each template: `−` / `+` buttons, "Duplicate" link
- Counter badge "2 added" on Units / Apartments (currently selected)

### Key audit note:
- **Units/Apartments default = $400k, 6.1% yield** (in this modal) but **custom block defaults to $350k, 7% yield**
- These are DIFFERENT default values — the template price ($400k) vs custom block price ($350k)
- **YELLOW ISSUE:** Prices are 12-18 months stale; should update to 2025 market rates
- Template data source → `DataAssumptionsContext.tsx` (likely `src/contexts/DataAssumptionsContext.tsx`)

---

## Screen 10 — Add to Timeline Modal (Events tab)
**Screenshot:** Life events picker  
**Component:** `src/components/AddToTimelineModal.tsx` (Events tab)  
**Constants:** `src/constants/eventTypes.ts`

### What the BA sees:
**ADD LIFE EVENTS THAT AFFECT YOUR INVESTMENT TIMELINE:**
| Category | Description | Sub-types |
|----------|-------------|-----------|
| Income Changes | Salary increases, partner income, bonuses | Salary · Partner · Bonus |
| Portfolio Changes | Sell, refinance, or renovate properties | Sell · Refinance · Renovate |
| Life Events | Inheritance, major expenses, family changes | Inheritance · Expense · Dependent |
| Market Events | Interest rate changes, market corrections | Rates · Correction |

### Key mapping:
- Each row → `EventCategoryButton` component → opens `EventConfigModal.tsx`
- Events appear as blocks on the timeline alongside property purchases

---

## Screen 11 — Create Custom Property Block Modal
**Screenshot:** Custom property creator  
**Component:** `src/components/CustomBlockModal.tsx`

### What the BA sees:
- **Property Name** text input
- **Property Overview** section (expanded):
  - State (VIC), Growth Assumption (High)
  - Purchase Price ($350,000), Valuation at Purchase ($378,000)
  - Rent/Week ($471), Yield (7%), Growth Rate (5%)
  - Minimum Yield (6.5%)
- **Contract & Loan Details** (collapsed)
- **One-Off Purchase Costs** (collapsed)
- **Annual Cashflow Expenses** (collapsed)
- **Summary Preview** (always visible):
  - Purchase Price: $350,000 | Loan Amount: $308,000
  - Deposit Required: $42,000 | Annual Rental Income: $24,492
  - Total One-Off Costs: $21,450 | Annual Expenses: $8,916

### Key audit notes:
- Loan Amount = $308k → $350k × 88% LVR = $308k ✅ confirms 88% LVR default
- Deposit = $42k → 12% of $350k ✅
- **RED ISSUE:** LVR default = 88% (should be 80%)
- Growth Assumption defaults to **"High"** for custom blocks
- **YELLOW ISSUE:** Units/Commercial should default to Medium, not High
- vacancyRate defaults to **0%** in `getDefaultFormData()` — confirmed in code
- **RED ISSUE:** Vacancy = 0% overstates rental income

---

## Summary: UI → Audit Issue Mapping

| Red Issue | Where it appears in UI | Code location |
|-----------|----------------------|---------------|
| Vacancy rate = 0% | Custom block → Annual Cashflow Expenses | `CustomBlockModal.tsx` → `getDefaultFormData()` + `property-defaults.json` |
| APRA 3% buffer missing | Borrowing Calculator result ($307k) | `calculateBorrowingCapacity.ts` |
| Borrowing capacity stub | BA manually enters $900k, no auto-recalc as properties added | `metricsCalculator.ts` → `calculateUpdatedBorrowingCapacity` |
| DTI not modelled | No DTI check anywhere in the UI | `guardrailValidator.ts` |

| Yellow Issue | Where it appears in UI | Code location |
|-----------|----------------------|---------------|
| LVR default 88% (should 80%) | Property block shows "Deposit 12%", Summary shows $308k loan | `CustomBlockModal.tsx` → `getDefaultFormData()` + templates |
| Units/Commercial → High growth | Custom block Growth Assumption defaults to "High" | `CustomBlockModal.tsx` → `getDefaultFormData()` |
| Stale purchase prices | Add to Timeline modal — all template prices | `DataAssumptionsContext.tsx` or `property-defaults.json` |

---

## Key Architecture Understanding

1. **The BA manually sets Borrowing Capacity** — it's a slider, not auto-calculated. The Borrowing Calculator popup is informational only and doesn't write back to the profile.

2. **Existing portfolio IS included in cashflow** — The client's $1M / $750k debt portfolio contributes to the INCOME and LOANS rows from day 1.

3. **Scenarios are fully independent** — Same client profile, different property timelines. Scenario B starts blank.

4. **Property blocks have rich per-instance data** — 4 tabs (Property, Loan, Assumptions, Costs) each feeding `PropertyInstanceDetails` type.

5. **Growth curve is tiered** — Y1 → Y2-3 → Y4 → Y5+ rates, not a single flat rate. Displayed in `PropertyBlocksPanel` growth rate string.

6. **Events system is built** — Income, Portfolio, Life, Market events can all be added to the timeline alongside property purchases.
