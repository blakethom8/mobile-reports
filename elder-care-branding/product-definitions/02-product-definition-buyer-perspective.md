# Product Definition — The Buyer's Perspective

*Product definitions series, doc 2 of 5*
*Status: Draft v1 for internal review · 2026-07-06*
*Working product name: **Harbor** (brand under evaluation)*

---

## Purpose of This Document

Doc 01 defined Harbor from the seats of the people who *use* it. This document defines it from the seats of the people who *pay* for it — which, in our chain, is three different buyers with three different value equations:

| Buyer | Who | What they're actually buying | Sales motion |
|---|---|---|---|
| **A. The D2C family buyer** | Usually the primary-coordinator sibling (Sarah) | Relief, family peace, and defensible stewardship | Self-serve + FSR-assisted, trigger-event-driven |
| **B. The health plan** | Marcus — VP, Medicare Advantage regional plan | Reduced avoidable utilization, better transitions, member/caregiver retention | Enterprise B2B2C, 6–18 month cycle, pilot-first |
| **C. The advisor channel** | Elder law attorneys, wealth managers, geriatric care managers, concierge medicine | A referral they're proud of; a client problem taken off their desk | Partnership/referral, trust-transfer motion |

The same product must be *bought* three ways without becoming three products. This doc specifies what each buyer needs to see, believe, and receive.

---

# Part A — The D2C Buyer (Sarah, holding the family credit card)

## A.1 Who actually buys

In the wedge segment (2–5 distributed siblings, one aging parent), the buyer is almost always the **primary coordinator** — the sibling already doing the work. She is not shopping a category; she is having a bad month. Purchase is emotional-first, justified rationally afterward, and then **re-justified to siblings** who will share the cost. That last step is unusual and decisive: our D2C purchase has an internal *committee sale* inside the family.

Demographics of the buying sibling (ICP 1): 45–60, household income $100K+, college-educated, comfortable with software, currently duct-taping portals + spreadsheets + group texts. Willingness to pay anchors not against apps but against the alternatives she's already contemplating: a geriatric care manager ($100–250/hr), reducing her own work hours, or continued unpaid-COO status at a real cost to her health and marriage.

## A.2 Purchase triggers (in observed order of frequency)

1. **Hospitalization or ER visit** — especially the *second* one, when "this is a phase" collapses.
2. **New diagnosis** — dementia/MCI above all; it converts an indefinite situation into a trajectory.
3. **A fall.**
4. **The financial scare** — suspected fraud, a discovered pile of unpaid bills, a bounced check from a parent who was never late in fifty years.
5. **Sibling conflict event** — the Thanksgiving fight; an accusation (explicit or felt) about money or effort.
6. **Care transition** — move to assisted living, loss of driving, death of the other parent leaving the survivor unsupported.
7. **Coordinator burnout event** — the buyer's own health scare, missed promotion, or spousal ultimatum.

**Product implication:** landing pages, onboarding, and FSR scripts should be organized by trigger, not by feature. Someone arriving from "mom fell" needs a different first five minutes than someone arriving from "I think someone is scamming dad."

## A.3 The objection stack (and what handles each)

| # | Objection (in the buyer's words) | What's underneath it | What handles it |
|---|---|---|---|
| 1 | "Another subscription. Another app my brothers won't open." | Fear of buying family software that becomes solo software | Sibling cost-split as proof-of-commitment (see A.5); family onboarding, not solo signup; Mike-facing digest that works without login |
| 2 | "I'm not giving a startup my mother's bank login and medical records." | Trust deficit; category is full of toys | Human onboarding (a named person, Dana, on video); HIPAA + bank-grade posture stated plainly; audit trail shown *during* the sales flow; POA/consent verification as a visible ritual, not fine print |
| 3 | "Mom will hate this." | Anticipated parent resistance; guilt | The parent-dignity principles as a *selling page* (consent-first, she sees who sees what, she can say no); Dana onboards Ruth personally on Supported/Managed; "ask her first" is our pitch, not our risk |
| 4 | "$149/month, forever?" | Duration ambiguity — this could be a 10-year purchase | Tier ladder (start at $79); split three ways it's $50/sibling — "less than one hour of a geriatric care manager, each month, for all of us"; income-scaled pricing removes the guilt edge; pause/downgrade freedom removes the trap feeling |
| 5 | "Can't I just do this with a shared spreadsheet and a group text?" | She literally is; sunk cost in her own system | "You are doing it. It costs you 10 hours a week and your brothers still think you're hiding things." The demo is her Tuesday (doc 01) shown back to her |
| 6 | "What happens when Mom dies? Do you delete everything? Do you keep charging us?" | Sophisticated buyers ask; it's a proxy for "are you decent people" | Memorial mode: read-only, free, 12 months, exportable estate records (see billing spec). This answer closes deals |
| 7 | "Is the AI going to make a mistake about medications?" | Safety liability fear | AI does retrieval/synthesis with provenance links, never clinical judgment; human escalation visible; "we show you the source, always" |

