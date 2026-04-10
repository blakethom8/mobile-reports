# FSR Onboarding as the Binding Constraint

*Created: 2026-04-09 | Core operational insight from brainstorm session*

---

## The Key Insight

**Onboarding new families is the dominant labor cost during the entire growth phase — by a wide margin.**

One onboarding event (3-6 hours) consumes the same FSR time as 57-113 months of panel support for that same family.

This means during Years 1-5, the company's operational challenge is almost entirely an **onboarding throughput problem**, not a panel management problem.

---

## The Ratio: Onboarding vs Panel Labor

Per family:

| Activity | Human Time | Relative Weight |
|----------|-----------|----------------|
| **Onboarding (one-time)** | 3-6 hours | 57-113x panel |
| **Panel support (ongoing, per month)** | ~0.053 hrs (3.2 min) | 1x |

**One onboarding = 5-9 years of monthly panel support for the same family.**

### Total FSR Hours Formula (Growth Phase Simplification)

```
Monthly FSR hours = (new families × onboarding hours) + (active families × 0.053)
```

During growth phase, panel is consistently 15-25% of total hours. Onboarding is 75-85%.

### Simple Heuristic

For Years 1-3 planning:

```
FSRs needed ≈ (new families/month × onboarding hours) ÷ 160
```

Add ~1 FSR for buffer and panel coverage. This approximation is accurate within 15% during the growth phase.

---

## When Does Panel Overtake Onboarding?

Panel hours exceed onboarding hours when:

```
active_families × 0.053 > new_families × onboarding_hours
```

| Growth Rate | Onboard Hours | Crossover Point |
|-------------|--------------|----------------|
| 50/month | 3 hrs | ~2,800 families |
| 100/month | 3 hrs | ~5,700 families |
| 200/month | 3 hrs | ~11,300 families |
| 500/month | 3 hrs | ~28,300 families |

With 3-hour onboarding, panel doesn't dominate until **Year 4-6 at moderate growth rates**. At 6-hour onboarding, it may never dominate at realistic growth rates.

---

## Long-Term Growth Projections (3 hrs/onboard, 2.5% churn — see note below)

### Slow & Steady: 50 new families/month

| Year | Active Families | FSRs Needed | Notes |
|------|----------------|-------------|-------|
| 1 | ~450 | 2 | Onboarding-bound |
| 3 | ~1,000 | 2 | Onboarding-bound |
| 5 | ~1,500 | 2 | Approaching steady state |
| 10 | ~1,800 | 2 | Steady state |

Steady state: ~2,000 families (50 new ≈ 50 churned at 2.5%)

### Moderate: 100 new families/month

| Year | Active Families | FSRs Needed | Notes |
|------|----------------|-------------|-------|
| 1 | ~900 | 3 | Onboarding-bound |
| 3 | ~2,200 | 3 | Onboarding-bound |
| 5 | ~3,200 | 3-4 | Onboarding still dominant |
| 10 | ~3,700 | 4 | Approaching steady state |

Steady state: ~4,000 families

### Aggressive: 200 new families/month

| Year | Active Families | FSRs Needed | Notes |
|------|----------------|-------------|-------|
| 1 | ~1,800 | 5 | Onboarding-bound |
| 3 | ~4,400 | 5-6 | Onboarding-bound |
| 5 | ~6,000 | 6 | Panel approaching 25% |
| 10 | ~7,400 | 7 | Steady state near |

Steady state: ~8,000 families

### Health Plan Scale: 500 new families/month

| Year | Active Families | FSRs Needed | Notes |
|------|----------------|-------------|-------|
| 1 | ~4,500 | 11 | Onboarding-bound |
| 3 | ~10,500 | 12-13 | Onboarding-bound |
| 5 | ~14,000 | 14 | Panel becoming meaningful |
| 10 | ~17,500 | 16 | Panel binding in late years |

Steady state: ~20,000 families

---

## The Churn Model — A Critical Assumption to Revisit

### Why 2% Monthly Churn Is Probably Too Low

