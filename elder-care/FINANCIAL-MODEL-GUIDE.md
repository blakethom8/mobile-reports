# Financial Model — Guide & Context

*Last updated: 2026-04-09*

---

## What This Model Does

This is an interactive financial planning tool for the Elder Care Platform — a services business that helps families manage elderly parents through an AI personal assistant backed by human Family Support Representatives (FSRs).

The model answers five planning questions across five views:

1. **Growth Model** — "If we grow at X families/month, what does the 36-month trajectory look like?"
2. **Model Setup** — "What assumptions are we actually using, what do they mean, and which downstream metrics do they move?"
3. **Capacity Planner** — "At a specific month in the ramp, what is actually constraining us: panel coverage, onboarding throughput, or budget?"
4. **Scenario Planner** — "How do the current plan and preset strategic paths compare on capital required, break-even timing, scale, and sensitivity?"
5. **Steady State** — "What does the mature business look like at 10K, 25K, 50K, 100K families?"

---

## The Business Model in a Nutshell

- Families pay a **monthly subscription** ($149-$499/mo depending on tier)
- Each family gets an **AI assistant** that handles ~95% of care coordination (information retrieval from banks, healthcare portals, care facilities)
- **FSRs (Family Support Representatives)** handle the remaining ~5% — onboarding, escalations, complex situations, quarterly reviews
- The company also has a **fixed cost base**: engineers building the platform/AI tools, org management, office/infrastructure

**Revenue = families × monthly price + onboarding fees**
**Costs = fixed (team + infra) + variable (FSRs + AI/cloud + processing)**

---

## Key Variables (Inputs)

### Demand-Side (What Drives FSR Needs)

| Variable | What It Is | Why It Matters |
|----------|-----------|----------------|
| **New families/month** | Growth target — how many families we onboard each month | Drives onboarding FSR needs and revenue ramp |
| **Onboarding hours/family** | Total human time to set up a new family (POA verification, portal connections, family setup) | THE bottleneck — determines how many families one FSR can onboard per month |
| **Monthly outreach rate** | % of active families that need human interaction each month | Drives ongoing panel workload (panel demand hours) |
| **Avg handle time** | Minutes per human interaction | Combined with outreach rate, sets panel demand hours per family |
| **Monthly churn rate** | % of families that leave each month (voluntary + structural) | Affects net growth, LTV, and steady-state family count |
| **Customer lifetime cap** | Max years a family stays (~5 years for the aging care journey) | Caps LTV and creates natural structural churn even at 0% voluntary churn |

### Revenue-Side

| Variable | What It Is |
|----------|-----------|
| **Monthly price/family** | Recurring subscription revenue |
| **Onboarding fee** | One-time fee when a family joins |
| **Paid acquisition cost** | Planning CAC input before onboarding labor is added |

### Supply-Side (FSR Capacity)

| Variable | What It Is | Why It Matters |
|----------|-----------|----------------|
| **FSR salary** | Annual compensation per FSR | Directly affects variable cost per family |
| **Families per FSR (target panel size)** | How many established (paneled) families one FSR should carry if workload allows | Key efficiency lever — AI tooling should drive this higher over time; the model binds this against workload so hiring reflects the tighter constraint |

### Fixed Costs (Team & Infrastructure)

| Variable | What It Is |
|----------|-----------|
| **Engineers** | Headcount building the platform and internal AI tools |
| **Org management** | Leadership, ops, compliance, admin |
| **Office/infra** | Physical offices, cloud infrastructure, tools |
| **AI/cloud cost per family** | Per-family compute/API costs |

---

## Key Metrics (Outputs)

### The #1 Metric: Human Time Per Family Per Month

Everything the AI/engineering team builds should drive this number down. It's the operational north star.

**Formula (same idea as panel demand hours):** `outreach_rate × handle_time_hours`

Example: 8% outreach × 40 min = 3.2 min/family/month = 0.053 hrs/family/month (**panel demand hours/family/mo**)

### Unit Economics

