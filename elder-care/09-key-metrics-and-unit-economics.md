# Key Metrics, Unit Economics, and Financial Drivers

*Prepared: 2026-04-08 | Updated: 2026-04-09*

## Executive Summary

The core economic lever in this business is **human time per family per month**. AI handles ~95% of routine retrieval, monitoring, and coordination work, allowing each FSR to manage a panel of **400 families in steady state** (with a long-term target of scaling toward 1,000 as the platform matures). This is what separates us from traditional care coordination where one coordinator handles 30-50 families.

**Key numbers at our current model assumptions ($249/month pricing):**

| Metric | Value |
|---|---|
| Contribution margin per family | ~$206/month |
| Variable cost per family | ~$43/month |
| Break-even families (Phase 1 costs) | ~730 |
| LTV:CAC ratio | 10.4x |
| Target monthly churn | 2% (~21.5% annual) |

**The three things that matter most:**
1. **Onboarding hours per family** — at 6 hours, this is the dominant cost driver and hiring trigger during growth. Reducing it via AI-guided onboarding is the single highest-leverage improvement.
2. **Monthly churn rate** — 1.67% is structural (5-year care lifecycle). Keeping voluntary churn to ~0.33% means the product is working.
3. **FSR panel capacity** — 400 families per service FSR is our current target. Every improvement in AI automation pushes this higher.

This document provides the detailed metric definitions, benchmarks, and analysis below.

---

## Modeling Assumptions Used in This Report

The analysis below uses the company notes plus a small number of explicit assumptions where the notes were directional rather than numeric.

### Given assumptions from founder notes

- Engineers: **$250K fully loaded each**
- FSRs: **$125K fully loaded each**
- Org management: **$200K fully loaded each**
- Office / infrastructure baseline: **$10K/month**, scaling upward with footprint
- Onboarding time: **6 human hours per new family** (conservative; AI-guided onboarding could reduce to 3 hours)
- Steady-state panel ratio: **1 FSR per 400 families** (current target; long-term aspiration of 1,000 as AI matures)
- AI handles roughly **95% of total family-management work**

### Additional operating assumptions used for modeling

These are not “truth”; they are working assumptions that should be validated with pilots.

- Initial product team: **4 engineers**, rising to 6+ as the platform scales
- Ops/compliance/admin: **1 FTE equivalent early**, adding with scale
- Average monthly AI/cloud/tooling cost per family: **$8 at <1,000 families**, improving to **$5-$6** at scale
- Shared infrastructure burden per family at scale: **~$4/family/month**
- Payment processing / bad debt reserve: **~3% of revenue**
- CAC for direct-to-consumer acquisition: modeled at **$600 per family** for planning purposes
- Average steady-state human time: **~0.06 hours per family per month** from panel coverage alone (3.6 minutes), plus targeted outreach and escalations embedded in the 1:1,000 staffing model

### Important caveat

This is a planning model, not an audited forecast. The two assumptions that matter most to validate in a real pilot are:

1. **Actual onboarding hours per family**
2. **Actual steady-state FSR capacity and escalation rate**

If either of those moves materially in the wrong direction, the economics change fast.

---

## 1) Metric Definitions

Below are the core metrics the business should use. For each one, the point is not just definitional clarity; it is operational discipline.

### A. Revenue metrics

| Metric | Formula | Unit | Why it matters | Target / benchmark |
|---|---|---:|---|---|
| ARPU / Average Revenue per Family per Month | Monthly subscription + service revenue / active families | $/family/month | Core monetization measure; anchors unit economics | Target blended ARPU **$199-$299** DTC; premium tier **$499+** |
| MRR | Active families × blended monthly revenue per family | $/month | Most useful monthly top-line measure | Must grow faster than fixed burn |
| ARR | MRR × 12 | $/year | Useful for fundraising/strategy comparisons, though this is not pure SaaS | Healthy only if backed by retention |
| Revenue per tier | Tier revenue / families in that tier | $/family/month | Shows mix shift and pricing power | Watch premium mix and payer-subsidized mix |
| Gross revenue per family | Subscription revenue before refunds, scholarships, payment losses | $/family/month | Reveals true customer willingness to pay | Track separately from net revenue |
| Net revenue per family | Gross revenue - discounts - refunds - bad debt - processing fees | $/family/month | Better measure for actual economics | Target within **90-97%** of gross |

