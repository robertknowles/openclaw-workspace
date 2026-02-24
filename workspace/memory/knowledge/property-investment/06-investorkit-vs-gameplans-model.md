# InvestorKit Deep Dive + The PropPath Model Statement
*Research: Feb 2026 | Purpose: Calibrate PropPath product audit correctly*

---

## THE CRITICAL FRAMING (Read This First)

**This document exists because the validation questions for PropPath depend entirely on which model it follows.**

There are two fundamentally different approaches to property portfolio planning tools:

| | **Gameplans Model** | **InvestorKit Model** |
|---|---|---|
| **Approach** | Simulation-first | Incremental, BA-guided |
| **How it works** | BA builds a full end-state 30-year simulation, then hands it back to the client | BA builds the plan one property at a time, guided by what's actually achievable right now |
| **Client experience** | "Here is your complete property future, modelled out" | "Here is your next move. We'll review when you're ready for the one after." |
| **Tool role** | Projection engine — inputs go in, trajectory comes out | Living record — each property gets added, numbers update, next step emerges |
| **Audit question** | Is the end-state simulation realistic? Are the 30-year growth assumptions defensible? | Does each individual property's numbers hold up? Does the cumulative portfolio logic stay coherent as the plan grows? |

**PropPath is incremental, not simulation-first.**

This is the correct framing. Any audit of PropPath must be calibrated to this — not to Gameplans' logic.

---

## What "Simulation-First" Means (Gameplans)

From Gameplans' own website:
- *"Show clients with confidence what their 30-year wealth trajectory looks like as you adjust the strategy in real-time"*
- *"Compare scenarios side-by-side. Residential vs commercial investments. Two properties vs one."*
- *"Show exactly how their current equity becomes their next property purchase — clear timelines, rental projections, and growth forecasts"*

**The Gameplans flow:**
1. BA inputs client's financial position
2. BA inputs a set of assumptions (growth rates, yields, leverage, future purchases)
3. System generates a full 30-year projection
4. Client sees the complete end-state output
5. BA and client compare scenarios (what if we buy commercial instead?)
6. Session ends — client has a vision of their future

**The risk in this model:** The output is only as good as the assumptions. If a BA inputs 7% annual growth in every market, the 30-year chart looks spectacular — but it's fiction. The audit question for Gameplans is: are the assumptions defensible?

**The product role:** Gameplans is primarily a *conversion tool* — used in live sessions to show clients a compelling enough future to commit to working with the BA. The BA leads the session. The tool generates the vision.

---

## What "Incremental, BA-Guided" Means (InvestorKit)

InvestorKit's process is fundamentally different. Key evidence:

### The 5-Step Process (confirmed from their website):
1. **Free discovery call** — is this client a fit?
2. **Comprehensive assessment** — financial goals, risk profile, investment experience
3. **Portfolio mapping session + strategy** — tailored roadmap built *with* the client
4. **Seamless acquisition** — find and buy the right property, *guided by the plan*
5. **Post-settlement support** — *ongoing reviews, next purchase planning*

**The critical word: ongoing.** InvestorKit doesn't build a 30-year chart and walk away. They stay in the relationship. They conduct monthly reviews. They help the client plan the *next* purchase when ready.

### InvestorKit's Property Sequence (confirmed from research):
Arjun explicitly describes how clients move through stages:
- **Foundation properties** — solid growth assets, built to last, entry-level to the journey
- **Momentum assets** — higher velocity, leverage the equity from foundations, accelerate the portfolio
- **Passive income phase** — commercial and unit blocks, transition to income-generating assets

This is not a simulation. This is a **sequence of real decisions**, made one at a time, each informed by what the previous property has done.

### The Acquire → Optimise → Consolidate Cycle (InvestorKit):
For **each individual property**:
1. **Acquire** — buy the right property, at the right price, in the right market
2. **Optimise** — refinance, rent review, depreciation schedule, property management improvements
3. **Consolidate** — assess current portfolio position, determine borrowing capacity, plan next cycle

The cycle repeats. Each time round, the whole portfolio is reassessed. The plan is never static — it updates based on what actually happened.

### What InvestorKit's Portfolio Mapping Session Actually Produces:
From case studies and job listing language:
- A **personalised roadmap** — showing the path from today's position to the long-term income goal
- Produced **collaboratively**, with the BA and client building it together
- Used as a **reference document** throughout the engagement — not a one-time output
- **Monthly reviews** keep the roadmap current
- When a client is ready for Property 2, the BA produces an updated **buyer brief** — a fresh, specific document aligned to where the client now sits