## A.4 How the tiers map to willingness to pay

| Tier | Price | The buyer's mental model | Who lands here | WTP anchor |
|---|---|---|---|---|
| **Connected** | $79/mo | "Let's get organized before this gets worse." | Pre-crisis, early-journey, price-sensitive, tech-confident families; also the post-crisis downgrade destination (retention, not loss) | vs. doing nothing / a bundle of point apps ($30–50) — priced above them deliberately, because seriousness signals |
| **Supported** | $149/mo | "We need help, and I need a human I can call." | Post-trigger-event families; the modal buyer. Human onboarding is the trust unlock for credentials | vs. 1 hr/mo of a care manager ($200+) — we're cheaper than one hour and present all month |
| **Managed** | $299/mo | "This is now complex enough that I want someone watching." | Multi-condition parents, active decline, high-net-worth estates, families in conflict who want a neutral professional in the room | vs. ongoing GCM engagement ($1–2K/mo) — one-fifth the cost; vs. the buyer reducing work hours — trivially cheaper |

Movement between tiers is a feature of the model: families upgrade as complexity rises (Dana proposes it at check-ins when warranted, with a stated reason — never a dark-pattern squeeze) and downgrade when things stabilize. **A downgrade retained is a customer kept**; our churn math (1.5–2%/mo target) depends on Connected being a dignified place to land, and on pause (hospitalization/hospice) existing so cancel isn't the only pressure valve. Income-scaled pricing and scholarships (billing spec §6) extend every tier down-market without a separate cheap brand.

## A.5 The sibling cost-split as a purchase feature

This is not a billing convenience; it is a **conversion and retention mechanism**, and we should market it on the pricing page.

**Why it converts:** Objection #1 ("my brothers won't engage") is neutralized by making the brothers *payers*. Asking Mike for $49.67/month is a smaller ask than asking him for engagement — but it *produces* engagement, because people attend to what they pay for. The buyer's committee sale gets a concrete artifact: "Harbor sent you a split invitation" is an easier text than "please care more."

**Why it retains:** A family with three cards on file has three people who must consent to cancellation — or at least three people who notice. And the equal/custom/one-payer options (billing spec §3) absorb real family economics: the sibling who does the physical visits pays less; the wealthy sibling covers it all but everyone *sees* that on the transparency ledger, converting money into acknowledged contribution instead of silent resentment.

**Why it differentiates:** No incumbent treats the family as the economic unit. Wellthy bills an employer; care apps bill a user. Billing the *sibling group* is the monetization mirror of our core positioning ("built for families, not just caregivers").

**Sales-flow requirement:** the buyer can complete purchase alone (never block the motivated moment on sibling response) and send split invitations afterward; her card covers unclaimed shares until siblings accept, and the product nudges gracefully.

## A.6 What success feels like to the D2C buyer

Ninety days in, Sarah can say to a friend at book club — our true acquisition channel — all three of: "I got my Sundays back," "my brothers actually help now," and "my mother doesn't hate it — honestly she likes that she can see everything too." When those three sentences are true, referral is organic and CAC falls with each cohort. That sentence-triple is a measurable target (see doc 05 metrics).

---

# Part B — The Health Plan Buyer (Marcus, Medicare Advantage VP)

## B.1 Marcus's seat

Marcus runs member experience and supplemental benefits for a regional MA plan (~180K members). His scoreboard: **Star Ratings** (CAHPS member experience, HEDIS quality measures), **medical loss ratio**, **member retention** (disenrollment during AEP), and **benefit differentiation** in a brutal county-by-county market. He is pitched constantly. His words from the meeting frame the whole sale:

> "Show me reduced ER utilization and better care transitions and I'll pay PEPM. But your brand can't look like a startup toy — it goes in front of my members."

He is buying an *outcome story he can defend to his actuaries* and a *benefit he's proud to print in the member packet*. In that order.

## B.2 The benefit economics (PEPM model)

**Structure:** Plan pays a per-eligible-member-per-month fee for a defined eligible population; enrolled families receive Harbor (typically the Supported-equivalent) as a covered or subsidized supplemental benefit, co-branded.

**The population insight that makes the math work:** the plan's *member* is Ruth; Harbor's *operator* is Sarah. We are, in effect, the first caregiver-facing benefit that plans can buy for the member's family — and the member's family is who actually determines whether Ruth ends up in the ER at 2am or at urgent care at 3pm.

**Illustrative pilot economics** (to be validated — these are the numbers we bring to the first conversation, clearly labeled as hypothesis):

