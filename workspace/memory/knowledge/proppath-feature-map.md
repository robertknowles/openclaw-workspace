# PropPath — Master Feature Map
*Compiled: Feb 2026 | Sources: 5 knowledge docs, Gameplans gap analysis, InvestorKit breakdown, APS framework*

---

## The PropPath Model Statement (Canonical — Read Before Any Audit)

> **PropPath is incremental, not simulation-first.**
>
> PropPath builds a portfolio plan property-by-property, in collaboration between the BA and the client. Each property is added with its own real inputs. The cumulative portfolio position updates after each addition. The roadmap evolves as the portfolio grows — it is never a static end-state output.
>
> The right validation lens for PropPath is: **does each individual property's numbers hold up as it gets added, and does the cumulative portfolio logic stay coherent as the plan grows?**
>
> This is fundamentally different from Gameplans, which generates a 30-year simulation and hands it back. PropPath is the living record of an ongoing, BA-guided investment journey. Evaluating PropPath against Gameplans' logic will draw the wrong conclusions.

---

## Strategic Position (One Line)

**PropPath is the living portfolio roadmap that sits between the BA and the client — the plan that persists between sessions, tracks progress, and triggers the next move.**

---

## ⚠️ Model Calibration (Read Before Auditing)

**PropPath is incremental, not simulation-first.**

PropPath follows the InvestorKit model — the BA builds the portfolio plan property-by-property as each acquisition happens, grounded in the client's real financial position at each step. It is NOT a Gameplans-style simulation that projects an end-state upfront.

**Audit against:** per-property logic, cumulative coherence, serviceability tracking, equity trigger accuracy.
**Do NOT audit against:** end-state simulation realism, 10-year forecast credibility, or portfolio-level growth assumptions.

Full model statement: `memory/knowledge/proppath-model-statement.md`

---

## The Core Problem We Solve

- BAs use Gameplans (or spreadsheets) **during a session** — client never sees it again
- No client-facing portal exists for ongoing portfolio tracking
- Clients feel out of the loop between purchases (6–24 month gaps)
- BAs lose touch with clients between deals → churn risk, missed upsell moments
- The portfolio "plan" lives in the BA's head or a PDF — not a living tool

---

## Feature Map — Prioritised by Impact × Feasibility

### TIER 1 — Core MVP (Highest Impact, Must Ship)

---

#### 1.1 Portfolio Roadmap Builder
**What:** Visual, step-by-step portfolio plan from current position → income goal
**Inputs:** Current properties, savings, income, target passive income, timeline
**Output:** 5–10 property roadmap showing sequence, expected values, yield, equity milestones
**Source insight:** Every BA does this manually in Gameplans or Excel. Nobody gives it to the client.
**Priority:** P0 — this IS the product

---

#### 1.2 Goal Reverse-Engineering Engine
**What:** Client sets a goal (e.g. "$100k passive income by 2035") → system calculates how many properties, at what yield, in what timeframe
**Based on:** APS framework — "reverse engineer your income goal"
**Inputs:** Target income, timeline, average yield assumption, average growth rate assumption
**Output:** "You need 4 properties averaging 6.5% yield. At your current pace, you reach this in 2031."
**Priority:** P0 — underpins the roadmap

---

#### 1.3 Current Portfolio Dashboard
**What:** Live view of client's existing portfolio — properties, equity, LVR, cash flow, total value
**Metrics per property:** Purchase price, current value (auto or manual), equity, LVR, rent, yield, cash flow (weekly/monthly)
**Portfolio totals:** Net equity, total value, total debt, portfolio yield, weekly cash flow
**Priority:** P0 — must show client where they are today

---

#### 1.4 Equity Trigger Alerts ⭐ (Gameplans Killer Feature)
**What:** Automatically alerts the BA and client when the client has enough equity to fund their next purchase
**Logic:** When (current equity - next deposit required - buffer) > 0 → trigger alert
**Alert modes:** Email, in-app notification, BA dashboard alert
**Source insight:** This is Gameplans' #1 feature — "Sarah has enough equity for her next purchase." PropPath must replicate and extend this.
**Priority:** P0 — this is the retention + upsell mechanism

---

#### 1.5 Milestone Tracker
**What:** Visual timeline showing planned vs. actual progress on the portfolio roadmap
**Milestones:** Property purchases, equity extraction events, valuation dates, review sessions, goal achievement
**Show:** "Property 2 — planned Q3 2024 → achieved Q1 2025"
**Priority:** P0 — keeps clients engaged between purchases

---

### TIER 2 — Core Product (High Impact, Ship in V1)

---

