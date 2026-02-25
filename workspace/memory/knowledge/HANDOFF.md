# HANDOFF.md — Session State Save
*Saved: Session ending after UI audit + competitive research*

---

## Status: Research Phase Complete ✅ | No Code Changes Made

---

## What Was Completed This Session

### 1. PropPath Dashboard — Full UI Map
- **12 screenshots** reviewed from Rob (8 dashboard + 4 property timeline)
- Every screen mapped to its source code file
- File: `memory/knowledge/proppath-ui-map.md`
- Screenshots saved: `memory/screenshots/proppath-dashboard/` (01–12)

### 2. Roadmap Lite — Competitive Analysis
- **6 screenshots** reviewed from Rob
- Full breakdown of competitor metrics, defaults, and gaps
- File: `memory/knowledge/roadmap-lite-competitive-analysis.md`
- Screenshots saved: `memory/screenshots/roadmap-lite/` (01–06)

### 3. Codebase Files Read This Session
| File | Purpose |
|------|---------|
| `src/components/ClientDetailsCard.tsx` | Client inputs panel |
| `src/components/BorrowingCalculatorModal.tsx` | Borrowing calculator modal |
| `src/components/InvestmentTimeline.tsx` | Main timeline + charts |
| `src/components/RetirementSnapshot.tsx` | Retirement scenario sliders |
| `src/components/PropertyBlocksPanel.tsx` | Left rail property cards |
| `src/components/AddToTimelineModal.tsx` | Add property/event modal |
| `src/components/CustomBlockModal.tsx` | Custom property creation |
| `src/components/PropertyDetailModal.tsx` | Per-property performance modal |
| `src/utils/guardrailValidator.ts` | 3 guardrail tests (deposit/borrowing/serviceability) |
| `src/utils/calculateBorrowingCapacity.ts` | Borrowing capacity formula |
| `src/utils/metricsCalculator.ts` | Growth + portfolio calculations |
| `src/data/property-defaults.json` | All property type defaults |

---

## Key Research Findings

### PropPath vs Roadmap Lite — Where PropPath Wins
- Scenario A vs B comparison (Roadmap Lite has nothing)
- Break-even line on cashflow chart (RL doesn't have it)
- Property type variety + per-property performance modal
- Events system (income, life, market events)
- Overall presentation quality — better for client-facing use
- More conservative growth assumptions (actually more defensible)

### Where Roadmap Lite Beats PropPath (Gaps to Fix)
1. **DTI cap** — RL labels "lower of Serviceability or 6x DTI" prominently. PropPath has no DTI check.
2. **LVR default** — RL uses 20% deposit (80% LVR). PropPath uses 12% deposit (88% LVR).
3. **Borrowing capacity model** — RL calculates from income/expenses/dependents. PropPath reverses from repayment amount only.
4. **"Plan Feasible" banner** — RL has clear ✅/❌ at top of dashboard. PropPath's guardrails are buried.
5. **Vacancy rate** — Both are 0% (both wrong). Industry standard is 2-4%.

### Growth Rate Finding (Important)
- Roadmap Lite MODERATE = 15% Years 1-4, then 10% forever (aggressive)
- PropPath HIGH = 12.5% → 10% → 7.5% → 6% (tiered down, more conservative)
- PropPath numbers are more defensible — this is a selling point

### Competitive Landscape Clarification
- **Roadmap Lite** = internal lead gen tool for The Investors Agency. Not a standalone product.
- **Gameplans** = proven standalone business but expensive + requires consultants to deploy.
- **PropPath gap** = self-serve, BA-owned, Gameplans-level output without the consultant dependency.

---

## Product Strategy Discussion (Key Points)
- Rob confirmed: BAs build the plan, then present finished product to client. BA is the user, not the client.
- Inputs being prominent makes sense — BA needs to tweak in real time during pitch.
- "Next Buy Window" feature suggested: surface the AVAIL row as a proactive callout ("Next purchase window: 2027"). Retention play for BAs. Rob agreed this is valid.
- Retirement Scenario output agreed to be a data table when it should feel like a moment.
- Growth assumption visibility: should be a prominent toggle (Conservative/Moderate/Aggressive) not buried in property modal.

---

## Files Written This Session
| File | Contents |
|------|----------|
| `memory/knowledge/proppath-ui-map.md` | Every UI screen → code file mapping with all values from screenshots |
| `memory/knowledge/roadmap-lite-competitive-analysis.md` | Full Roadmap Lite analysis from 6 screenshots |
| `memory/screenshots/proppath-dashboard/` | 12 PropPath screenshots saved and named |
| `memory/screenshots/roadmap-lite/` | 6 Roadmap Lite screenshots saved and named |

---

## Confirmed Red Items (From Audit — Not Yet Fixed, Rob Not Ready to Fix)
1. **Vacancy rate = 0%** on most property types in `property-defaults.json`
2. **No APRA 3% serviceability buffer** in `calculateBorrowingCapacity.ts`
3. **Borrowing capacity stub** — `calculateUpdatedBorrowingCapacity` returns base unchanged
4. **No DTI check** in `guardrailValidator.ts`
5. **88% LVR default** across most property types → should be 80%
6. **Existing portfolio growth hardcoded at 3%** in `metricsCalculator.ts` → should be 5-6%

---

## Next Actions (When Rob Is Ready)

### Research Continuation
- Rob wants to continue research mode — not implementing fixes yet
- Outstanding question: where do the Add-to-Timeline modal display prices come from? ($400k for Units vs $350k in JSON)
- Consider: deeper analysis of useAffordabilityCalculator.ts to understand borrowing capacity cascade

### When Ready to Fix (Priority Order)
1. Add DTI check (6x) to `guardrailValidator.ts`
2. Fix LVR defaults 88% → 80% in `property-defaults.json`
3. Fix vacancy rates (2% minimum) in `property-defaults.json`
4. Add APRA 3% buffer to `calculateBorrowingCapacity.ts`
5. Fix borrowing capacity stub in metricsCalculator
6. "Plan Feasible" banner (UI only, 1 hour)

### UI Improvements Discussed (Not Prioritised Yet)
- Retirement Scenario — make it feel like a moment, not a data grid
- Growth assumption visibility — prominent Conservative/Moderate/Aggressive toggle
- "Next Buy Window" callout from AVAIL row data
- Borrowing calculator → connect result back to main dashboard

---

## Git Status
- No code changes this session
- Research files written to workspace (not yet committed)
- `ignito-project-kit` remains local only