| Metric | Formula | What It Tells You |
|--------|---------|-------------------|
| **Variable cost/family** | FSR cost per family + AI/cloud + infra + payment processing | What each family costs to serve monthly |
| **Contribution margin** | Monthly price − variable cost | Profit per family before fixed costs |
| **Break-even families** | Monthly fixed costs ÷ contribution margin | How many families needed to cover the burn |
| **LTV** | Contribution margin × avg lifetime months (capped at ~60 months) | Total value of one family over their lifetime |
| **CAC** | Acquisition cost + onboarding labor cost | What it costs to get one family on the platform |
| **LTV:CAC ratio** | LTV ÷ CAC | Should be >3x for a healthy business |
| **Payback period** | CAC ÷ monthly contribution margin | Months to recoup acquisition cost |

### FSR Math

Each month, FSR time goes to one of two jobs: **onboarding new families** or **supporting families already on a panel**. The formulas below use the same time-budget pattern for both lanes so you can see which pressure dominates. If you later model **dedicated** onboarding vs panel-only roles, the demand rows stay the same; only the time-budget rows change (each role allocates 100% of its hours to one lane).

#### Shared time budget (per FSR, cross-trained assumption)

| Building block | Formula | Notes |
|----------------|---------|--------|
| **Monthly work hours** | 160 hrs/mo | Full-time baseline |
| **Onboarding hour share** | 50% of monthly work hours | Tunable if the product changes the split |
| **Panel hour share** | 50% of monthly work hours | Must sum with onboarding share to 100% for this staffing shape |
| **Onboarding hours budget per FSR/mo** | Monthly work hours × onboarding hour share | How many hours per FSR per month the model *assigns* to new-family setup after the split |
| **Panel hours budget per FSR/mo** | Monthly work hours × panel hour share | How many hours per FSR per month the model *assigns* to paneled families after the split |

With **160 hrs/mo** and a **50/50** split, each is **80 hrs/mo**. This is not “productivity” or utilization in the ops sense — it is only the **time budget** carved out for each lane before you divide by work per family.

#### Onboarding lane (new families / month)

| Metric | Formula | Meaning |
|--------|---------|---------|
| **Onboarding capacity per FSR** | Onboarding hours budget per FSR/mo ÷ onboarding hours/family | How many new families one FSR can complete per month at this split |
| **Onboarding FSRs needed** | New families/month ÷ onboarding capacity per FSR | Headcount if onboarding were the only job |

#### Panel lane (established / paneled families)

| Metric | Formula | Meaning |
|--------|---------|---------|
| **Panel demand hours/family/mo** | Outreach rate × handle time (hours) | Expected human hours per paneled family per month |
| **Workload-limited panel size per FSR** | Panel hours budget per FSR/mo ÷ panel demand hours/family/mo | Max paneled families one FSR can carry before hours run out |
| **Binding panel size per FSR** | min(target families per FSR, workload-limited panel size per FSR) | The panel size the model actually uses — target vs workload, whichever is tighter |
| **Panel FSRs needed** | Active families ÷ binding panel size per FSR | Headcount if panel support were the only job |

#### Panel size: what sets it — target vs demand buildup

Two different ideas get merged in the panel lane; both need to be explicit:

1. **Target families per FSR** (supply-side input) — what you *want* or *assume* for planning (e.g. scenario preset **1,000/FSR**). This is a thesis about leverage, not something physics derives for you.
2. **Demand buildup** (demand-side inputs) — for each paneled family, expected human load is **panel demand hours/family/mo** = outreach × handle time. Multiply by how many families sit on one FSR’s panel and you get total panel hours that FSR must cover for that panel.

The model combines them with **binding panel size** = **min(target, workload-limited)**. So:

- If **workload-limited** ≥ **target**, the target binds — you are panel-capacity-rich; staffing follows the **1,000** (or whatever you typed).
- If **workload-limited** is **smaller than** **target**, demand binds — the **1,000** is still your *goal*, but for staffing the model behaves as if each FSR can only safely carry the **workload-limited** number until outreach/handle time improves or you change the hour split / role design.

**Sanity check (your intuition):** 1,000 paneled families × **10%** outreach × **1 hour** per touch = **100 hours/mo** of panel work for that panel alone. Under a **50/50** cross-train, each FSR only has **80 hours/mo** for the whole panel lane — so **one FSR cannot** carry 1,000 families at that intensity; the workload math caps the panel long before the 1,000 target does.

##### Heuristic panel sizes (80 hr/mo panel budget, 50/50 on 160)

