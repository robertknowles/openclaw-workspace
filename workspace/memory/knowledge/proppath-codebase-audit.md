# PropPath Codebase Audit
*Prepared by Bertie | February 2026*
*Scope: Validate what's built before BA rollout. Not a feature gap analysis — a validation of what exists.*

---

## Executive Summary

The core simulation engine is **more sophisticated than average** for a product at this stage. The incremental cascade model is correctly implemented. The three guardrail tests exist and fire correctly. The main risks are: (1) growth assumptions that will raise eyebrows with sophisticated BAs, (2) a serviceability test that is real but simplified, and (3) purchase price defaults that are stale for the markets BAs actually buy in. These are fixable before rollout.

---

## Audit 1 — Default Property Metrics vs Industry Reality

### 1A. Growth Assumptions

**What's built:**
All 8 property types default to `"High"` growth assumption.

```
High: Year 1 = 12.5%, Years 2–3 = 10%, Year 4 = 7.5%, Year 5+ = 6%
Medium: Year 1 = 8%, Years 2–3 = 6%, Year 4 = 5%, Year 5+ = 4%
Low: Year 1 = 5%, Years 2–3 = 4%, Year 4 = 3%, Year 5+ = 2.5%
```

**Industry reality:**
- Long-term Australian capital city average: **6.8–7.4% p.a.** (30-year historical, PropertyUpdate/Propertyology)
- InvestorKit uses **market-specific projections**, not flat-rate assumptions — they model by suburb, not property type
- APS/School of Property teaches clients to expect **6–8% long-term** for well-selected properties
- The `High` Year 1 figure of **12.5%** is not indefensible (2021–23 saw 20–30% in some markets), but it's optimistic as a *default*

**Verdict by property type:**

| Property Type | Current Default | Recommended Default | Reason |
|---|---|---|---|
| Units/Apartments | High | **Medium** | Units historically underperform houses; strata drag; oversupply risk |
| Villas/Townhouses | High | **High** | Defensible — land content, scarcity |
| Houses Regional | High | **High** | Defensible if BA-selected markets |
| Duplexes | High | **High** | Land content + dual income |
| Small Blocks (3–4 units) | High | **Medium** | Commercial lending, lower liquidity |
| Metro Houses | High | **High** | Core BA buy — land appreciates |
| Larger Blocks (10–20 units) | High | **Medium** | Commercial asset class, different dynamics |
| Commercial | High | **Low–Medium** | Cap rate compression ≠ residential growth; 7.5% is aggressive for commercial |

**What Sam Gordon or Arjun Paliwal would say:**
- "Why are units on High growth? That's not how we think about them."
- "12.5% Year 1 is possible but it's not a default — it's a best case."
- "Your long-run 6% for Year 5+ is actually the right number — that's the industry consensus."

**Recommendation:** Change Units, Small Blocks, Larger Blocks, and Commercial to `Medium` as default. BAs can upgrade to `High` for individual properties. This is a 4-line change in `property-defaults.json`.

---

### 1B. Purchase Prices

**What's built (current defaults):**

| Property Type | Default Price | State |
|---|---|---|
| Units/Apartments | $350,000 | VIC |
| Villas/Townhouses | $325,000 | QLD |
| Houses Regional | $350,000 | NSW |
| Duplexes | $550,000 | QLD |
| Small Blocks | $900,000 | NSW |
| Metro Houses | $800,000 | VIC |
| Larger Blocks | $3,500,000 | NSW |
| Commercial | $3,000,000 | VIC |

**Reality check:**
- $350k units (VIC): Possible in outer suburbs/regional VIC but most IK/APS clients buy in **$450–600k** range for quality stock
- $325k villas (QLD): **Stale** — Brisbane units/townhouses are now $500k+ in BA-targeted submarkets
- $350k regional houses: Plausible for Ballarat, Bendigo, Toowoomba — still defensible
- $800k metro houses (VIC): Reasonable for Melbourne middle ring
- $550k duplexes (QLD): **Low** — QLD duplex stock runs $650k–$900k now

**Verdict:** Prices are 12–18 months behind market. For a BA demo, a sophisticated BA will immediately notice if their typical buy ($550k QLD unit) doesn't match the template. Recommend updating to 2025 market medians, or framing clearly as "editable defaults, not recommendations."

---

### 1C. Rental Yields

**What's built:**
- Most types default to `minimumYield: 6.5%` — this is a *required* yield, not the actual yield
- Actual rent: Units $471/wk on $350k purchase = **7.0% gross** (imputed)
- Metro Houses: $615/wk on $800k = **4.0% gross**
- Commercial: $4,615/wk on $3M = **8.0% gross**