| Line | Assumption | Basis |
|---|---|---|
| Eligible cohort | 2,000 members (high-risk: 75+, 2+ chronic conditions, recent inpatient/ED event, identified family caregiver) | Plan's own stratification |
| Engagement rate | 15–25% of eligible families activate | Comparable caregiver-benefit programs |
| PEPM fee | $8–15 on eligible population (≈ $40–75 per *engaged* family — below our D2C price because the plan removes CAC) | Pricing doc: "What's the PEPM they'd subsidize? $50? $100? $150?" — we structure so the engaged-family cost lands in that band |
| Avoidable ED visits | Baseline ~600/yr in cohort; target 8–12% reduction among engaged | Coordination + med adherence + earlier escalation to appropriate care |
| Cost per avoided ED visit | $2,500–3,500 (plus downstream admissions averted) | Plan's actuarial tables |
| 30-day readmissions | Target 10–15% relative reduction among engaged post-discharge families | Discharge-task orchestration (below) |
| Break-even | ~25–40 avoided ED visits/yr on a 2,000-member cohort at the low PEPM | Before counting retention or Stars value |

**The soft-dollar kicker that often decides it:** a member whose family is enrolled in a plan-branded coordination benefit is materially harder to switch at AEP — the family, not just the member, now has a relationship with the plan. One retained MA member ≈ $10–14K/yr in premium revenue. Marcus knows this math better than we do; our job is to instrument it.

## B.3 The outcomes story (what we report, how)

Harbor's clinical-adjacent mechanisms, mapped to what Marcus's team measures:

| Plan metric | Harbor mechanism | Evidence we can produce |
|---|---|---|
| Avoidable ED utilization | Family alerted early to symptoms/med issues → nurse-line/urgent-care routing surfaced in-product; assistant flags refill gaps before they become crises | Engaged vs. matched-control utilization (plan runs claims; we supply engagement + event data) |
| Care transitions (readmissions, TRC-type measures) | Discharge ingestion → auto-generated family task list (follow-up appt within X days, med reconciliation prompt, home-prep tasks) with named owners | % discharges with follow-up scheduled ≤7 days; med-rec completion; family confirmation timestamps |
| Medication adherence (PDC-relevant) | Refill monitoring + family-visible gaps + assistant-arranged delivery | Refill-gap closure rate, days-late distribution |
| CAHPS / member experience | Ruth's dignity surface + family relief reflected in member perception of plan | Enrolled-member CAHPS deltas (plan-measured); our own family NPS + parent-dignity scores shared quarterly |
| Disenrollment | Family-level stickiness of a plan-branded benefit | AEP retention, enrolled vs. matched cohort |
| SDOH / caregiver burden | Caregiver-strain instrument at onboarding and quarterly (e.g., Zarit short form) | Pre/post burden deltas — Marcus's population-health team values this for Stars narratives |