#### Notes on benchmarks
Healthcare navigation, concierge support, and chronic-care-adjacent services often support higher price points than consumer SaaS because the value at stake is large: avoided time, avoided mistakes, fewer crises, and emotional relief. For a family service handling financial, medical, and care coordination, **$199-$299/month is reasonable mid-market pricing** if trust and usefulness are real. **$99** may work only as a lighter-touch tier or subsidized offering.

### B. Operational metrics

| Metric | Formula | Unit | Why it matters | Target / benchmark |
|---|---|---:|---|---|
| **Human time per family per month** | Total human labor hours spent on active families in month / active families | Hours/family/month | **Primary operating metric**; compressing this is the whole AI strategy | Mature target: **<0.10 hr**; excellent: **0.05-0.08 hr** |
| Human time per family per year | Monthly human time × 12 | Hours/family/year | Helps price long-run service burden | Target **<1.2 hours/year** steady state excluding onboarding |
| Onboarding time per family | Total human hours spent onboarding / families onboarded | Hours/new family | Main growth bottleneck and early variable cost driver | Baseline **3.0 hours**; target **<2.0** over time |
| Steady-state monitoring time | Non-onboarding human hours / active families | Hours/family/month | Reveals whether service model is drifting upward | Target **0.03-0.08 hr** |
| FSR-to-family ratio | Active families / account FSRs | Families per FSR | Single best capacity metric after human time | Early acceptable: **300-700**; mature target: **1,000+** |
| Human outreach rate | Families with ≥1 human interaction in month / active families | % | Indicates case complexity and AI exception rate | Baseline planning assumption **5%** |
| Average handle time (AHT) | Human interaction minutes / human interactions | Minutes per interaction | Important if outreach rate rises | Target **30-60 min** for standard issues |
| First-response time | Median time from family request to first meaningful response | Minutes or hours | Strong trust metric; especially important in care | Same-day for normal, <1 hour for urgent |

#### Why the core metric matters so much
If human time per family per month rises from **0.06 to 0.20 hours**, the model begins to behave more like a labor business than a software-amplified business. At 10,000 families, that difference is **600 hours vs 2,000 hours per month** — effectively the difference between a few FSRs and an entire department.

### C. Growth metrics

| Metric | Formula | Unit | Why it matters | Target / benchmark |
|---|---|---:|---|---|
| New families per month | Count of newly activated paying families | Families/month | Top funnel output; basis for staffing and cash modeling | Modeled cases: **50 / 100 / 200** |
| Monthly churn rate | Families lost in month / starting families | %/month | Biggest long-term growth governor | Good: **<2%**; workable: **2-3%**; risky: **>4%** |
| Annual churn rate | 1 - (1 - monthly churn)^12 | %/year | More intuitive for investors/operators | 2% monthly ≈ **21.5% annual**; 3% monthly ≈ **30.6% annual** |
| Net family growth | New families - churned families | Families/month | True installed-base growth | Must remain strongly positive through scale-up |
| CAC | Sales + marketing spend / new families acquired | $/family | Determines payback and capital needs | DTC target **<$600-$800**; payer channels should be lower |

### D. Unit economics metrics

| Metric | Formula | Unit | Why it matters | Target / benchmark |
|---|---|---:|---|---|
| Variable cost per family | FSR variable labor + AI/cloud + support tooling + payment fees | $/family/month | Defines contribution margin | Mature target **$25-$35** |
| Contribution margin per family | Net revenue per family - variable cost per family | $/family/month | Cash available to absorb fixed costs | Positive at all paid tiers; ideally **>$150** at core tier |
| Gross margin | Contribution margin / net revenue | % | Shows whether model behaves like software-amplified service | Target **75-90%** depending on tier |
| LTV | Contribution margin per family / monthly churn | $ | Most useful retention-adjusted value measure | Must materially exceed CAC |
| LTV:CAC ratio | LTV / CAC | x | Standard efficiency measure | Target **>3x** |
| Payback period | CAC / monthly contribution margin | Months | Key self-financing metric | Target **<6 months**, acceptable **<12** |

### E. Efficiency and reliability metrics

| Metric | Formula | Unit | Why it matters | Target / benchmark |
|---|---|---:|---|---|
| AI automation rate | Tasks completed end-to-end by AI / total tasks | % | Direct read on product leverage | Target **90-95%+** |
| AI-to-human handoff rate | Cases requiring human intervention / total cases | % | Reverse side of automation; should trend downward | Target **<10%**, ideally **~5%** |
| Platform uptime | Time core service available / total scheduled time | % | Trust business; downtime is reputationally costly | Target **99.9%+** |
| Data sync freshness | Median age of connected data when requested | Minutes/hours | Families need current facts, not stale snapshots | Health/finance critical connections ideally **<24h**, priority events faster |