From the Ryan & Lauren case study:
> *"Using their portfolio plan with InvestorKit, they can see the long-term impact."*

This portfolio plan is a **living thing** — it's there throughout the journey, not handed over once and forgotten.

---

## The InvestorKit Property Sequence Framework (Confirmed)

From the data framework Arjun described:

**Market categorisation:**
- Early Adopter Markets (starting growth, low awareness)
- Hotspots (tight stock, bidding wars, FOMO-driven)
- Second-Wind Zones (cooled-off post-boom, ripe for re-entry)

**Portfolio stage sequence (confirmed language):**
1. **Foundation** → solid growth asset, proven location, capital growth priority
2. **Momentum** → accelerate using equity from foundation, higher velocity
3. **Passive income** → commercial and unit blocks, income over growth, 5+ states spread

This is directly analogous to APS's B&B → Cash Flow → Growth sequence, and Pivot Property's 5-phase model (Accumulate → Expedite → Mature → Consolidate → Debt Reduce).

All roads lead to the same underlying logic: **portfolio building is a sequence of deliberate, stage-aware property decisions — not a single simulation.**

---

## Why This Matters for PropPath

### The wrong audit (Gameplans framing):
*"Is PropPath's 30-year projection realistic? Are the growth rate assumptions defensible? Does the end-state model account for interest rate variance?"*

This is the wrong set of questions. It treats PropPath as a simulation engine. If PropPath is incremental, these aren't the primary risks.

### The right audit (InvestorKit framing):
*"When a new property is added to a client's plan, do that property's individual numbers hold up? As properties accumulate, does the cumulative portfolio logic stay coherent? Does the system correctly update borrowing capacity, cash flow, and equity position after each addition?"*

This is the real risk surface for PropPath. The questions become:
- Is the equity extraction calculation correct after each property is added?
- Does borrowing capacity re-calculate correctly when cash flow changes?
- If Property 2 underperforms, does the plan correctly reflect the impact on when Property 3 is viable?
- Are the per-property inputs (yield, growth rate, LVR, purchase costs) producing correct outputs at the portfolio level?
- Does the portfolio cascade logic stay coherent — i.e., does a change to Property 1 correctly flow through to the equity available for Property 3?

---

## PropPath Model Statement (Canonical)

> **PropPath is incremental, not simulation-first.**
>
> PropPath builds a portfolio plan property-by-property, in collaboration between the BA and the client. Each property is added with its own real inputs. The cumulative portfolio position updates after each addition. The roadmap evolves as the portfolio grows — it is never a static end-state output.
>
> The right validation lens for PropPath is: does each individual property's numbers hold up as it gets added, and does the cumulative portfolio logic stay coherent as the plan grows?
>
> This is a fundamentally different product from Gameplans, which generates a 30-year simulation and hands it back. PropPath is the living record of an ongoing, BA-guided investment journey.

---

## Competitive Summary: InvestorKit vs Gameplans (as tool models)

| Dimension | Gameplans | InvestorKit |
|-----------|-----------|-------------|
| Planning model | Simulation-first | Incremental, sequence-driven |
| Time horizon shown | 30-year projection | Next 1–3 properties (with long-term goal anchor) |
| When plan is built | In a live session, upfront | Iteratively, as each property is acquired |
| Client touchpoint | Session tool (one-time or refresh) | Monthly reviews, ongoing lifecycle |
| Property stages | Agnostic (input what you want) | Foundation → Momentum → Passive Income |
| Equity trigger | Yes (built in, alerts BA) | Yes (built into review cadence) |
| Client portal | No (BA-facing only) | No (BA-managed, client not self-service) |
| Post-settlement | Not core product | Core product (Optimise + Consolidate cycle) |
| PropPath resemblance | Shares: scenario tool, equity alert | Shares: incremental build, living roadmap, lifecycle |

**PropPath is closer to InvestorKit's model. The audit must reflect that.**

---

## Open Questions (Carry Forward)

- Does InvestorKit's Portfolio Wealth Accelerator (their name for their internal tool) do anything more than Gameplans? Is it Gameplans white-labelled, or custom-built?
- How does InvestorKit's monthly review session actually work — what format, what data is reviewed?
- When InvestorKit updates a portfolio plan mid-journey, how is that change communicated to the client? (Email? Portal? Session?)
- What does InvestorKit's "buyer brief" document actually contain, and how does it connect back to the long-term roadmap?
- Can a client request changes to their portfolio plan, or is it fully BA-controlled?