**Industry reality (Q3 2025):**
- National average gross yield: **4.92%**
- Sydney houses: **~3.0%**
- Darwin units (best in country): **~7.8%**
- Regional/affordable markets: **5–6%**
- Commercial: **6–8%** — the $3M commercial default is in range

**Verdict:**
- The 6.5% `minimumYield` filter is actually a BA-facing tool to screen for cashflow properties — this is **correct and intentional**, BAs use this
- The *imputed* yields from price/rent defaults are reasonable for the types they represent (regional/affordable stock)
- Metro Houses at 4.0% gross is realistic for Melbourne
- ✅ Yields are defensible as-is — but the framing matters: BAs need to know these are *target market* yields, not Sydney/Melbourne generic

---

### 1D. LVR — 88% on Most Residential

**What's built:** `lvr: 88` across Units, Townhouses, Regional Houses, Duplexes, Metro Houses.

**Industry reality:**
- 88% LVR = 12% deposit + LMI
- This is **unusual for investment loans** — most investors use either:
  - **80% LVR** (no LMI, clean)
  - **90% LVR** (maximise leverage, accept LMI)
  - 88% is an odd middle ground — some lenders do 88% with reduced LMI tiers
- For investors building a portfolio, **most BAs recommend 80% LVR** to avoid LMI drag and maintain bank appetite for subsequent loans
- IK and APS clients typically target 80% as the portfolio scales

**Verdict:** ⚠️ 88% as the universal default will confuse sophisticated BAs. Most would expect to see **80% as default** with 88–90% as an option for property 1 (before portfolio constraints kick in). Consider making this configurable per-property and changing the default to 80% for properties 3+.

---

## Audit 2 — Client-Facing Output: What's There

**What's built (from `client-view/` and `strategyAnalyzer.ts`):**

### What exists:
1. ✅ **Portfolio growth chart** — value over time
2. ✅ **Cashflow chart** — net cashflow projection
3. ✅ **Goal achievement cards** — equity goal vs cashflow goal with projected year
4. ✅ **Strategy narrative** — auto-generated text (Growth-Funded Income Transition, Pure Wealth Accumulation, etc.)
5. ✅ **Property timeline** — sequential purchases with period labels
6. ✅ **Milestone tracker** — key portfolio events
7. ✅ **At-a-Glance page** — KPI summary cards
8. ✅ **Comparison KPI cards** — side-by-side scenario view
9. ✅ **Tabbed timeline** — BA + client views
10. ✅ **Strategy pathway page** — narrative + bullets per asset class

### What would make a sophisticated BA trust this output:
- ✅ The strategy narrative is smart — detecting "Serviceability Valve" and "Commercial Injection" is genuine BA-level thinking
- ✅ The tiered growth curve is more honest than flat-rate tools
- ✅ Dual BA/client portal separation is a legitimate differentiator
- ✅ The guardrail tests (deposit/borrowing/serviceability) before each purchase are the right architecture

### What would make a sophisticated BA uncomfortable:
- ⚠️ **No DSR (Debt Service Ratio) displayed** — IK and most sophisticated BAs track DSR throughout the portfolio journey. It's calculated in the data model (`dsr` field exists in `YearBreakdownData`) but unclear if it surfaces in the report
- ⚠️ **Vacancy rate defaults to 0%** on Units, Townhouses, Duplexes — industry standard is **1–4%** minimum. A BA reviewing this will see "0% vacancy" and distrust the cashflow projections
- ⚠️ **No depreciation / tax benefit modelling** — `potentialDeductionsRebates: 0` on all defaults. IK clients routinely factor in depreciation schedules. This isn't a dealbreaker but a BA will ask "where's the tax benefit?"
- ⚠️ **Existing portfolio growth rate hardcoded at 3%** — `DEFAULT_EXISTING_PORTFOLIO_GROWTH_RATE = 0.03`. This is conservative but it's a TODO comment in the code, suggesting it's unfinished. 3% is below inflation — it undersells the portfolio value for existing property holders.
- ⚠️ **`strategyAnalyzer.ts` uses a flat 80% LVR** for equity calculations — but the rest of the system uses per-property LVR. These two systems are inconsistent.

---

## Audit 3 — The Three System Tests: Are They Accurate?

### Test 1: Deposit Test ✅ Solid

**What it does:** Checks `availableFunds >= totalCashRequired` (deposit + acquisition costs)