#### 2.1 Borrowing Capacity Tracker
**What:** Year-by-year projection of borrowing capacity as portfolio grows
**Show:** How each new property affects borrowing capacity (positive via cash flow, negative via increased debt)
**Alert:** "Serviceability ceiling approaching — you may need a cash flow deal before your next growth purchase"
**Source insight:** APS serviceability management — interleave cash flow + growth deals to stay borrowable
**Priority:** P1 — critical for multi-property portfolios

---

#### 2.2 Deal Type Sequencing Engine
**What:** Recommend the right deal type (B&B, Cash Flow, Manufactured Equity) based on client's current position
**Logic:**
- If borrowing capacity tight → recommend Cash Flow deal next
- If equity available but servicing strong → recommend B&B growth deal
- If equity needs boosting fast → recommend Manufactured Equity deal
**Source insight:** APS's 3 deal type framework — this is how they think. No tool visualises it.
**Priority:** P1 — differentiator vs Gameplans

---

#### 2.3 Cash Flow Projection (Portfolio Level)
**What:** Forward projection of weekly/monthly cash flow as new properties are added
**Show:** Portfolio cash flow at each stage — how it changes with interest rate moves, rent reviews, new purchases
**Alert:** "If rates rise 1%, your portfolio moves from +$200/wk to -$150/wk"
**Priority:** P1 — clients want to know if they're sustainable

---

#### 2.4 Equity Growth Chart (Per Property + Portfolio)
**What:** Visual chart showing equity accumulation over time — per property and total portfolio
**Show:** Capital growth trajectory + debt reduction → net equity line over 10–20 years
**Priority:** P1 — most visually compelling output for client

---

#### 2.5 Scenario Modelling / "What If" Tool
**What:** Side-by-side comparison of portfolio trajectories under different scenarios
**Scenarios:** Different growth rates, different purchase timing, adding vs. not adding property, selling one asset
**Source insight:** Gameplans does this in live sessions. PropPath should let client run it themselves.
**Priority:** P1 — high engagement driver, mirrors Gameplans core function

---

#### 2.6 BA ↔ Client Portal (Dual View)
**What:** Separate views for BA (full edit, client management, alerts) and client (read-only roadmap + progress)
**BA view:** Manage all clients, set roadmaps, update properties, see equity alerts, manage review sessions
**Client view:** Their roadmap, portfolio dashboard, milestones, messages from BA
**Source insight:** Gameplans is BA-only. This is PropPath's biggest differentiator.
**Priority:** P1 — defines the product model

---

#### 2.7 Acquire → Optimise → Consolidate Cycle Tracker
**What:** For each property, show where it sits in the InvestorKit cycle — is it being Acquired, Optimised, or being Consolidated (sold down)?
**Actions per phase:** Acquire = purchase actions; Optimise = rent review due, refinance opportunity, depreciation schedule; Consolidate = sell triggers
**Source insight:** InvestorKit's explicit portfolio lifecycle model
**Priority:** P1 — resonates with InvestorKit-style BA clients

---

### TIER 3 — Growth Features (High Value, Ship in V2)

---

#### 3.1 Portfolio Review Session Tool
**What:** Structured template for BA to conduct monthly/quarterly client reviews inside PropPath
**What it generates:** Progress since last session, equity change, cash flow change, next action items
**Replaces:** Unstructured phone calls, manual spreadsheet updates before each session
**Source insight:** InvestorKit builds monthly reviews into every engagement. PropPath should make these structured and documented.
**Priority:** P2

---

#### 3.2 State Diversification Map
**What:** Visual map showing which states the client has exposure in — and recommended diversification
**Show:** Properties per state, equity per state, cash flow per state
**Alert:** "3 of your 4 properties are in QLD. Consider geographic diversification."
**Source insight:** APS and InvestorKit both invest across 3+ states. This is standard BA advice.
**Priority:** P2

---

#### 3.3 Buyer Brief Builder
**What:** BA uses PropPath to generate a structured buyer brief for the next acquisition — aligned to client's roadmap position
**Output:** Property type, price range, location criteria, yield target, growth target, deal type
**Source insight:** InvestorKit Portfolio Strategist job listing — "generate accurate, actionable buyer briefs"
**Priority:** P2 — bridges planning to acquisition

---

#### 3.4 Borrowing Capacity Optimization Suggestions
**What:** Proactive suggestions for how the client can improve their borrowing capacity before next purchase
**Suggestions:** Reduce credit card limits, refinance existing properties, cash flow deal first, pay down non-deductible debt (debt recycling)
**Source insight:** APS "acting rich vs being wealthy" — kill expenses that hurt serviceability
**Priority:** P2

---

