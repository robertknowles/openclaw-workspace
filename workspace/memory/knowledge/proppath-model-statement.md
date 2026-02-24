# PropPath Model Statement — Calibration Document
*For use in any PropPath audit, feature evaluation, or product decision*
*Compiled: Feb 2026*

---

## THE CORE STATEMENT

**PropPath is incremental, not simulation-first.**

This is the single most important statement for calibrating any audit of PropPath's logic, features, or product decisions. Everything below explains what it means and why it matters.

---

## Two Distinct Planning Models in the BA Market

### Model A: Simulation-First (Gameplans)
- BA inputs a hypothetical end-state: "client buys 5 properties over 10 years at X% growth"
- Tool runs the simulation forward and produces a projected outcome
- Client sees a polished end-state: "in 2034, your portfolio will be worth $X with $Y passive income"
- The output is a **forecast** — a picture of a possible future
- Session-time tool: used live with the client, then filed away
- Validation question: **"Is the end-state realistic? Are the assumptions credible?"**
- Weakness: assumes the future plays out as modelled. Real decisions (which deal next, serviceability constraints, market shifts) are abstracted away.

### Model B: Incremental, BA-Guided (InvestorKit)
- BA works with client one property at a time
- Each acquisition decision is made based on the client's *current* financial position
- After each purchase: review actual performance, reassess serviceability, decide on next move
- The portfolio plan is a living document — it updates with reality, not just with projections
- Validation question: **"Does this specific property make sense given where the client is right now? And does adding it keep the cumulative portfolio coherent?"**
- Strength: each decision is grounded in real numbers (actual equity, actual borrowing capacity, actual cash flow)

---

## InvestorKit's Incremental Model — How It Actually Works

### Property Sequence Framework (Three Stages)
InvestorKit explicitly moves clients through a staged sequence:
1. **Foundation Properties** — capital growth assets that build the equity base
2. **Momentum Assets** — properties that combine growth + yield to maintain serviceability and accelerate the portfolio
3. **Passive Income** — commercial assets and unit blocks that generate stable cash flow at portfolio maturity

Each stage informs the NEXT decision. You don't buy a passive income asset before you've built the equity base. The sequence is the strategy.

### The Acquire → Optimise → Consolidate Cycle (Repeats Per Property)
For each property added:
1. **Acquire** — find and purchase the right property for the client's current position
2. **Optimise** — maximise performance: rent reviews, refinancing, depreciation, property management
3. **Consolidate** — review updated portfolio position, recalculate borrowing capacity, decide if/when to acquire next

This cycle **repeats** for every property. The plan is never "set and forget" — it's re-evaluated at each consolidation step.

### Monthly Reviews Are Structural (Not Optional)
InvestorKit Portfolio Strategists conduct monthly client review sessions as a core part of the service. This is not an add-on — it's how the plan stays alive. Each review:
- Checks actual performance vs plan
- Updates borrowing capacity based on current position
- Identifies whether conditions are right for the next acquisition
- Generates any buyer brief for the next property

### The "3 Properties in 3 Years" Outcome
InvestorKit's headline stat is "most clients get 3 properties in 3 years." This is not a simulation output — it's a repeatable incremental outcome. Each property is a discrete decision, grounded in the client's real numbers at that point in time.

---

## Where PropPath Sits

**PropPath is aligned to the InvestorKit model, not the Gameplans model.**

PropPath's design premise:
- The BA adds properties one at a time as they are acquired (not upfront as hypotheticals)
- Each property addition updates the portfolio's real numbers (equity, cash flow, LVR, borrowing capacity)
- The roadmap evolves as the portfolio grows — it is not a fixed forecast
- The client sees their *actual* progress against their *goal*, not a simulation of what might happen
- Alerts (equity triggers, serviceability warnings) fire based on real positions, not modelled ones

**Analogy:**
- Gameplans is Google Maps route preview — shows you the full journey before you leave
- PropPath is a live navigation tool — it knows where you are now, updates in real time, and recalculates the route as conditions change

---

## What This Means for Auditing PropPath

### The RIGHT audit questions for PropPath (incremental model):
1. **Per-property logic:** When a new property is added, do all downstream numbers update correctly? (equity, LVR, cash flow, borrowing capacity, goal progress)
2. **Cumulative coherence:** As properties accumulate, does the portfolio remain internally consistent? (e.g. if Property 2 reduces borrowing capacity, does that flow through to the roadmap?)
3. **State transition accuracy:** When a client moves from "Foundation" to "Momentum" stage, does the tool correctly reflect the change in what deal type is appropriate?
4. **Serviceability logic:** Does the tool correctly model that each new mortgage increases assessed liabilities — and flag when the client is approaching a serviceability ceiling?
5. **Equity trigger precision:** Is the equity-available-for-next-purchase calculation correct at each point in the portfolio's lifecycle?
6. **Real number grounding:** Are all projections clearly labelled as estimates vs real data? Does the tool distinguish between confirmed values (actual purchase price, actual rental income) and modelled values (projected growth rate, future valuation)?

### The WRONG audit questions for PropPath (these apply to Gameplans, not PropPath):
- ❌ "Is the 10-year end-state realistic?"
- ❌ "Are the growth rate assumptions credible at portfolio level?"
- ❌ "Does the simulation match historical market performance?"
- ❌ "Is the output PDF a believable forecast document?"

These are Gameplans validation questions. Applying them to PropPath will produce false negatives — PropPath will look "less impressive" because it doesn't promise a polished end-state simulation. That's by design.

---

## The Key Tension to Hold

PropPath must show clients enough of the forward picture to be motivating (they need to see the path to $100k passive income), but ground every forward projection in the current real position.

The resolution:
- **Actuals are actuals** — confirmed purchase prices, current rental income, known mortgage rates
- **Projections are projections** — clearly marked, adjustable by the BA, not presented as certainty
- **The roadmap is directional, not contractual** — it shows the shape of the journey, not a guaranteed destination

This is exactly how InvestorKit operates: the portfolio plan shows the long-term picture, but every acquisition decision is made fresh based on where the client actually is.

---

## Summary Table

| Dimension | Gameplans | InvestorKit | PropPath |
|-----------|-----------|-------------|----------|
| Planning model | Simulation-first | Incremental, BA-guided | Incremental, BA-guided |
| Output | End-state forecast | Living portfolio plan | Living portfolio plan |
| Client interaction | Session tool (BA-facing) | Ongoing relationship | Client portal + BA view |
| Plan updates | Manually re-run | Monthly reviews | Real-time as properties added |
| Validation unit | Full portfolio simulation | Per-property decision | Per-property decision |
| Numbers used | Hypothetical inputs | Real + projected (clearly separated) | Real + projected (clearly separated) |
| Key risk | Garbage-in-garbage-out | Relies on BA discipline | Relies on BA keeping data current |

---

## Instruction to Future Bertie Sessions

When auditing PropPath features, evaluating product logic, or reviewing whether the tool is "correct" — always apply the incremental model test:

> "If a BA adds Property 3 to a client's portfolio today, with real numbers — does PropPath update every downstream calculation correctly? Does the roadmap remain coherent? Does the client's position toward their goal update accurately?"

That is the audit. Not "does the 10-year simulation look right."
