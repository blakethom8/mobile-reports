# Elder Care Financial Model Foundation

*Working draft: 2026-04-08*

## Why This Exists

We got ahead of ourselves in the financial model.

This document is the reset point. It is meant to give us a cleaner shared language before we keep expanding the dashboard, the scenarios, or the staffing logic.

The goal here is simple:

- define the business in plain English
- define the core metrics in a MESI-ish structure
- separate onboarding work from ongoing service work
- define a simpler monthly waterfall
- separate a steady-state analysis from the 36-month ramp model

This is not an audited forecast. It is a working operating definition.

---

## First Principles

### 1. The company is not pure SaaS

This is a software-amplified service business. Families pay for a recurring service, but the economics only work if software keeps compressing human time.

### 2. Monthly is the default unit of management

Unless stated otherwise, our primary planning unit should be the month.

That means we want:

- monthly revenue rate
- monthly spend rate
- monthly onboarding demand
- monthly service demand
- monthly operating result

### 3. Separate stocks from flows

We should not mix these up.

- **Stocks** are point-in-time states, like `active families`
- **Flows** are monthly movements, like `new families`, `churned families`, `monthly revenue`, or `monthly spend`

### 4. Separate demand from capacity

Demand is what the business needs to deliver.
Capacity is what the current team can deliver.

Those are different concepts and should stay different in the model.

### 5. Separate onboarding FSRs from service FSRs in the base model

This is the biggest reset from the current model mechanics.

For the base model:

- **Onboarding FSRs** handle the work required to activate new families
- **Service FSRs** handle the ongoing work required to support active families

If we later want to model cross-training, swing capacity, or pooled utilization, that should be a later advanced layer, not the default mechanic.

---

## The Business in Three Layers

### 1. Demand Layer

This answers:

- how many new families are we adding each month?
- how many families are churning each month?
- how many active families do we have at the end of the month?

### 2. Service Delivery Layer

This answers:

- how much onboarding work do new families create?
- how much ongoing service work do active families create?
- how many onboarding FSRs and service FSRs are required?

### 3. Company Build Layer

This answers:

- how much fixed company spend do we carry?
- what engineering, management, compliance, and infrastructure cost base are we funding?
- how much monthly contribution do we need before the company becomes self-funding?

---

## Metric Taxonomy

We should organize the model metrics into three buckets:

1. **Cost metrics**
2. **Revenue metrics**
3. **Operational metrics**

This is simple enough to manage and covers the core business without trying to do everything at once.

---

## Cost Metrics

These should be defined first, because the company is trying to answer a monthly question:

**What are we spending per month, what are we earning per month, and when does the spread turn positive?**

| Metric | Definition | Formula / construction | Why it matters |
|---|---|---|---|
| **Monthly fixed spend rate** | Monthly spend that does not directly scale with family count | founders + engineering + product + management + compliance + office + fixed software + fixed infrastructure | This is the monthly burden the business must absorb before it is truly self-funding |
| **Monthly onboarding labor spend** | Monthly payroll cost for onboarding FSRs | onboarding FSR headcount x loaded monthly cost per onboarding FSR | This is the labor cost of growth |
| **Monthly service labor spend** | Monthly payroll cost for service FSRs | service FSR headcount x loaded monthly cost per service FSR | This is the labor cost of supporting the installed base |
| **Monthly AI / cloud spend** | Usage-linked technology cost | active families x AI/cloud cost per family, plus any usage-based tooling | This is the main non-labor variable delivery cost |
| **Monthly payment and billing spend** | Revenue-linked payment costs and reserves | payment processing + refunds + bad debt reserve | This keeps revenue and net cash more honest |
| **Monthly total variable spend** | Monthly spend that scales with customers or service load | onboarding labor + service labor + AI/cloud + payment/billing + other variable delivery costs | This is the cost to acquire and serve this month's demand |
| **Monthly total spend rate** | Full monthly spend burden | fixed spend + total variable spend | This is the total operating load of the business |
| **Monthly contribution after variable spend** | Revenue left after delivery costs but before fixed company costs | total monthly revenue - total variable spend | This tells us whether the service model itself is healthy |
| **Monthly operating result** | Profit or loss for the month | total monthly revenue - total monthly spend rate | This is the cleanest monthly scoreboard |
| **Capital required** | Peak funding gap before the company becomes self-funding | max cumulative cash deficit over the model horizon | This is the financing question the ramp model needs to answer |

### Cost Metric Rules

- Keep onboarding labor separate from service labor
- Keep fixed spend separate from variable spend
- Do not bury payment processing inside revenue unless explicitly stated
- Prefer monthly cost rates over annualized abstractions during planning

---

## Revenue Metrics

Revenue should stay simple in the base model.

