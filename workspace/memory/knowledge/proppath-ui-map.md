# PropPath UI Map — Dashboard Screenshots
*Captured from Rob's screenshots — session Feb 2026*
*Maps every visible UI screen to its corresponding source code file*

---

## Screen 1: Client Details Card
**File:** `src/components/ClientDetailsCard.tsx`

### Layout: 3-column grid
**Column 1 — Investment Goals**
- Investment Horizon slider (12 years in screenshot)
- Equity Goal slider ($1.5M in screenshot)
- Cashflow Goal Annual slider ($50k in screenshot)

**Column 2 — Personal Details**
- Deposit Pool slider ($120k in screenshot)
- Borrowing Capacity slider ($900k in screenshot)
- Annual Savings slider ($24k in screenshot)

**Column 3 — Current Portfolio**
- Current Value slider ($1.0M in screenshot)
- Current Debt slider ($750k in screenshot)
- Use Existing Equity toggle (off in screenshot)
- Advanced Settings button → `AdvancedSettingsModal.tsx`

**Footer:** "Calculate Borrowing Capacity" button → opens `BorrowingCalculatorModal.tsx`

**Collapsed state shows:** "$120k deposit | $900k capacity | $24k/yr savings"

---

## Screen 2: Borrowing Calculator Modal
**File:** `src/components/BorrowingCalculatorModal.tsx`
**Calc logic:** `src/utils/calculateBorrowingCapacity.ts`

### Inputs (3-column grid)
- Affordable Repayment: $2,000 (required field)
- Repayment Frequency: Monthly (dropdown)
- Interest Rate: 6.04% (required field)
- Length of Loan: 25 years
- Fees: $10
- Fees Frequency: Monthly

### Output
- **Estimated Borrowing Capacity: $307,693** (large bold)
- Total Repayments: $600,000
- Total Interest: $289,307
- Total Fees: $3,000
- Disclaimer text below

### ⚠️ Known Issues
- Uses PV formula reversed from repayment — not income-based serviceability
- No APRA 3% buffer applied
- No DTI (6x) cap
- Result is standalone — doesn't feed back into main dashboard borrowing capacity

---

## Screen 3: Investment Timeline — Wealth View
**File:** `src/components/InvestmentTimeline.tsx`

### KPI Header Strip (3 metrics)
- Portfolio Value: $2.8M (current year = Year 12)
- Total Equity: $1.5M / $1.5M (goal shown)
- Annual Cashflow: $27.2k / $50k (goal shown, green when positive)

### Chart (Wealth tab)
- Area chart: green fill = equity, lighter grey = debt/value
- Property icons pinned to purchase years (2025 Apt, 2027 Apt)
- X-axis: 2025–2036

### Data Table (below chart, collapsible)
| Row | Description |
|-----|-------------|
| BUY | Purchase year markers (Apt icons) |
| AVAIL | Available funds each year ($120k → $934k) |
| LVR | Portfolio LVR declining (78% → 48%) |
| DEBT | Total debt flat at $1M |
| SERVICE | Annual loan repayments ($51k → $118k) |

---

## Screen 4: Investment Timeline — Cashflow View
**File:** `src/components/InvestmentTimeline.tsx` (same component, tab toggle)

### Chart (Cashflow tab)
- Bar chart: red bars = negative cashflow years, green bars = positive
- Break-even dotted line labelled
- Turns positive ~2032 in screenshot

### Data Table (below chart)
| Row | Description |
|-----|-------------|
| BUY | Purchase year markers |
| INCOME | Rental income ($64.5k → $157.2k) |
| EXPEN | Expenses ($20.3k → $41.2k) |
| LOANS | Loan repayments ($68.8k flat) |
| NET | Net cashflow (-$24.6k → +$27.2k) |

---

## Screen 5: Scenario A vs B Comparison
**File:** `src/components/Dashboard.tsx` (scenario container)
**Add button:** `src/components/AddScenarioButton.tsx`

- Scenario A: Active (shown with timeline, data)
- Scenario B: Empty state (Year 15, $0 everything — no properties added yet)
- Each scenario has its own Investment Timeline component
- "Add a second scenario to compare strategies" button at bottom

---

## Screen 6: Retirement Scenario
**File:** `src/components/RetirementSnapshot.tsx`

### Controls
- Snapshot Time slider: 10 years (top right shows "10y 0m | 0% sell-off | $1.4M equity")
- Sell-Off Portfolio slider: 0%

### Portfolio Snapshot (6-metric grid)
| Metric | Value | Colour |
|--------|-------|--------|
| VALUE | $2.7M | White |
| DEBT | $1.4M | Red |
| EQUITY | $1.4M | Green |
| CASHFLOW | $21k | Green |
| LIQUIDITY | $0 | Yellow |
| SERVICE | $106k | Green |

---