---

## 2) Churn Analysis

### What churn will actually look like in this business

This business will not churn like a standard consumer app. A meaningful share of churn is **structural** and may even reflect mission completion rather than product failure.

### Likely churn drivers

1. **Death / end of care journey**  
   The parent dies, estate matters conclude, and the platform is no longer needed.
2. **Transition to facility-based or fully managed care**  
   A family may move from distributed family management to an institutional model with less need for active coordination.
3. **Dissatisfaction / trust failure**  
   The platform fails to deliver clarity, reliability, empathy, or action.
4. **Financial pressure**  
   The family no longer sees enough value relative to monthly cost.
5. **Competition or substitution**  
   Another sibling takes over, a care manager is hired directly, or a payer-sponsored alternative appears.

### Expected lifetime on platform

The founder notes suggest a likely care journey of **3-7 years**. That is directionally plausible. But actual paying lifetime will depend on when the family enters the journey.

A practical planning framework:

- **Early-entry family**: enters after diagnosis or first warning signs → **36-72 months**
- **Crisis-entry family**: enters after hospitalization, fall, or acute transition → **18-36 months**
- **Late-stage family**: enters during high-acuity decline → **12-24 months**

That implies a blended expected customer life of roughly **30-50 months**, which corresponds to monthly churn of about **2-3.3%**.

### Benchmark framing

Comparable benchmarks come from a mix of categories rather than one perfect analog:

- Consumer subscription businesses: often **3-6%+ monthly churn**
- High-trust B2C health navigation / concierge services: often materially lower when value is clear
- Services businesses embedded in a real ongoing workflow can sustain better retention than ordinary SaaS because switching is painful

For this business, the right benchmark is not “best consumer SaaS churn”; it is “how much avoidable churn remains after accounting for life-stage churn.”

### Suggested churn targets

- **Excellent:** 1.5-2.0% monthly
- **Good / workable:** 2.0-3.0% monthly
- **Warning zone:** 3.0-4.0% monthly
- **Broken economics:** >4.0% monthly unless price is much higher

### Why churn matters so much financially

Example at $299/month with a monthly contribution margin of about **$268**:

- At **2% monthly churn**, LTV ≈ **$13.4K** before CAC
- At **3% monthly churn**, LTV ≈ **$8.9K** before CAC
- At **5% monthly churn**, LTV ≈ **$5.4K** before CAC

The business can survive moderate churn because pricing is meaningful and variable cost is low. But high churn breaks compounding. It forces a perpetual onboarding treadmill.

### Early-stage vs mature churn

Early churn usually looks worse for three reasons:

1. Product gaps are still obvious
2. Wrong-fit customers get acquired
3. Trust systems and onboarding playbooks are immature

A realistic expectation is:

- **Pilot / early stage:** 3-5% monthly churn is possible
- **After process maturity:** 2-3% monthly churn should be the operating goal
- **Mature, payer-supported, well-targeted product:** 1.5-2.5% may be achievable

The company should explicitly split churn into:

- **Structural churn**: death, facility transition, estate closure
- **Controllable churn**: dissatisfaction, value perception, trust issues, onboarding failure

That distinction matters because only the second category should drive performance accountability.

---

## 3) Unit Economics Deep Dive

### Cost to acquire, onboard, and maintain one family

A simple bottom-up economics stack per family looks like this.

#### A. Acquisition cost

Planning assumption: **$600 CAC** direct-to-consumer.  
This should include paid acquisition, content, referral incentives, and intake labor allocated per converted family.

#### B. Onboarding cost

Onboarding requires **3 hours of human time**. At an FSR fully loaded monthly cost of **$10,417** and ~160 work hours/month, the implied hourly cost is about **$65/hour**.

So baseline onboarding labor cost is:

- **3.0 hours × $65 ≈ $195 per family**

Add some tooling / setup overhead, and a practical planning figure is **$200-$250 per onboarded family**.

#### C. Ongoing monthly variable cost per family

At mature scale, a reasonable planning estimate is:

| Component | Estimated monthly cost/family |
|---|---:|
| FSR steady-state labor allocation | $10.42 |
| AI/cloud compute and agent tooling | $8.00 |
| Shared infrastructure / support systems | $4.00 |
| Payment processing / billing reserve | ~3% of revenue |

That yields approximate monthly variable cost by price point:

| Price | Variable cost/family/month | Contribution margin/family/month | Gross margin |
|---|---:|---:|---:|
| $99 | $25.39 | $73.61 | 74.4% |
| $199 | $28.39 | $170.61 | 85.7% |
| $299 | $31.39 | $267.61 | 89.5% |
| $499 | $37.39 | $461.61 | 92.5% |

### Contribution margin at different price points

This table makes the strategic point clear: **the model works much better at $199+ than at $99**.

- **$99/month** can be profitable on a contribution basis, but it leaves little room to absorb fixed payroll and brand-quality service.
- **$199/month** is the likely minimum attractive core tier.
- **$299/month** is strong for a DTC flagship offer.
- **$499/month** creates excellent economics for complex families or premium concierge service.

### LTV by retention level

Using the standard planning formula:

**LTV = monthly contribution margin / monthly churn**

And showing a net view after subtracting **$600 CAC**:

| Price | Net LTV @ 1% churn | Net LTV @ 2% churn | Net LTV @ 3% churn | Net LTV @ 5% churn |
|---|---:|---:|---:|---:|
| $99 | $6,761 | $3,081 | $1,854 | $872 |
| $199 | $16,461 | $7,931 | $5,087 | $2,812 |
| $299 | $26,161 | $12,781 | $8,320 | $4,752 |
| $499 | $45,561 | $22,481 | $14,787 | $8,632 |

### Payback period

**Payback period = CAC / monthly contribution margin**

| Price | Monthly CM | Payback on $600 CAC |
|---|---:|---:|
| $99 | $73.61 | 8.2 months |
| $199 | $170.61 | 3.5 months |
| $299 | $267.61 | 2.2 months |
| $499 | $461.61 | 1.3 months |

### When does a family become profitable?

If the company spends roughly **$600 CAC + $200 onboarding cost = $800 up front**, then profitability happens once cumulative contribution margin exceeds $800.

| Price | Monthly CM | Months to cover CAC + onboarding |
|---|---:|---:|
| $99 | $73.61 | ~10.9 months |
| $199 | $170.61 | ~4.7 months |
| $299 | $267.61 | ~3.0 months |
| $499 | $461.61 | ~1.7 months |

This is the central unit-economic insight: **below $199, the company can make money, but recovery is slower and the business becomes much more sensitive to churn and acquisition efficiency**.

---

## 4) Economies of Scale

### What changes as the platform scales?

| Active families | Likely characteristics | Main improvement | Main risk |
|---|---|---|---|
| 100 | Pilot / founder-led | Fast learning | Terrible absorption of fixed costs |
| 1,000 | Real operating business | Early FSR leverage visible | Onboarding systems strain |
| 5,000 | Multi-team company | Better AI, more repeatable ops | Quality control and management layers |
| 10,000 | Scaled platform | Brand trust, partner leverage | Compliance, incident management |
| 50,000 | Major category player | Distribution power, data flywheel | Geographic/regulatory complexity |

### Illustrative economics by scale

| Scale | Approx. steady-state account FSRs | Monthly FSR labor/family | Likely AI/cloud/family | Overall variable cost trend |
|---|---:|---:|---:|---|
| 100 families | 1 dedicated/generalist role | High | High | Worst economics |
| 1,000 families | 1 account FSR + onboarding pool | ~$10 | ~$8 | Economics begin to normalize |
| 5,000 families | 5 account FSRs + specialized onboarding | Stable to lower | ~$6 | Stronger gross margins |
| 10,000 families | 10 account FSRs + specialized teams | Potentially lower with better tooling | ~$5-$6 | Attractive mature model |
| 50,000 families | Full service org with management layers | Can improve in workflow efficiency | Negotiated infra savings | Margin partly offset by org complexity |

### What improves with scale

1. **FSR efficiency**  
   Better playbooks, better triage, and more structured escalation trees should reduce human time.
2. **AI quality**  
   More real-world interaction patterns improve prompts, tools, retrieval design, and exception handling.
3. **Onboarding speed**  
   More reusable connection templates and pre-built workflows should cut onboarding below 3 hours.
4. **Negotiating power**  
   Scale helps with vendors, data access partners, insurers, and possibly payment rails.
5. **Brand trust**  
   Families may convert faster when the company feels established and reputable.

### What gets harder with scale

1. **Quality control**  
   A small team can manually rescue issues. A large team needs systems.
2. **Hiring and training**  
   Going from 3 great FSRs to 30 is much harder than going from 0 to 3.
3. **Compliance and security**  
   The risk surface expands with every additional connection and state footprint.