| Metric | Definition | Formula / construction | Why it matters |
|---|---|---|---|
| **Recurring monthly revenue** | Monthly subscription revenue from active families | active families x monthly price per family | This is the core revenue engine |
| **Onboarding revenue** | One-time revenue from newly activated families | new families x onboarding fee | Useful if we charge a setup fee; should stay separate from recurring revenue |
| **Gross monthly revenue rate** | Total top-line revenue before revenue deductions | recurring revenue + onboarding revenue | This is the top of the monthly waterfall |
| **Net monthly revenue rate** | Revenue after payment losses, refunds, or similar deductions | gross monthly revenue - payment / refund deductions | Better proxy for what the company actually keeps |
| **ARPU / revenue per active family** | Monthly recurring revenue per active family | recurring revenue / active families | Helps compare pricing and customer mix |
| **Onboarding revenue per new family** | One-time activation revenue per family | onboarding revenue / new families | Useful if onboarding is monetized and should partially offset onboarding labor |

### Revenue Metric Rules

- Separate recurring revenue from onboarding revenue
- Prefer gross and net revenue as two different metrics
- Do not let onboarding fees hide weak recurring unit economics

---

## Operational Metrics

Operational metrics should be split into two sub-models:

1. **Demand model**
2. **Care / service model**

That is the simplest way to avoid muddled staffing math.

### A. Demand Model Metrics

| Metric | Definition | Formula / construction | Why it matters |
|---|---|---|---|
| **New families per month** | Newly activated paying families in the month | direct input or scenario output | This is the top-line growth driver |
| **Churned families per month** | Families lost in the month | active families at start of month x monthly churn rate | This is the offset to growth |
| **Net family adds** | Net growth in installed base | new families - churned families | This is the monthly change in family count |
| **Active families, end of month** | Families still on platform after adds and churn | prior active families + net family adds | This is the main stock variable |
| **Onboarding demand hours** | Total monthly onboarding work required | new families x onboarding hours per family | This creates onboarding staffing demand |
| **Service demand hours** | Total monthly service work required for the active base | active families x service hours per active family per month | This creates ongoing service staffing demand |

### B. Care / Service Model Metrics

| Metric | Definition | Formula / construction | Why it matters |
|---|---|---|---|
| **Productive onboarding hours per FSR / month** | Hours one onboarding FSR can actually spend onboarding in a month | monthly working hours - non-productive time | Capacity driver for onboarding team |
| **Productive service hours per FSR / month** | Hours one service FSR can actually spend on existing-family support in a month | monthly working hours - non-productive time | Capacity driver for service team |
| **Onboarding capacity per onboarding FSR** | New families one onboarding FSR can activate per month | productive onboarding hours / onboarding hours per family | Converts onboarding work into headcount |
| **Service families per service FSR** | Active families one service FSR can support | productive service hours / service hours per active family per month | Converts service work into headcount |
| **Required onboarding FSRs** | Onboarding headcount needed this month | onboarding demand hours / productive onboarding hours per onboarding FSR | Shows how growth pressure scales labor |
| **Required service FSRs** | Service headcount needed this month | service demand hours / productive service hours per service FSR | Shows how installed-base support scales labor |
| **Total FSR headcount** | Total frontline staffing needed | onboarding FSRs + service FSRs | Cleanest labor planning number once roles are separated |

### Operational Metric Rules

- Onboarding demand comes from `new families`
- Service demand comes from `active families`
- Onboarding FSRs and service FSRs are separate in the base model
- Do not use one blended `families per FSR` metric as the main staffing mechanic
- If we show a blended ratio, it should be a summary output, not a core input

---

## The Simpler Base Model

This is the model we should anchor first before we add more scenario complexity.

### Step 1. Demand model

```text
churned_families_t = active_families_(t-1) x churn_rate
net_adds_t = new_families_t - churned_families_t
active_families_t = active_families_(t-1) + net_adds_t
```

### Step 2. Workload model

```text
onboarding_demand_hours_t = new_families_t x onboarding_hours_per_family
service_demand_hours_t = active_families_t x service_hours_per_active_family_per_month
```

### Step 3. Staffing model

```text
onboarding_fsrs_t = onboarding_demand_hours_t / productive_onboarding_hours_per_fsr
service_fsrs_t = service_demand_hours_t / productive_service_hours_per_fsr
total_fsrs_t = onboarding_fsrs_t + service_fsrs_t
```

### Step 4. Revenue model

```text
recurring_revenue_t = active_families_t x monthly_price
onboarding_revenue_t = new_families_t x onboarding_fee
gross_revenue_t = recurring_revenue_t + onboarding_revenue_t
net_revenue_t = gross_revenue_t - revenue_deductions_t
```

### Step 5. Cost model