Illustrative **max paneled families per FSR** implied purely by demand — **panel hours budget ÷ (outreach × handle time in hours)**. Same formula as **workload-limited panel size per FSR**; numbers below are rounded. If your **target** is higher than the heuristic max, demand is binding.

**Problem-solving events (PSEs)** are the human-led interactions the model prices at **avg handle time** (escalations, complex coordination, live problem resolution — not routine AI-handled traffic). In this simplified demand stack, treat **monthly outreach rate** as the **average PSEs per paneled family per month** (one PSE ≈ one handle-time block). Then:

- **PSEs per FSR per month** at a full workload-limited panel ≈ **(max panel / FSR) × outreach** = **panel hours budget ÷ handle time (hours)** — the FSR’s 80 hr/mo panel budget converts straight into a PSE count at that handle time.

| Heuristic | Monthly outreach (≈ PSEs / family / mo) | Handle time / PSE | Panel demand hrs/family/mo | ≈ Max panel / FSR @ 80 hr panel budget | ≈ PSEs resolved / FSR / mo @ max panel |
|-----------|-------------------------------------------|---------------------|----------------------------|----------------------------------------|----------------------------------------|
| **Lighter touch** (strong AI, fewer exceptions) | 5% | 30 min | 0.025 | ~3,200 | ~160 |
| **Moderate** | 8% | 40 min | ~0.053 | ~1,500 | ~120 |
| **Heavier touch** (your 10% × 1 hr shape) | 10% | 60 min | 0.10 | ~800 | ~80 |

Change the **panel hour share** or go to **dedicated panel FSRs** (100% of monthly hours on the panel) and these caps scale roughly in proportion — e.g. **160 hr** all on panel at 10% × 1 hr → **~1,600** max per FSR from workload alone (and **~160** PSEs/mo at that handle time).

##### Illustrative: annual panel subscription vs one FSR (1,000-family panel)

Sometimes it helps to isolate **“subscription dollars for the families on one FSR’s panel”** vs **“what we pay that one FSR for the year.”** This is **not** full contribution margin — it ignores AI/cloud, payment processing, onboarding labor, other FSRs, and all fixed corporate cost. It is only a **labor-vs-panel-revenue** slice.

Assume **1,000 families** on one FSR’s panel and **$125K/year** all-in for one FSR (swap for your **FSR salary** assumption in the model). **Annual subscription revenue from that panel** = `1,000 × monthly price × 12`.

| Monthly price / family | Annual panel subscription revenue | Illustrative 1 FSR annual comp | Subscription revenue minus FSR comp only |
|------------------------|-----------------------------------|----------------------------------|------------------------------------------|
| **$100** | ~$1.20M | ~$0.125M | ~$1.08M |
| **$175** | ~$2.10M | ~$0.125M | ~$1.98M |
| **$250** | ~$3.00M | ~$0.125M | ~$2.88M |

At **$100/mo**, one FSR’s illustrative comp is on the order of **~10%** of that panel’s gross subscription revenue; at **$250/mo**, **~4%**. Your real **variable cost / family** in the model still layers in non-FSR variable costs on top of this.

#### Staffing outcome (cross-trained pool)

| Metric | Formula | Meaning |
|--------|---------|---------|
| **Required FSR pool** | max(onboarding FSRs needed, panel FSRs needed) | Under cross-training, one pool covers both lanes; staffing follows the **binding** lane, not the sum |

Implementation note: the current dashboard assumes a **cross-trained FSR pool** (continuity of care): each FSR draws from the same hour budget for onboarding and for paneled families. The model shows **onboarding FSRs needed** and **panel FSRs needed** as if each lane were isolated — that answers “which workload would force hiring first?” The **required FSR pool** is the larger of those two, not an additive total.

### Growth Metrics

| Metric | Formula |
|--------|---------|
| **Net family growth** | New families − churned families |
| **Active families** | Previous month active + net growth |
| **Monthly revenue** | (Active families × price) + (new families × onboarding fee) |
| **Monthly net income** | Revenue − fixed costs − variable costs |
| **Cumulative cash** | Running sum of monthly net income |
| **Capital required** | Peak cumulative cash deficit (how much you need to fund before break-even) |

---

## Relationship Map: How Variables Connect