4. **Geographic expansion**  
   Care ecosystems, provider relationships, and regulations vary by region.
5. **Management overhead**  
   At high scale, some productivity gains are eaten by leads, QA, training, and internal coordination.

### Key inflection points

- **~100 families:** prove retention and willingness to pay
- **~500 families:** prove onboarding throughput and early panel model
- **~1,000 families:** first credible sustainable operating unit
- **~5,000 families:** real company infrastructure required
- **~10,000 families:** payer partnerships and compliance maturity become strategic, not optional

---

## 5) Financial Scenarios (36-Month View)

The monthly models below assume disciplined hiring, the compensation assumptions above, 3-hour onboarding, and the target FSR ratios from the notes. These are scenario illustrations, not exact forecasts.

### Scenario A: Conservative

**Assumptions**
- New families/month: **50**
- Average price: **$299**
- Monthly churn: **3.0%**
- No major payer subsidy in first 3 years

**Result**
- Monthly operating break-even: **Month 14**
- Peak external capital required: **~$966K**
- End of Month 36 active families: **~1,110**

**Selected monthly cash flow points**

| Month | Active families | Revenue | Net cash flow | Cumulative cash |
|---|---:|---:|---:|---:|
| 1 | 50 | $7,475 | -$151,475 | -$151,475 |
| 6 | 278 | $76,817 | -$83,989 | -$702,282 |
| 12 | 510 | $147,222 | -$15,467 | -$960,305 |
| 14 | 579 | $167,972 | $4,728 | -$960,793 |
| 24 | 864 | $254,717 | $89,152 | -$427,999 |
| 36 | 1,110 | $329,302 | $95,194 | $740,115 |

**Team shape by stage**
- Early: 2 founders, 4 engineers, 1 ops, **3 FSRs**
- Around 1,000 families: 2 founders, 6 engineers, 2 ops, **4 FSRs**

### Scenario B: Moderate

**Assumptions**
- New families/month: **100**
- Average DTC price: **$249**
- Monthly churn: **2.5%**
- Health plan partnership beginning Month 13 adds roughly **$60 PMPM equivalent**

**Result**
- Monthly operating break-even: **Month 9**
- Peak external capital required: **~$706K**
- End of Month 36 active families: **~2,392**

**Selected monthly cash flow points**

| Month | Active families | Revenue | Net cash flow | Cumulative cash |
|---|---:|---:|---:|---:|
| 1 | 100 | $12,450 | -$167,533 | -$167,533 |
| 8 | 733 | $172,187 | -$12,929 | -$706,199 |
| 9 | 815 | $192,782 | $7,005 | -$699,194 |
| 18 | 1,464 | $442,341 | $185,418 | $172,523 |
| 24 | 1,821 | $554,193 | $295,098 | $1,677,008 |
| 36 | 2,392 | $732,827 | $459,848 | $6,315,783 |

**Team shape by stage**
- Early: 2 founders, 4 engineers, 1 ops, **5 FSRs**
- After 1,000 families: 2 founders, 6 engineers, 2 ops, **6 FSRs**
- By ~2,400 families: **7 FSRs**

### Scenario C: Aggressive

**Assumptions**
- New families/month: **200** from day one
- Average DTC price: **$199**
- Monthly churn: **2.0%**
- Multiple health plan partners beginning Month 13 add roughly **$80 PMPM equivalent**

**Result**
- Monthly operating break-even: **Month 9**
- Peak external capital required: **~$798K**
- End of Month 36 active families: **~5,168**

**Selected monthly cash flow points**

| Month | Active families | Revenue | Net cash flow | Cumulative cash |
|---|---:|---:|---:|---:|
| 1 | 200 | $19,900 | -$202,150 | -$202,150 |
| 8 | 1,492 | $279,706 | -$18,727 | -$798,486 |
| 9 | 1,663 | $313,912 | $14,447 | -$784,039 |
| 14 | 2,464 | $665,883 | $351,147 | $101,240 |
| 24 | 3,842 | $1,054,442 | $720,932 | $5,704,645 |
| 36 | 5,168 | $1,428,079 | $990,701 | $16,534,759 |

**Team shape by stage**
- Early: 2 founders, 4 engineers, 1 ops, **9 FSRs**
- Around 1,000+ families: 2 founders, 6 engineers, 2 ops, **10-11 FSRs**
- Around 5,000 families: 2 founders, 8 engineers, 4 ops, **14 FSRs**

### Interpretation of the scenarios

