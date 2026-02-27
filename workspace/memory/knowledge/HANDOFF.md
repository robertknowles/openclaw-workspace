# HANDOFF.md — Session State Save
*Saved: Session ending — PropPath Research & Competitive Analysis Complete*

---

## Status: Research Phase Complete ✅ | No Code Changes Made

---

## What Was Completed This Session

### 1. PropPath Dashboard — Full UI Screenshot Tour
- Rob sent 12 screenshots covering every major dashboard screen
- All screens mapped to source code files
- Full document saved: `memory/knowledge/proppath-ui-map.md`
- All screenshots saved: `memory/screenshots/proppath-dashboard/` (01–12)

### 2. Roadmap Lite — Competitive Analysis
- Rob sent 6 screenshots of Roadmap Lite (The Investors Agency's internal tool)
- Full competitor breakdown saved: `memory/knowledge/roadmap-lite-competitive-analysis.md`
- All screenshots saved: `memory/screenshots/roadmap-lite/` (01–06)

### 3. Product Strategy Discussion
- Discussed and debated PropPath's positioning
- Rob corrected key assumption: tool is BA-led, not client-led
- Agreed on the market gap PropPath is targeting

---

## Key Research Findings This Session

### PropPath vs Roadmap Lite — Critical Gaps
| Issue | PropPath | Roadmap Lite |
|-------|----------|-------------|
| DTI check | ❌ Missing | ✅ "Lower of serviceability or 6x DTI" — prominent |
| LVR default | ❌ 88% (12% deposit) | ✅ 80% (20% deposit) |
| Vacancy rate | ❌ 0% on most types | ❌ Also 0% (both wrong) |
| Borrowing calc | ❌ Reverse from repayment | ✅ Income-based serviceability |
| Scenario comparison | ✅ A vs B | ❌ Not present |
| Break-even line | ✅ On cashflow chart | ❌ Not present |
| Property type variety | ✅ 7 types | ❌ Generic "Property 1-6" |
| Events system | ✅ Full (income/life/market) | ❌ Not present |

### Growth Rate Finding (Important)
- Roadmap Lite MODERATE = 15% p.a. years 1-4, then 10% p.a.
- PropPath HIGH = 12.5% → 10% → 7.5% → 6% (tiered down)
- **PropPath is already more conservative than competitor's middle tier** — defensible position

### Competitor Context
- **Roadmap Lite** = internal lead gen tool for The Investors Agency, not a standalone product
- **Gameplans** = proven standalone business, but expensive + consultant-dependent model
- **PropPath gap** = self-serve, BA-owned, Gameplans-quality output without the consultant overhead

### Product Strategy Agreed
- PropPath doesn't need to out-feature Gameplans
- Needs to be credible enough for a BA to present confidently without a consultant
- Financial rigor gaps (DTI, LVR, vacancy) are the credibility blockers
- "Next Buy Window" callout identified as high-value retention feature for BAs

---

## Confirmed Code Locations for Red Items

| Fix | File | Status |
|-----|------|--------|
| Vacancy rate = 0% | `src/data/property-defaults.json` | Ready to fix |
| No APRA 3% buffer | `src/utils/calculateBorrowingCapacity.ts` | Ready to fix |
| Borrowing capacity stub | `src/utils/metricsCalculator.ts` | Ready to fix |
| No DTI check | `src/utils/guardrailValidator.ts` | Ready to fix |
| LVR 88% default | `src/data/property-defaults.json` | Ready to fix |

**Note: Rob does NOT want to implement fixes yet. Research phase only.**

---

## Files Written This Session
| File | Contents |
|------|----------|
| `memory/knowledge/proppath-ui-map.md` | Every dashboard screen mapped to source code |
| `memory/knowledge/roadmap-lite-competitive-analysis.md` | Full competitor breakdown with numbers |
| `memory/screenshots/proppath-dashboard/` | 12 PropPath dashboard screenshots (named) |
| `memory/screenshots/roadmap-lite/` | 6 Roadmap Lite screenshots (named) |

---

## Screenshot Index

### PropPath Dashboard
| File | Screen |
|------|--------|
| 01-borrowing-calculator-modal.png | "How much can I borrow?" modal |
| 02-retirement-scenario.png | Retirement Scenario sliders + 6-metric grid |
| 03-add-second-scenario-button.png | "Add a second scenario" button |
| 04-investment-timeline-wealth.png | Investment Timeline — Wealth tab |
| 05-scenario-ab-comparison.png | Scenario A vs B side-by-side |
| 06-investment-timeline-cashflow.png | Investment Timeline — Cashflow tab with break-even |
| 07-property-performance-modal.png | Per-property performance (Units/Apts) |
| 08-client-details-card.png | Client Details 3-column card |
| 09-property-timeline-panel.png | Property Timeline left panel |
| 10-custom-property-block-modal.png | Create Custom Property Block modal |
| 11-add-to-timeline-properties.png | Add to Timeline — Properties tab |
| 12-add-to-timeline-events.png | Add to Timeline — Events tab |

### Roadmap Lite
| File | Screen |
|------|--------|
| 01-financial-profile-borrowing-power.png | $1.56M borrowing power + financial profile inputs |
| 02-property-pipeline.png | 6-property pipeline with MODERATE tags |
| 03-dashboard-output.png | Full dashboard: KPIs, charts, retirement scenario |
| 04-expenses-tab.png | Property expenses tab (council, insurance, maintenance) |
| 05-buying-costs-tab.png | Buying costs tab (stamp duty, BA fee, other) |
| 06-assumptions-tab.png | Assumptions tab (growth profile + interest rate) |

---

## Next Session — Where to Pick Up

Rob wants to continue research. Likely next topics:
1. Deep dive into PropPath numbers audit (growth rates, vacancy, serviceability calculations)
2. Product roadmap / feature prioritisation discussion
3. OR: Begin implementing fixes when Rob is ready

**Do NOT start fixing code without Rob explicitly saying so.**

---

## Codebase Location
- Repo: `robertknowles/ignito-project-kit`
- Local path: `/Users/robertknowles/.openclaw/workspace/ignito-project-kit/`