## Screen 7: Property Timeline Panel (Left Rail)
**File:** `src/components/PropertyBlocksPanel.tsx`

### Layout
- "Add to Timeline" button with count badge (2 in screenshot)
- Properties grouped by year
- Each property card shows: type icon, name (truncated), price
- Expandable: tabs for PROPERTY / LOAN / ASSUMPTIONS / COSTS

### Expanded Property Card (Units/Apartments, 2025)
- Purchase Price slider: $350k
- Valuation at Purchase: $350k
- Weekly Rent: $471
- Deposit: 12.0% ← **88% LVR confirmed here**
- State: VIC dropdown

---

## Screen 8: Add to Timeline Modal — Properties Tab
**File:** `src/components/AddToTimelineModal.tsx`

### Property Templates (with displayed prices)
| Type | Display Price | Yield | State |
|------|--------------|-------|-------|
| Units / Apartments | $400,000 | 6.1% | Victoria |
| Villas / Townhouses | $500,000 | 4.6% | Queensland |
| Houses (Regional) | $450,000 | 5.4% | NSW |
| Duplexes | $550,000 | 7.0% | Queensland |
| Small Blocks (3-4 Units) | $700,000 | 5.5% | NSW |
| Metro Houses | $650,000 | 5.4% | Victoria |
| Larger Blocks (10-20 Units) | $3,500,000 | 7.0% | NSW |

**⚠️ Note:** Display prices in modal differ from `property-defaults.json`:
- Units/Apartments: Modal shows $400k, JSON has $350k
- These template display prices likely come from a separate constants file (not yet located)

### Also on this tab
- "+ Add Custom Property" at top → opens `CustomBlockModal.tsx`
- Each card: property image, name, price, yield, state badge, +/- buttons, count badge

---

## Screen 9: Add to Timeline Modal — Events Tab
**File:** `src/components/AddToTimelineModal.tsx` (Events tab)
**Event types:** `src/constants/eventTypes.ts`

### Event Categories
| Category | Subcategories |
|----------|---------------|
| Income Changes | Salary · Partner · Bonus |
| Portfolio Changes | Sell · Refinance · Renovate |
| Life Events | Inheritance · Expense · Dependent |
| Market Events | Rates · Correction |

---

## Screen 10: Custom Property Block Modal
**File:** `src/components/CustomBlockModal.tsx`

### Sections (collapsible)
1. **Property Overview** (expanded by default)
   - State: VIC
   - Growth Assumption: High
   - Purchase Price: $350,000
   - Valuation at Purchase: $378,000
   - Rent/Week: $471
   - Yield: 7%
   - Growth Rate: 5%
   - Minimum Yield: 6.5%

2. **Contract & Loan Details** (collapsed)
3. **One-Off Purchase Costs** (collapsed)
4. **Annual Cashflow Expenses** (collapsed)

### Summary Preview (bottom)
- Purchase Price: $350,000 | Loan Amount: $308,000
- Deposit Required: $42,000 | Annual Rental Income: $24,492
- Total One-Off Costs: $21,450 | Annual Expenses: $8,916

**⚠️ Note:** Loan = $308,000 on $350k purchase = 88% LVR confirmed

---

## Screen 11: Property Performance Modal (Per-Property)
**File:** `src/components/PropertyDetailModal.tsx`

### Header KPIs (6 cards)
| Metric | Value |
|--------|-------|
| Value at Year 12 | $816K |
| Equity | $508K |
| Projection | 12 Years |
| Cash Invested | $121K |
| ROI (Annualised) | 35.0% |
| Cash-on-Cash | -1.1% |

### Charts
1. **Equity Growth Over Time**: 3-line chart (Value, Equity, Loan Balance)
2. **Property Cashflow Analysis**: Multi-bar chart (Rental Income, Expenses, Loan Interest, Net Cashflow)

---

## Key Data Flow Summary

```
ClientDetailsCard (profile inputs)
  → useInvestmentProfile hook
  → InvestmentTimeline (calculations)
  → RetirementSnapshot (portfolio snapshot)
  → guardrailValidator (3 tests: deposit/borrowing/serviceability)

PropertyBlocksPanel (property selection)
  → property-defaults.json (default values)
  → PropertyDetailModal (per-property editing)
  → CustomBlockModal (custom properties)

AddToTimelineModal
  → PropertySelectionContext (state management)
  → EventConfigModal (event configuration)
```

---

## Files Not Yet Mapped
- `src/hooks/useAffordabilityCalculator.ts` — drives AVAIL row calculations
- `src/hooks/useRoadmapData.ts` — drives retirement scenario
- `src/hooks/useChartDataGenerator.ts` — drives chart data
- `src/constants/financialParams.ts` — SERVICEABILITY_FACTOR and other constants
- Template display prices source (separate from property-defaults.json)