A surprising result is that the moderate and aggressive models break even faster than the conservative one despite heavier staffing. That is because the business has meaningful contribution margin per family; once acquisition and onboarding machine throughput is working, faster growth helps absorb fixed engineering and founder payroll.

### Key sensitivities

The biggest sensitivities are:

1. **Churn**: a 1-point monthly churn change matters a lot
2. **Onboarding hours**: if 3 hours becomes 5+, onboarding FSR needs jump
3. **Blended price**: $299 vs $199 changes everything
4. **Real FSR capacity**: 1:1,000 is a thesis, not yet a fact
5. **Timing and economics of payer partnerships**

---

## 6) The Metric Dashboard

The company should not try to monitor 50 things in real time. It should monitor the **10 that drive decisions**.

### Daily metrics

1. **Human time per family per month (rolling 30-day)**  
   The main operating truth. If this rises, margins and scalability erode.
2. **AI-to-human handoff rate**  
   Tells engineering whether the system is actually reducing human exception load.
3. **First-response time**  
   Trust and service quality metric.
4. **Platform uptime / critical incident count**  
   Reliability matters more here than in a normal consumer app.

### Weekly metrics

5. **New families onboarded**  
   Indicates top-of-funnel conversion and onboarding throughput.
6. **Onboarding hours per family**  
   Early warning on process drift and training gaps.
7. **Human outreach rate**  
   If this rises, case complexity or product failure may be increasing.
8. **Average handle time**  
   Useful paired with outreach rate; one without the other can mislead.

### Monthly metrics

9. **Monthly churn, split into structural vs controllable**  
   This is mandatory. Otherwise the team will misread retention.
10. **Contribution margin per family / gross margin**  
   Final financial proof that the model is behaving correctly.

### The #1 metric

If the company has to pick one number to optimize across product, operations, and finance, it should be:

## **Human time per family per month**

Why this one?

- It links directly to FSR capacity
- It determines variable cost per family
- It determines whether pricing tiers are viable
- It reflects whether the AI layer is actually valuable
- It compounds across scale more than almost any other operational lever

The AI team should be judged not on abstract model quality but on whether it lowers this metric **without hurting trust, safety, or response quality**.

---

## 7) Early Stage vs Mature Stage

### 100 families vs 10,000 families

At **100 families**, the company is economically fragile:

- Founders and engineers dominate cost structure
- One FSR may be underutilized but still required
- Brand trust is low and onboarding is manual
- Almost every family issue feels custom

At **10,000 families**, the business should be fundamentally different:

- Onboarding is templated and semi-automated
- FSR roles specialize into onboarding, account, escalations, QA
- AI workflows handle the overwhelming majority of standard retrieval and reminders
- Partnerships reduce CAC and improve revenue stability
- The company has bargaining power and data/process advantages

### Minimum viable sustainable scale

Based on the modeled cost structure, the company likely becomes sustainably viable around **700-1,200 active families**, depending on average price and churn.

Rule of thumb:

- At **$199 blended price**, aim for **1,000+ families** to feel safe
- At **$299 blended price**, **700-900 families** may be enough
- At **$99**, the business is unlikely to support the intended service level without subsidy or extreme automation

### Hiring triggers

Recommended operating triggers:

| Trigger | Suggested action |
|---|---|
| Onboarding queue >2 weeks or onboarding time >3.5 hours/family | Add onboarding FSR capacity or redesign workflow |
| Account panel exceeds 850-900 families per FSR for 2 consecutive months | Start hiring next account FSR |
| Human time per family >0.10 hours/month for 2 months | Product escalation: AI and workflow fix required |
| Controllable churn >2% monthly | Investigate onboarding, trust, and service failures |
| First-response time misses SLA repeatedly | Add support coverage or fix triage automation |
| Active families exceed 1,000 | Add engineering and ops depth; formalize QA/compliance |
| Active families exceed 5,000 | Add management layers, training, and dedicated compliance/security leadership |

---

## Appendix A: 36-Month Cash Flow — Conservative Scenario