Our customers have a structural "shelf life." This is not like a SaaS product where a customer churns due to dissatisfaction — it's the nature of the care journey:

- Families typically join the platform **3-5 years before** the parent passes away or enters full-time facility care
- When that event happens, the customer relationship ends (structural churn)
- This is unavoidable, not something better service prevents

### Implied Monthly Churn by Average Care Journey Length

| Average Care Journey | Monthly Churn Needed | Comment |
|----------------------|---------------------|---------|
| 2.5 years (30 months) | ~3.3% | Families that join late in journey |
| 3 years (36 months) | ~2.8% | Conservative estimate |
| 4 years (48 months) | ~2.1% | Moderate estimate |
| 5 years (60 months) | ~1.7% | Optimistic estimate |
| Our previous model | 2% | Implied ~4-year journey — probably too long |

**Recommended assumption: 2.5-3% monthly churn** — accounting for both structural end-of-journey churn and a small amount of voluntary churn (cost, dissatisfaction, care transferred to facility).

### Impact on Steady-State Active Families

At constant 100 new/month:

| Monthly Churn | Steady State Families | Revenue @ $100/mo |
|--------------|----------------------|------------------|
| 1.5% | ~5,600 | $560K MRR |
| 2.0% | ~4,200 | $420K MRR |
| 2.5% | ~3,400 | $340K MRR |
| 3.0% | ~2,800 | $280K MRR |

**Key implication:** Higher realistic churn means you need a higher sustained new-family rate just to maintain (not grow) your base. The business is more of a "treadmill" than a pure compounding growth story — which is actually fine, it just means **acquisition and onboarding throughput are always important**, even at maturity.

### Two-Component Churn Model (Better Accuracy)

Rather than one blended churn rate, model churn as two components:

```
monthly_churn_rate = structural_churn + voluntary_churn

Where:
  structural_churn = 1 / (avg_care_journey_months)
  voluntary_churn = 0.5-1.0% (dissatisfaction, cost, competition)
```

At 4-year average journey + 0.75% voluntary = **2.1 + 0.75 = ~3% total monthly churn**

---

## Strategic Implications

### 1. Onboarding Throughput Is the Growth Lever
- Reducing onboarding from 6 hrs to 3 hrs doubles your onboarding capacity with the same team
- AI-guided onboarding (Clicky-style) is the highest-ROI investment in Years 1-3
- Not just a cost reduction — it's a **growth rate multiplier**

### 2. Higher Churn Makes the Math Harder — But Manageable
- At 3% monthly churn, you need 67% more new families to achieve the same steady state as at 2%
- This puts more pressure on acquisition and the health plan partnership channel
- Monthly onboarding target should be set against churn: `target_new_per_month > churn_rate × desired_active_families`

### 3. LTV Is Capped
- At 3% monthly churn: average customer lifetime = ~33 months = ~$3,300 per family at $100/mo
- LTV should never be modeled as open-ended — always cap at implied care journey length
- This lowers LTV:CAC targets to more modest levels (~2-3x is realistic, not 10x)

### 4. The Business Needs Steady Intake to Survive
- Unlike SaaS, you can't "rest on your laurels" with a large installed base
- At 3% churn, a 5,000-family base loses ~150 families/month
- You need to permanently maintain ~150+ new families/month just to stay flat
- This means the health plan channel isn't optional — it's how you maintain scale without spending all your energy on acquisition

---

## Summary: The Simple Operating Model

For Years 1-3, the business can be modeled simply:

```
FSRs needed = (new_families/month × 3-6 hrs) ÷ 160 hrs + 1 buffer

Revenue = active_families × monthly_price

Active families grows until: new_families/month = churn_rate × active_families
  → Steady state = new_families/month ÷ churn_rate
```

Everything else (panel efficiency, phase scaling, capacity planning) is second-order until you have 5,000+ active families.

---

*Key takeaway: Hire for onboarding. Optimize onboarding. Build the AI guide. The panel takes care of itself until you're well past 5,000 families.*
