# Pricing, Ramp Rates & Price Elasticity

*Captured: 2026-04-08 | Source: Blake late-night thinking*

---

## The Pricing Problem

We're struggling to find the right price point because there are competing forces:

1. **Higher price** → more revenue per family → fewer families needed for break-even → but harder to acquire customers and slower ramp
2. **Lower price** → faster adoption → bigger addressable market → but need way more families and tighter unit economics
3. **Our costs are real** — FSRs at $125K, onboarding at 3-6 hours of human time. We can't price below our variable costs.

---

## Price Elasticity Thinking

### What We're Selling vs. Comparables

| Category | Monthly Cost | What They Get |
|----------|-------------|---------------|
| **Streaming (Netflix)** | $15 | Entertainment |
| **Gym membership** | $50 | Fitness |
| **Financial apps (Mint, YNAB)** | $10-15 | Budget tracking |
| **Care.com premium** | $40 | Caregiver search |
| **Life Alert** | $50 | Emergency button |
| **Wellthy (employer-paid)** | ~$100-150 PEPM | Human care coordinator |
| **Elder law attorney** | $300-500/hr | Legal advice |
| **Geriatric care manager** | $100-250/hr | Professional care management |
| **In-home aide** | $6,500/mo | Physical care |
| **Assisted living** | $5,900/mo | Facility care |

### Key Insight
We're not competing with Netflix. We're competing with:
- The family member who quits their job to manage care (opportunity cost: $4-8K/month in lost wages)
- A geriatric care manager ($200/hr, maybe $1,000-2,000/month if used regularly)
- The chaos of not having coordination (ER visits at $3K+ each, duplicated tests, missed medications)

At $149/month, we're 1/10th the cost of a professional care manager and we're available 24/7 through AI.

---

## Realistic Ramp Rates

### What Does "New Families Per Month" Actually Look Like?

**Year 1 reality check — direct-to-consumer:**
- Month 1-3: 5-15 families (friends, family, word of mouth, initial marketing)
- Month 4-6: 15-30 families (referral engine starting, content marketing, local partnerships)
- Month 7-12: 30-75 families (paid acquisition, physician referrals, community partnerships)
- **Year 1 total: ~300-500 families** (realistic for self-funded D2C)

**Years 2-3 organic growth:**
- Proven playbook from Year 1, expanding referral networks and small sales team
- 150-250 families/month from combined organic channels (referrals, content, community partnerships)
- Health plan partnerships are a Year 4+ accelerant, not a Year 2 dependency
- Health plan sales cycles are 6-18 months — start conversations in Year 2, close in Year 3+

**Comparable ramp rates:**
- Honor (home care platform): took 2+ years to reach meaningful scale
- Wellthy: grew primarily through employer channel, not D2C
- Most B2C health startups: 5-10% month-over-month growth is strong
- At 8% MoM growth starting from 20 families: ~60 by month 12, ~160 by month 24

### The Honest Ramp Model

| Month | Conservative | Moderate | With Health Plan Partner |
|-------|-------------|----------|------------------------|
| 3 | 30 | 50 | 50 |
| 6 | 80 | 150 | 200 |
| 12 | 250 | 500 | 800 |
| 18 | 450 | 900 | 2,000 |
| 24 | 700 | 1,500 | 4,000 |
| 36 | 1,200 | 3,000 | 8,000+ |

These are cumulative active families, assuming 1.5-2% monthly churn.

---

## Price Elasticity Scenarios

### The Core Trade-Off

| Price | Estimated Adoption Speed | Year 1 Families | Year 1 Revenue | Variable Cost/Family | Margin |
|-------|------------------------|-----------------|----------------|---------------------|--------|
| $79/mo | Fast — broad market | 400-600 | $300-400K | ~$40-60 | Tight |
| $149/mo | Moderate — mid market | 250-400 | $400-550K | ~$40-60 | Healthy |
| $249/mo | Slower — premium | 150-250 | $400-550K | ~$40-60 | Strong |
| $499/mo | Very slow — concierge | 50-100 | $300-450K | ~$60-80 | Very strong |

**Observation:** Revenue in Year 1 is surprisingly similar across price points because higher prices slow adoption. The difference shows up in Year 2-3 when the compounding base matters more.

### Variable Cost Floor

Before pricing, we need to know our floor — what does it cost to serve one family per month?

| Component | Low (AI-heavy) | Mid | High (Human-heavy) |
|-----------|----------------|-----|---------------------|
| FSR allocation | $15 | $30 | $60 |
| AI/cloud | $3 | $5 | $10 |
| Infrastructure | $3 | $4 | $5 |
| Payment processing (3%) | $2-5 | $4-7 | $8-15 |
| **Total variable** | **$23** | **$43** | **$83** |

At $79/month with a $43 variable cost, contribution margin is $36/family.
At $149/month, contribution margin is $106/family.
At $249/month, contribution margin is $206/family.

**Break-even families** (at $150K/month fixed costs — Phase 1):
- $79 price → need ~4,200 families
- $149 price → need ~1,400 families
- $249 price → need ~730 families

---

## Proposed Tiered Approach

### Tier 1: "Connected" — $79/month
- AI assistant only (no dedicated FSR)
- Connected to bank portals and healthcare systems
- Family coordination dashboard
- Automated alerts and reminders
- Self-serve onboarding (AI-guided, no human)
- **Target:** Broad market, early-stage caregiving families
- **Variable cost:** ~$15-20/family (mostly AI/infra, no FSR allocation)
- **Margin:** ~$55-60/family

### Tier 2: "Supported" — $149/month
- Everything in Connected
- Shared FSR support (pooled, not dedicated)
- Human onboarding (guided setup)
- Monthly check-in
- Escalation to human for complex issues
- **Target:** Active caregiving families, moderate complexity
- **Variable cost:** ~$40-50/family
- **Margin:** ~$100/family

### Tier 3: "Managed" — $299/month
- Everything in Supported
- Dedicated FSR relationship
- Quarterly care plan reviews
- Proactive monitoring and outreach
- Financial advisory access
- Medical guidance consultations
- **Target:** Complex care situations, higher-net-worth families
- **Variable cost:** ~$80-100/family
- **Margin:** ~$200/family

### Why This Works
- Tier 1 is the **growth engine** — low cost, high volume, gets families in the ecosystem
- Tier 2 is the **workhorse** — where most revenue comes from
- Tier 3 is the **margin driver** — high value, high touch, high margin
- Families naturally upgrade as care gets more complex over time

---

## What We Need to Validate

- [ ] Would families pay $79/month for an AI-only tier? Or is the human touch required for trust?
- [ ] What's the actual conversion rate from Tier 1 → Tier 2 as care complexity increases?
- [ ] Can we actually deliver Tier 1 with near-zero human time? Or does every family need some onboarding?
- [ ] What's the health plan PEPM they'd subsidize? ($50? $100? $150?)
- [ ] Do families comparison-shop this, or is it a "we need help NOW" purchase with low price sensitivity?

---

*Late-night thinking. Needs modeling in the financial tool with these tier assumptions.*