| Mo. | Families | Revenue | Net cash flow | Cumulative cash |
|---:|---:|---:|---:|---:|
| 1 | 50 | $7,475 | -$151,475 | -$151,475 |
| 2 | 98 | $22,201 | -$137,143 | -$288,618 |
| 3 | 146 | $36,485 | -$123,241 | -$411,860 |
| 4 | 191 | $50,340 | -$109,757 | -$521,616 |
| 5 | 235 | $63,780 | -$96,677 | -$618,293 |
| 6 | 278 | $76,817 | -$83,989 | -$702,282 |
| 7 | 320 | $89,462 | -$71,682 | -$773,963 |
| 8 | 360 | $101,728 | -$59,744 | -$833,707 |
| 9 | 400 | $113,626 | -$48,164 | -$881,871 |
| 10 | 438 | $125,168 | -$36,931 | -$918,802 |
| 11 | 474 | $136,363 | -$26,036 | -$944,838 |
| 12 | 510 | $147,222 | -$15,467 | -$960,305 |
| 13 | 545 | $157,755 | -$5,216 | -$965,521 |
| 14 | 579 | $167,972 | $4,728 | -$960,793 |
| 15 | 611 | $177,883 | $14,374 | -$946,419 |
| 16 | 643 | $187,497 | $23,730 | -$922,689 |
| 17 | 674 | $196,822 | $32,806 | -$889,883 |
| 18 | 703 | $205,867 | $41,609 | -$848,274 |
| 19 | 732 | $214,641 | $50,148 | -$798,126 |
| 20 | 760 | $223,152 | $58,431 | -$739,695 |
| 21 | 788 | $231,407 | $66,466 | -$673,229 |
| 22 | 814 | $239,415 | $74,259 | -$598,970 |
| 23 | 839 | $247,183 | $81,819 | -$517,151 |
| 24 | 864 | $254,717 | $89,152 | -$427,999 |
| 25 | 888 | $262,026 | $96,265 | -$331,734 |
| 26 | 912 | $269,115 | $103,165 | -$228,569 |
| 27 | 934 | $275,991 | $109,857 | -$118,712 |
| 28 | 956 | $282,662 | $116,349 | -$2,363 |
| 29 | 978 | $289,132 | $122,646 | $120,283 |
| 30 | 998 | $295,408 | $128,754 | $249,037 |
| 31 | 1,018 | $301,496 | $67,946 | $316,982 |
| 32 | 1,038 | $307,401 | $73,732 | $390,715 |
| 33 | 1,057 | $313,129 | $79,345 | $470,060 |
| 34 | 1,075 | $318,685 | $84,790 | $554,850 |
| 35 | 1,093 | $324,074 | $90,071 | $644,921 |
| 36 | 1,110 | $329,302 | $95,194 | $740,115 |

## Appendix B: 36-Month Cash Flow — Moderate Scenario

| Mo. | Families | Revenue | Net cash flow | Cumulative cash |
|---:|---:|---:|---:|---:|
| 1 | 100 | $12,450 | -$167,533 | -$167,533 |
| 2 | 198 | $37,039 | -$143,735 | -$311,268 |
| 3 | 293 | $61,013 | -$120,531 | -$431,799 |
| 4 | 385 | $84,387 | -$97,907 | -$529,706 |
| 5 | 476 | $107,178 | -$75,849 | -$605,555 |
| 6 | 564 | $129,398 | -$54,342 | -$659,897 |
| 7 | 650 | $151,063 | -$33,373 | -$693,271 |
| 8 | 733 | $172,187 | -$12,929 | -$706,199 |
| 9 | 815 | $192,782 | $7,005 | -$699,194 |
| 10 | 895 | $212,863 | $26,440 | -$672,754 |
| 11 | 972 | $232,441 | $45,390 | -$627,364 |
| 12 | 1,048 | $251,530 | -$2,864 | -$630,229 |
| 13 | 1,122 | $335,236 | $80,393 | -$549,835 |
| 14 | 1,194 | $357,755 | $102,475 | -$447,360 |
| 15 | 1,264 | $379,711 | $124,005 | -$323,355 |
| 16 | 1,332 | $401,119 | $144,997 | -$178,359 |
| 17 | 1,399 | $421,991 | $165,463 | -$12,895 |
| 18 | 1,464 | $442,341 | $185,418 | $172,523 |
| 19 | 1,527 | $462,182 | $204,875 | $377,398 |
| 20 | 1,589 | $481,528 | $223,844 | $601,242 |
| 21 | 1,650 | $500,390 | $242,340 | $843,582 |
| 22 | 1,708 | $518,780 | $260,373 | $1,103,955 |
| 23 | 1,766 | $536,710 | $277,955 | $1,381,910 |
| 24 | 1,821 | $554,193 | $295,098 | $1,677,008 |
| 25 | 1,876 | $571,238 | $311,812 | $1,988,821 |
| 26 | 1,929 | $587,857 | $328,109 | $2,316,930 |
| 27 | 1,981 | $604,060 | $343,998 | $2,660,927 |
| 28 | 2,031 | $619,859 | $349,073 | $3,010,000 |
| 29 | 2,080 | $635,262 | $364,177 | $3,374,177 |
| 30 | 2,128 | $650,281 | $378,904 | $3,753,081 |
| 31 | 2,175 | $664,924 | $393,263 | $4,146,344 |
| 32 | 2,221 | $679,201 | $407,262 | $4,553,606 |
| 33 | 2,265 | $693,121 | $420,912 | $4,974,519 |
| 34 | 2,309 | $706,693 | $434,221 | $5,408,739 |
| 35 | 2,351 | $719,925 | $447,196 | $5,855,935 |
| 36 | 2,392 | $732,827 | $459,848 | $6,315,783 |