**Is it accurate?**
- ✅ Acquisition costs are calculated properly via `costsCalculator` (stamp duty, LMI, legal, inspection, conveyancing)
- ✅ Stamp duty is state-specific with real bracket rates for all 8 states/territories
- ✅ LMI is calculated with the correct "lower of purchase price or valuation" logic — this is a subtle but accurate detail
- ✅ Funding breakdown correctly tracks cash, savings, and equity components
- ✅ The cascade model (available funds update after each purchase) is architecturally correct

**One issue:** `vacancyRate: 0` on most property types feeds into cashflow reinvestment projections. Because vacancy isn't modelled, available funds will be slightly overstated across a long timeline.

---

### Test 2: Borrowing Capacity Test ⚠️ Simplified but Present

**What it does:** Checks remaining borrowing capacity against the new loan required.

**Is it accurate?**
- ✅ The PV formula in `calculateBorrowingCapacity.ts` is correctly reverse-engineered from MoneySmart
- ✅ Supports weekly/fortnightly/monthly frequency
- ⚠️ **The APRA 3% serviceability buffer is NOT applied in the borrowing capacity calculation** — APRA requires lenders to assess at rate + 3%. At 6.5%, that means testing at 9.5%. This is a real gap: the system will allow purchases that a real bank would reject.
- ⚠️ **`calculateUpdatedBorrowingCapacity` is a stub** — the code has a comment: *"Simplified logic: just return the base capacity for now"*. This means borrowing capacity does NOT decrease as new loans are added to the portfolio over time. In reality, each new loan reduces future capacity. The system is overestimating how much a client can borrow for properties 3, 4, 5+.
- ⚠️ **Rental income contribution**: Banks typically shade 70–80% of rental income when assessing serviceability. There's a `rentalRecognitionRate` field in the data model (and a `0.7` factor referenced in `calculateBorrowingCapacityProgression`) but it's not consistently applied in the core test.

---

### Test 3: Serviceability Test ⚠️ Present but Light

**What it does:** Checks `serviceabilityTestSurplus >= 0` before allowing a purchase.

**Is it accurate?**
- ✅ The test fires and blocks or warns correctly (errors vs warnings based on shortfall threshold)
- ✅ Warning vs error logic is sensible — small shortfalls warn, large shortfalls block
- ⚠️ **The actual serviceability calculation is not fully visible in these files** — it's computed upstream in `useAffordabilityCalculator` (not audited). The guardrail validator consumes the result but doesn't own the logic.
- ⚠️ **DTI (Debt-to-Income ratio)** is not part of the serviceability test. APRA is actively moving toward DTI limits. A 7× DTI portfolio would pass PropPath's serviceability test but face real-world bank rejection.
- ⚠️ The serviceability test uses `shortfall > (property.cost * 0.02)` to escalate from warning to error — this threshold is arbitrary and not grounded in lending policy.

---

## Summary: Risks Before BA Rollout

### 🔴 Must Fix (will undermine BA trust)
1. **Vacancy rate at 0%** on most types — set to minimum 2% across the board
2. **APRA 3% buffer not applied** in borrowing capacity test — system will approve purchases a real bank would reject
3. **Borrowing capacity stub** (`calculateUpdatedBorrowingCapacity` returns base capacity unchanged) — portfolio capacity doesn't shrink as loans accumulate. This means properties 4–6 may show as "feasible" when they aren't.

### 🟡 Should Fix Before Serious Demo (will cause BA questions)
4. **Units/Commercial defaulting to High growth** — change to Medium
5. **Purchase prices ~12 months stale** — update or add a "prices are indicative" disclaimer
6. **88% LVR default** — change to 80% or make it clearly editable per property
7. **Existing portfolio growth at 3%** — raise to 5–6% or make configurable

### 🟢 Good As-Is (or acceptable for V1)
8. Stamp duty calculations — correct bracket rates for all states
9. LMI calculation — correctly uses lower of purchase price/valuation
10. Tiered growth curve architecture — better than competitors
11. Strategy narrative generation — "Serviceability Valve" and injection detection is genuinely smart
12. Cascade model architecture — sound incremental design
13. Land tax calculations — present for all states

---

## Files Audited
- `src/types/property.ts`
- `src/data/property-defaults.json`
- `src/utils/propertyInstanceDefaults.ts`
- `src/utils/cascadeCalculator.ts`
- `src/utils/calculateBorrowingCapacity.ts`
- `src/utils/metricsCalculator.ts`
- `src/utils/feasibilityChecker.ts`
- `src/utils/guardrailValidator.ts`
- `src/utils/detailedCashflowCalculator.ts`
- `src/utils/stampDutyCalculator.ts`
- `src/utils/lmiCalculator.ts`
- `src/utils/landTaxCalculator.ts`
- `src/client-view/utils/strategyAnalyzer.ts`