```
New Families/Month ──→ Onboarding FSRs Needed ──→ FSR Cost
        │                                              │
        ↓                                              ↓
Active Families ──→ Panel FSRs Needed ──→ Variable Cost/Family
        │                                              │
        ↓                                              ↓
   Revenue ←── Price/Family              Contribution Margin
        │                                              │
        ↓                                              ↓
  Net Income = Revenue − Fixed Costs − Variable Costs
        │
        ↓
  Break-Even when Net Income ≥ 0
```

**The key tension:** Growing faster (more new families/month) increases revenue BUT also increases onboarding FSR needs. The model finds the sweet spot where growth rate, pricing, and FSR efficiency balance.

**The AI team's job:** Drive down `onboarding hours/family` and `outreach rate` through better tooling → fewer FSRs needed → lower variable costs → faster break-even.

---

## Phase Scaling

The model supports 3 company phases with different team sizes and costs:

| | Phase 1: Build & Launch | Phase 2: Early Growth | Phase 3: Scale |
|---|---|---|---|
| **Typical months** | 1-12 | 13-24 | 25-36 |
| **Engineers** | 5 | 8 | 12 |
| **Org mgmt** | 2 | 4 | 6 |
| **Office/infra** | $10K/mo | $25K/mo | $40K/mo |
| **New families/mo** | 75 | 150 | 250 |

Phase transitions create "cliff events" where costs jump. The model calculates break-even and cash flow through these step-ups.

---

## Scenario Presets

| Scenario | FSR Ratio | Outreach | Onboard Time | Price | Growth | Churn |
|----------|-----------|----------|-------------|-------|--------|-------|
| **Optimistic** | 1,000/FSR | 5% | 3 hrs | $299 | 100/mo | 1% |
| **Conservative** | 400/FSR | 8% | 6 hrs | $249 | 75/mo | 2% |
| **Premium Concierge** | 300/FSR | 10% | 8 hrs | $499 | 50/mo | 1.5% |
| **Health Plan Scale** | 500/FSR | 6% | 4 hrs | $199 | 300/mo | 1% |

---

## Churn: Two Types

1. **Voluntary churn** — family leaves due to dissatisfaction, cost, or competition. This is controllable.
2. **Structural churn** — parent passes away or transitions to end-of-life care. This is unavoidable and should be modeled as a **customer lifetime cap** (~5 years / 60 months).

The model should use the HIGHER of: monthly churn rate OR the implied churn from the lifetime cap (1/60 = ~1.7%/month).

**LTV should be capped** at contribution margin × min(1/churn_rate, lifetime_cap_months).

---

## What We're Still Working On

### UI/UX Issues to Fix
- [x] **Headcount by phase** — card now shows corporate headcount vs FSR headcount per phase
- [x] **Fixed cost by phase** — phase-aware card now shows cost per phase including ops load
- [x] Growth Model view uses collapsible input sections and phase cards
- [x] Model Setup view now acts like a planning workbook with grouped assumptions, impact chains, and visible formulas
- [x] Capacity Planner now uses a snapshot month and clearer constraint visualization
- [x] Scenario Planner now compares presets vs. current plan and includes sensitivity readout

### Model Enhancements Needed
- [x] Customer lifetime cap (separate from churn rate) — caps LTV and adds structural churn floor
- [x] Separate structural vs. controllable churn tracking in the UI
- [x] Phase-aware metric cards that show values at each phase, not just one number
- [ ] Tier mix / payer subsidy modeling
- [ ] Explicit starting cash and financing events
- [ ] Import/export for structured scenario data outside localStorage

### Views
- [x] Growth Model (36-month trajectory)
- [x] Model Setup (assumptions, impacts, and formulas in one place)
- [x] Capacity Planner (snapshot month → binding constraint)
- [x] Scenario Planner (preset comparison + sensitivity readout)
- [x] Steady State (what does 10K-100K families look like)

---

## File Location

- **Source:** `~/Repo/elder-care-platform/business/financial-model.html`
- **Published:** GitHub Pages via `mobile-reports` repo
- **Single self-contained HTML** — inline CSS/JS, Chart.js from CDN
- **No backend** — all calculations client-side, scenarios saved to localStorage

---

*This guide is for anyone (human or AI) working on the financial model. Update it when the model changes.*