#### 3.5 Debt Recycling Visualiser
**What:** Show how converting PPOR debt into investment debt (debt recycling) affects the portfolio trajectory over 10–20 years
**Show:** Tax savings + investment growth vs base case (no debt recycling)
**Source insight:** Doc 02 — debt recycling is an advanced but common strategy for PPOR + IP holders
**Priority:** P2 — differentiator for clients who own their PPOR

---

#### 3.6 Multi-Entity / Structure View
**What:** Portfolio view that spans multiple ownership structures — individual, joint, trust, SMSF
**Show:** Properties per entity, equity per entity, total portfolio consolidated
**Source insight:** Doc 02 — clients hold across entities. A portfolio tool that only sees one entity misses half the picture.
**Priority:** P2 — important for more advanced clients

---

#### 3.7 Valuation Update Requests
**What:** Client or BA can flag a property for valuation review — log estimated vs. bank valuation vs. market estimate
**Show:** Equity impact of valuation update — does it trigger an equity alert?
**Priority:** P2

---

#### 3.8 Rent Review Tracker
**What:** Track lease end dates, current rent, market rent benchmarks, when to request a rent review
**Alert:** "Property 2 lease expires in 45 days — market rent has increased $80/wk"
**Source insight:** InvestorKit Optimise phase — rent reviews are a standard optimisation action
**Priority:** P2

---

### TIER 4 — Advanced / Future (V3+)

---

#### 4.1 SMSF Sub-Portfolio Tracker
- Separate SMSF view within multi-entity mode
- Show LRBA balance, contribution room, pension phase toggle
- Source: APS + InvestorKit both have SMSF clients

#### 4.2 Renovation / Manufactured Equity Tracker
- Log reno budget, actual spend, before/after valuation
- Show equity manufactured vs. cost
- Show how it changes the portfolio roadmap timeline

#### 4.3 Commercial Property Module
- InvestorKit does residential AND commercial
- Phase 4 of the 5-phase journey = sell down residential → move into commercial cash flow assets
- PropPath should be able to show commercial assets in the portfolio view

#### 4.4 Syndicated / Co-Investment Portfolio View
- Emerging trend (Doc 02 — equity stacking / co-investment)
- Show partial ownership stakes in syndicates
- Future-proofing for more sophisticated investors

#### 4.5 Portfolio Health Score
- Single number (0–100) that shows portfolio health
- Inputs: diversification, cash flow, LVR, equity trajectory, goal progress
- "Your portfolio health score is 74/100. Improve cash flow to unlock next purchase."

#### 4.6 Rate Sensitivity Stress Test
- "What happens to my portfolio if rates go up 2%?"
- Show: cash flow impact, new weekly deficit, how long until portfolio is stressed
- Could be a selling point for risk-aware clients

#### 4.7 Lender/Broker Integration
- Connect to broker's serviceability calculators
- Auto-import current mortgage rates, remaining balances
- Trigger equity alerts based on real bank valuations, not estimates

---

## Gameplans Gap Analysis Summary

| Feature | Gameplans | PropPath |
|---------|-----------|----------|
| Session-time scenario modelling | ✅ | ✅ (V1) |
| BA-facing tool | ✅ | ✅ |
| Client-facing portal | ❌ | ✅ P0 |
| Ongoing living roadmap | ❌ (likely) | ✅ P0 |
| Equity trigger alerts | ✅ | ✅ P0 |
| Milestone tracking | ❌ | ✅ P0 |
| Deal type sequencing | ❌ | ✅ P1 |
| Acquire→Optimise→Consolidate cycle | ❌ | ✅ P1 |
| Review session tool | ❌ | ✅ P2 |
| Multi-entity view | Unknown | ✅ P2 |
| SMSF module | Unknown | ✅ V3 |

---

## Summary — The PropPath MVP

**6 features that define the product:**
1. Portfolio Roadmap Builder (visual, BA-created, client-viewable)
2. Goal Reverse-Engineering Engine (income goal → property count → timeline)
3. Current Portfolio Dashboard (equity, LVR, cash flow, value)
4. Equity Trigger Alerts (automated "time to buy again" notifications)
5. Milestone Tracker (planned vs actual progress)
6. Dual BA/Client Portal (BA builds, client views ongoing)

These 6 features make PropPath the first client-facing, living portfolio planning tool in the Australian BA market.

---

## Open Questions (Carry Forward)
- Does Gameplans have a client portal / ongoing access?
- What is Gameplans' pricing for BAs?
- What does the Gameplans output actually look like?
- Should PropPath show the Acquire→Optimise→Consolidate cycle explicitly?
- Should PropPath have a borrowing capacity calculator built in, or connect to broker tools?
- Does PropPath's roadmap show the 5-phase portfolio journey (Accumulate → Expedite → Mature → Consolidate → Debt Reduce)?
- What is the right pricing model for PropPath? Per BA? Per client seat? Flat SaaS?