**Reporting deliverable:** a quarterly outcomes pack per plan — engagement funnel (eligible → invited → activated → active-at-90-days), utilization deltas (with the plan's analytics team co-owning methodology so the numbers are *theirs*, not vendor-claimed), transition-task completion, adherence metrics, caregiver-burden deltas, member-dignity scores, and a de-identified "saves" narrative annex (the fraud caught, the interaction flagged, the readmission averted) — because committee decks run on stories with numbers attached, not numbers alone.

## B.4 Co-branding and member experience

- **Co-branded, plan-forward enrollment**: member/family receives it as "[Plan] Family Care Coordination, powered by Harbor." The plan's brand carries the trust with the member; ours carries the product experience. (This is why the brand evaluation weighs "would Marcus put it in a benefits packet" — Direction C energy matters here even if we choose A or B for D2C.)
- **Non-negotiables we keep:** the parent-dignity principles, the consent model, and the data wall. **Plan receives outcomes reporting, aggregate and de-identified; the plan never receives family financial data, family communications, or non-claims PHI.** This wall is a *selling point* to Marcus (his compliance office will love us) and an absolute condition of family trust.
- **Eligibility file in, engagement file out** — standard SFTP/API exchange, HIPAA BAA executed, SOC 2 report available.

## B.5 Implementation asks (what Marcus's team will require) and what we ask back

**They will ask for:** BAA + security review (SOC 2 Type II, pen test summary, HITRUST roadmap); eligibility-file integration; member-services training + warm-transfer script for their call center; marketing-material review through their compliance (CMS marketing rules apply to how the benefit is described); a named implementation manager; a pilot design with control methodology; quarterly business reviews; and an exit/data-disposition clause.

**We ask for:** a defined high-risk cohort (not the whole book — engagement rates on unstratified populations kill pilots); co-marketing in at least two member touchpoints (post-discharge call, care-management outreach) because a letter alone won't drive activation; claims-data collaboration for the outcomes analysis; and a pre-agreed success definition with expansion terms, so the pilot's finish line is a contract, not a second pilot.

**Timeline honesty (from the ramp analysis):** health-plan cycles run 6–18 months. Conversations start Year 2, revenue lands Year 3–4. This channel is the *scale* engine, not the *survival* engine — doc 05 sequences accordingly, and nothing in the MVP is allowed to block on plan requirements.

---

# Part C — The Advisor Referral Channel

## C.1 Why advisors matter

Elder law attorneys, wealth managers, geriatric care managers (GCMs), and concierge-medicine practices sit at the exact moment of trigger events — the estate-planning meeting after the diagnosis, the account review where dad's confusion becomes undeniable, the discharge that needs a care plan. They see the family chaos we solve, weekly, and they currently have nothing clean to hand the family. A referral from a fiduciary transfers trust we cannot buy with ads. (Positioning doc, ICP 4.)

Each refers for a different reason:

| Advisor | Their moment | Why they refer | What they fear |
|---|---|---|---|
| **Elder law attorney** | POA/estate documents being drafted; guardianship avoidance | Harbor *operationalizes* the documents they draft — a POA on file but unexecuted is a malpractice-adjacent sadness they see constantly | Referring anything that later embarrasses them; anything that practices law |
| **Wealth manager / RIA** | Aging-client protocols; the "trusted contact" conversation; fiduciary duty to flag diminished capacity | Client families in chaos leak assets and attention; Harbor's financial transparency + two-person controls reduce elder-fraud risk on *their* book | Data security above all; anything that touches custody or looks like it competes for the assets |
| **GCM** | Assessment done, plan written — now who runs it day-to-day between her visits? | Harbor is her delivery/communication layer with the family; makes her look modern; she's in the loop between billable visits | Being disintermediated. **Positioning to GCMs: we are the operating system their care plan runs on, not a cheaper replacement for their judgment.** (Managed tier can embed/coordinate with an external GCM.) |
| **Concierge medicine / geriatricians** | Family asks "how do we manage all this?" at the visit | Their patient's outcomes depend on family execution; Harbor makes the family a competent care team | Clinical liability; anything that seems to give medical advice |

## C.2 What advisors need in order to refer confidently

1. **A professional-grade first impression.** The advisor will inspect the site and product before staking reputation. The brand must pass "would an elder-law attorney refer it without hesitation" (brand strategy evaluation criterion #4). Trust posture — HIPAA, encryption, audit trail, named humans — visible within one click.
2. **A clean referral mechanism.** Unique advisor link/code → warm handoff to a named FSR within one business day → the advisor gets a *consented* status ping ("the Hendersons completed onboarding") so referrals never vanish into a void. **No referral fees to fiduciaries by default** — for attorneys and RIAs, payment can taint or prohibit the referral; the currency is client outcomes and a professional partner portal. (A compliant revenue-share may exist later for non-fiduciary partners; it is never required.)
3. **Boundary clarity in writing.** One-pager per advisor type stating what Harbor is not: not legal advice, not investment advice or custody, not clinical judgment, not a GCM replacement. Advisors refer *into* well-marked lanes.
4. **Artifacts that make them look good.** A client-facing leave-behind (print-quality — this audience hands people paper); a "family readiness" checklist they can co-brand; for attorneys, the killer feature: **Harbor's document-status view showing which executed documents are actually on file and operationalized** (POA uploaded and verified, beneficiary forms missing — positioning doc Phase-3 example made real).
5. **A named partnership contact and an FSR tier-match.** Advisor-referred families skew complex and affluent — route them to Supported/Managed onboarding with an experienced FSR; a fumbled first family ends the pipeline.
6. **Proof.** Two or three referenceable families (with consent) and, later, the outcomes pack lite. GCMs and attorneys talk to each other in tight professional circles (NAELA, ALA chapters, local networks); one delighted attorney is a channel, one burned one is an anti-channel.

## C.3 What success looks like per channel (summary)

| Buyer | 12-month success statement |
|---|---|
| D2C | Trigger-event buyers convert at target CAC; ≥60% of new households activate ≥2 sibling payers; the book-club sentence-triple shows up verbatim in referral interviews |
| Health plan | 1–2 signed pilots with defined cohorts and co-owned outcomes methodology; a quarterly pack Marcus forwards internally without editing |
| Advisor | 10–15 active referring advisors across 3 professions; ≥25% of new Managed-tier households arrive advisor-referred; zero referred-family incidents |

---

*Related docs: `01-product-definition-family-perspective.md` (what the money buys) · `04-feature-spec-billing-payments.md` (cost-split, income-scaled pricing, memorial mode — the mechanics behind Part A) · `05-mvp-scope-and-release-plan.md` (why plans and advisors are Phase 2/3 motions).*