```text
onboarding_labor_cost_t = onboarding_fsrs_t x loaded_monthly_onboarding_fsr_cost
service_labor_cost_t = service_fsrs_t x loaded_monthly_service_fsr_cost
total_variable_spend_t = onboarding_labor_cost_t + service_labor_cost_t + ai_cloud_t + payment_t + other_variable_t
total_spend_t = fixed_spend_t + total_variable_spend_t
operating_result_t = net_revenue_t - total_spend_t
```

This is enough to answer the basic business question.

---

## Monthly Waterfall: What We Should Actually Chart

Before we add more planner views, the cleanest chart to build is a simple monthly waterfall between revenue rate and spend rate.

### Recommended Waterfall Order

1. **Gross monthly revenue**
2. **Less: payment processing / refunds / bad debt**
3. **Net monthly revenue**
4. **Less: onboarding labor spend**
5. **Less: service labor spend**
6. **Less: AI / cloud / variable tooling**
7. **Contribution after variable spend**
8. **Less: fixed company spend**
9. **Monthly operating result**

### Spend Categories We Should Keep Separate

#### Fixed spend

- founders
- engineering
- product / design
- management
- compliance / legal / finance
- office and fixed infrastructure

#### Variable spend

- onboarding FSR payroll
- service FSR payroll
- AI / cloud / agent usage
- payment processing
- variable support tooling

This is the cleanest way to show the business as a services-enabled operating model.

---

## Steady-State Analysis Should Be Separate From the Ramp Model

We should stop trying to force every question into one model.

There are really two distinct analyses:

### 1. Bottom-up steady-state analysis

Start from the mechanics of service delivery.

Questions:

- how many productive onboarding hours does one onboarding FSR have?
- how many productive service hours does one service FSR have?
- how many families can one service FSR support at the target service intensity?
- what is the variable cost to serve one active family?

Outputs:

- onboarding capacity per onboarding FSR
- service families per service FSR
- monthly variable cost per family
- contribution margin per family

### 2. Top-down steady-state analysis

Start from the business outcome we want.

Questions:

- if we want to support 10K, 25K, or 50K active families, what monthly revenue does that imply?
- what service staffing does that imply?
- what fixed spend can the business support at those revenue and margin levels?
- what margin and cash profile do we get at scale?

Outputs:

- revenue envelope at target scale
- staffing envelope at target scale
- maximum affordable fixed spend
- steady-state operating result

### Why These Should Be Separate

The bottom-up model validates whether the service mechanics are believable.
The top-down model validates whether the business looks attractive at scale.

The 36-month ramp model is a third thing. It should sit on top of the first two, not try to replace them.

---

## What We Should Not Force Into the Base Model Yet

To keep the model simpler, the following should be deferred until the base mechanics are settled:

- cross-trained FSR pool assumptions
- complex phase-plan overrides
- multiple payer mixes and subsidy logic
- advanced scenario sensitivity matrices
- financing events and capital stack mechanics
- tiered pricing mix beyond a small number of explicit cases
- detailed LTV / CAC storytelling as the center of the product

These are not bad ideas. They are just second-order questions.

---

## Working Definitions We Need To Hold Consistently

| Term | Working definition |
|---|---|
| **Family** | One paying family unit being supported through the platform |
| **New family** | A newly activated paying family in the current month |
| **Active family** | A family still on platform and paying at month end |
| **Onboarding FSR** | Human staff primarily responsible for activating new families |
| **Service FSR** | Human staff primarily responsible for supporting existing active families |
| **Onboarding hours per family** | Human hours required to activate one new family |
| **Service hours per active family per month** | Human hours required to support one active family during a normal month |
| **Fixed spend** | Spend that exists even if family count does not change materially |
| **Variable spend** | Spend that scales with new families, active families, or service load |
| **Contribution after variable spend** | Revenue remaining after delivery costs but before fixed company costs |
| **Operating result** | Monthly revenue minus total monthly spend |

---

## Open Decisions To Resolve Next

These are the next clean definitional questions, not dashboard questions:

1. What exactly counts as `service hours per active family per month`?
2. Do escalations sit fully inside service FSR time, or do they need a separate specialist bucket later?
3. Do onboarding FSRs and service FSRs have the same loaded cost, or should we model two compensation bands?
4. Should payment processing be shown above or below net revenue in the monthly waterfall?
5. What does the minimum fixed company team look like in the simplest version of the model?

---

## Recommendation For The Next Build Step

Before we change the main dashboard again, the next implementation should probably be:

1. a simple monthly waterfall view
2. a clean steady-state bottom-up calculator
3. a separate steady-state top-down calculator
4. only then a revised 36-month ramp model using split onboarding vs service FSR roles

That sequence is calmer, easier to reason about, and more likely to produce a model we trust.