## Appendix C: 36-Month Cash Flow — Aggressive Scenario

| Mo. | Families | Revenue | Net cash flow | Cumulative cash |
|---:|---:|---:|---:|---:|
| 1 | 200 | $19,900 | -$202,150 | -$202,150 |
| 2 | 396 | $59,302 | -$164,332 | -$366,482 |
| 3 | 588 | $97,916 | -$127,270 | -$493,752 |
| 4 | 776 | $135,758 | -$90,950 | -$584,702 |
| 5 | 961 | $172,842 | -$55,356 | -$640,058 |
| 6 | 1,142 | $209,186 | -$87,121 | -$727,180 |
| 7 | 1,319 | $244,802 | -$52,579 | -$779,759 |
| 8 | 1,492 | $279,706 | -$18,727 | -$798,486 |
| 9 | 1,663 | $313,912 | $14,447 | -$784,039 |
| 10 | 1,829 | $347,434 | $46,958 | -$737,081 |
| 11 | 1,993 | $380,285 | $78,819 | -$658,262 |
| 12 | 2,153 | $412,479 | $99,626 | -$558,636 |
| 13 | 2,310 | $622,534 | $308,729 | -$249,907 |
| 14 | 2,464 | $665,883 | $351,147 | $101,240 |
| 15 | 2,614 | $708,366 | $392,715 | $493,955 |
| 16 | 2,762 | $749,998 | $433,453 | $927,408 |
| 17 | 2,907 | $790,798 | $473,375 | $1,400,783 |
| 18 | 3,049 | $830,782 | $512,499 | $1,913,282 |
| 19 | 3,188 | $869,967 | $540,424 | $2,453,707 |
| 20 | 3,324 | $908,367 | $577,999 | $3,031,706 |
| 21 | 3,457 | $946,000 | $614,823 | $3,646,529 |
| 22 | 3,588 | $982,880 | $650,909 | $4,297,438 |
| 23 | 3,717 | $1,019,022 | $686,275 | $4,983,713 |
| 24 | 3,842 | $1,054,442 | $720,932 | $5,704,645 |
| 25 | 3,965 | $1,089,153 | $754,897 | $6,459,542 |
| 26 | 4,086 | $1,123,170 | $777,766 | $7,237,308 |
| 27 | 4,204 | $1,156,507 | $810,386 | $8,047,694 |
| 28 | 4,320 | $1,189,177 | $842,353 | $8,890,047 |
| 29 | 4,434 | $1,221,193 | $873,681 | $9,763,727 |
| 30 | 4,545 | $1,252,569 | $904,382 | $10,668,110 |
| 31 | 4,654 | $1,283,318 | $934,470 | $11,602,579 |
| 32 | 4,761 | $1,313,451 | $963,955 | $12,566,534 |
| 33 | 4,866 | $1,342,982 | $992,851 | $13,559,385 |
| 34 | 4,969 | $1,371,923 | $1,021,169 | $14,580,554 |
| 35 | 5,069 | $1,400,284 | $963,504 | $15,544,058 |
| 36 | 5,168 | $1,428,079 | $990,701 | $16,534,759 |

## Final Conclusions

1. **This can be a real business, not just a vision, if the service stays software-amplified.**
2. **$199-$299/month is the likely economic sweet spot** for a core DTC offer, with $499+ reserved for higher-touch families.
3. **The company should treat onboarding as its first scaling bottleneck** and invest heavily in compressing onboarding hours.
4. **Churn needs to be measured intelligently**; structural churn is not the same as product failure.
5. **Self-financing is plausible**, but only with hiring discipline, strong pricing, and a refusal to drift into labor-heavy bespoke service.
6. **The key decision variable for the entire company is human time per family per month**. That is the number the AI team, FSR team, and founders should all rally around.

If that metric stays low while trust and retention stay high, the company has a credible path to sustainability and long-run scale.
