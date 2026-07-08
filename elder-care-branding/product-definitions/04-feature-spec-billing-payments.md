# Feature Spec — Billing & Payments

*Product definitions series, doc 4 of 5*
*Status: Draft v1 for internal review · 2026-07-06*
*Working product name: **Harbor** (brand under evaluation)*
*Owner: Product · Reviewers: Finance, FSR Ops (Dana), Compliance (Elena), Engineering*

---

## 1. Design philosophy

Billing in this category is not a back-office function; it is a **trust surface**. Our customers are paying us during the hardest season of their lives, sometimes through a death, and the sibling cost-split makes our invoices a topic of family conversation. Three principles govern every requirement below:

1. **Money mirrors the mission.** The family is the unit — so the family, not a user, is the payer. Cost-splitting is a first-class feature, not a workaround (doc 02 §A.5 makes the business case; this doc specifies it).
2. **Never extractive, visibly.** Income-scaled pricing, scholarships, pause states, memorial mode, and compassionate dunning are product features with specs — not support-desk exceptions. (Stakeholder decision #5: "mission-driven, never extractive.")
3. **No dark patterns, at a category-extreme standard.** Cancellation is one screen. Downgrades are self-serve. A grieving family is never dunned. Any billing pattern we'd be ashamed to explain to Ruth doesn't ship.

**Objects** (extends the doc 03 model): `BillingGroup` (per household: plan, payers, split policy, ledger, state) · `Payer` (member + payment method + share) · `SplitPolicy` (equal / custom % / one-payer) · `Ledger` (append-only record of charges, payments, credits, and inter-sibling attribution) · `BillingState` (active / grace / paused / memorial / cancelled).

---

## 2. Plans, trials, and tier changes

### 2.1 Tier lineup (from the pricing analysis)

| | **Connected** $79/mo | **Supported** $149/mo | **Managed** $299/mo |
|---|---|---|---|
| AI assistant + coordination workspace | ● | ● | ● |
| Onboarding | Self-serve (AI-guided) | **Human onboarding (FSR)** | Human onboarding (FSR, extended) |
| FSR relationship | — | Pooled; monthly check-in | **Dedicated FSR**; proactive monitoring |
| Care-plan reviews | — | — | Quarterly |
| Escalation to human | Best-effort | Included | Priority |

Annual prepay: 2 months free (16.7% off), refundable pro-rata on cancellation — annual is a discount, not a lock-in. Two-household families (divorced parents, in-laws — doc 03 §9.4): 20% off the second household's subscription.

### 2.2 Trial vs. onboarding fee

These two mechanisms serve opposite tiers and must not blur:

- **Connected: 30-day free trial**, card required, cancel-anytime, **three reminder notices before first charge** (day 23, day 27, day 29 — we remind *more* than the law requires; auto-convert surprise is a trust wound in this category). Full product access during trial; data connections made in trial persist on conversion and are exportable-then-deleted on non-conversion.
- **Supported/Managed: no free trial — a paid onboarding engagement instead.** Human onboarding consumes 3–6 hours of FSR time (pricing doc cost basis); giving it away free-trial-style invites consuming the service and churning. Structure: **one-time onboarding fee of $199 (Supported) / $299 (Managed)**, positioned as the "Family Setup" — consent ceremonies, data connections, sibling onboarding, POA document review, first care review. **Guarantee:** if the family cancels within 30 days of onboarding completion, the onboarding fee is refunded in full. This converts "no trial" from a barrier into a confidence statement.
- Onboarding fee is **waived** for: scholarship families, health-plan-channel enrollments (the plan's fee covers it), and advisor-referred Managed households (channel incentive, doc 02 §C.2).

### 2.3 Upgrades, downgrades, mid-cycle math

- **Upgrade (any → higher):** immediate. Prorated charge for the remainder of the cycle at daily granularity; upgrade to Supported/Managed schedules the human onboarding delta (e.g., Connected→Supported adds the FSR setup session; the onboarding fee applies at 50% for existing customers, waived after 12 months' tenure). Upgrades proposed by an FSR must carry a stated reason in the family's ledger ("Dana suggested Managed after the second hospitalization") — sales pressure and care advice must never blur, and the record proves it.
- **Downgrade (any → lower):** self-serve, one screen, effective at next cycle close (no clawbacks, no retention-hostage flows; one optional "what changed?" question, skippable). Features degrade gracefully: leaving Managed keeps the family's care-plan documents; leaving Supported keeps all data and connections — the family loses the human layer, never their record.
- **Split interaction:** any plan-price change recomputes shares per the SplitPolicy and notifies every payer *before* it takes effect, with the new per-payer amount stated ("Your share changes from $49.67 to $99.67 on Aug 1"). A tier change is a family decision; the product treats Care Lead–initiated changes above the current tier as requiring acknowledgment (not approval) from other payers — they get 72 hours' notice before their card is charged a higher amount, and an objection routes to a family discussion thread, not a silent charge.

**US-BILL-1 — The complexity upgrade**
*As Sarah, after Mom's hospitalization, I want to upgrade Supported→Managed mid-cycle so the dedicated FSR starts now, without a billing argument with my brothers later.*
Acceptance criteria:
- [ ] Upgrade takes effect immediately; prorated delta computed and displayed per payer before confirmation
- [ ] Mike and Jenny notified with the reason field Sarah wrote + new share amounts + 72-hour notice before their cards are charged the higher recurring amount (the immediate prorated delta may go to Sarah's card alone by her choice: "I'll cover the difference this month")
- [ ] Ledger records the change, the reason, and who paid what
- [ ] Dana's post-hospitalization check-in is auto-scheduled as part of the upgrade

---

## 3. Sibling cost-splitting (first-class feature)

### 3.1 Split policies

| Policy | Mechanics | Real-world fit |
|---|---|---|
| **Equal split** | Price ÷ active payers; remainder cents assigned round-robin | Default; "we're all in this together" |
| **Custom percentage** | Care Lead proposes %s summing to 100; each payer accepts their own % before it binds | "Jenny does the drop-ins, she pays 10%"; "David makes triple what we do" |
| **One-payer with transparency ledger** | One card pays all; the ledger still *attributes* the cost visibly to the family ("David covers Harbor: $149/mo, $1,788 this year") with optional IOU tracking (recorded, never enforced) | The wealthy sibling; the only-solvent sibling; the guilt economy made legible |

Core mechanics, all policies:
- **Each payer pays their share on their own payment method.** Separate charges, separate receipts, separate card statements reading "HARBOR — [Household] share." No sibling ever fronts money invisibly (the resentment engine we exist to shut down).
- Charges for a cycle are initiated together on the cycle date; the household's service state is computed from the *aggregate* (see §3.3 for partial failure).
- Payers join by **split invitation** (from purchase flow or later): invite shows plan, policy, their proposed share, and what they get (the digest, the visibility — doc 02's "smaller ask that produces engagement"). Until accepted, the inviting payer's method covers the unclaimed share — **purchase never blocks on sibling response.**
- Any payer may **leave the split** with 30 days' notice; shares recompute per policy (equal) or return to proposal (custom); the family is notified factually, without editorializing.
- The **ledger** is the billing mirror of the audit trail: every charge, payment, failure, credit, and coverage event, per payer, forever, exportable. Money transparency is family-visible to all *payers* and to Care Leads; non-payer members see only that billing is in good standing. **The parent is never shown fundraising mechanics** unless she is herself a payer (some parents insist on paying — supported: the Parent role can hold a Payer seat, and some families report this matters enormously to the parent's sense of agency).

### 3.2 User stories — splitting

**US-SPLIT-1 — Equal split at purchase**
*As Sarah, I want to buy Supported tonight and invite my brothers to split it, so that the family commits together but my momentum isn't hostage to their inboxes.*
Acceptance criteria:
- [ ] Purchase completes on Sarah's card alone; split invitations to Mike and Jenny sent in the same flow
- [ ] Invitation states: plan, equal policy, $49.67/mo share (remainder-cent rule disclosed), first-charge date, link to what Harbor is
- [ ] On Mike's acceptance + card add, next cycle charges split correctly; the *current* cycle optionally rebalances via credit to Sarah (her choice, one tap)
- [ ] 14-day expiry with one re-send; unaccepted share remains on Sarah's card with a monthly gentle note to her only (never a nag to the decliner)

**US-SPLIT-2 — Custom percentages without a fight**
*As the family, we want a 45/45/10 split because Jenny contributes in person, so that money mirrors our real arrangement.*
Acceptance criteria:
- [ ] Care Lead proposes percentages with an optional reason line; each payer accepts *their own* share explicitly; policy binds only when all accept
- [ ] Any payer can propose a revision at any time; revisions require all-payer acceptance; history retained in the ledger
- [ ] No payer ever sees a share change on their card that they did not individually accept (except equal-split recomputation on payer exit, which is notified 30 days ahead)

**US-SPLIT-3 — One payer, visible generosity**
*As David (a hypothetical fourth sibling who out-earns everyone), I want to just pay for the whole thing without either hiding it or lording it, so that money helps instead of distorting.*
Acceptance criteria:
- [ ] One-payer policy selectable with a family-visible attribution line (wording choices offered, from plain "David covers Harbor" to none-beyond-the-ledger)
- [ ] Optional IOU tracking off by default; if enabled, it records and never dunns
- [ ] Conversion path to equal/custom later without re-entering payment methods

### 3.3 When one sibling's payment fails

This is the flow most likely to either damage a family or prove our values. Requirements:

1. **Grace, quietly, first.** Failed charge → automatic retries (day 0, 3, 7, smart retry timing) with notices **to that payer only**. The household's service is unaffected. No family broadcast. A card decline is a private event for 14 days.
2. **The covering rule.** From day 14, the unpaid share is flagged to the Care Lead *as a neutral system state, not a sibling report*: "One share for July is unresolved. Options: cover it this cycle / adjust the split / ask Harbor to keep retrying." The failing payer is told exactly what the Care Lead can see — no information asymmetry about the asymmetry.
3. **Notification etiquette, codified.** Copy never names blame ("Mike's card was declined" is banned; "a share is unresolved" is the pattern). The failing sibling gets tools before exposure: update card, self-downgrade their share (request a split revision), or a hardship flag that routes to the income-scaled program (§6) *privately*. **Design intent: a sibling in quiet financial trouble must have a dignified exit ramp before the family finds out — we are not a family-shame machine.**
4. **Household floor.** If shares remain unresolved 30+ days and no one covers, the household — with FSR outreach first on Supported/Managed — moves to the standard dunning path (§7) on the *unpaid fraction*: practical effect is a proposed downgrade or split revision, never a sudden lockout of a family whose other members are paying.
5. Every event lands in the ledger with the neutral phrasing; the full mechanics of who-saw-what-when about payment failures follow the audit rules of doc 03 §8.

**US-SPLIT-4 — The quiet decline**
*As Mike, whose card was compromised during a job transition, I want two weeks and a private fix path, so that a $49 hiccup doesn't become a family incident.*
Acceptance criteria:
- [ ] Days 0–14: retries + private notices to Mike only (email + push, calm copy, one-tap card update); household service and family surfaces unchanged
- [ ] Day 14: Care Lead sees the neutral unresolved-share state; Mike is shown *exactly* the sentence the Care Lead sees
- [ ] Hardship flag available to Mike at every step, routing to §6 privately
- [ ] At no point does any family-facing surface use Mike's name in connection with the failure; ledger records use neutral system phrasing until resolution, then record the resolution factually

---

## 4. Income-scaled pricing

- **What it is:** the same tiers at scaled prices for households below income thresholds — published as a program ("Harbor Access"), not a hidden coupon. Bands (initial, to be tuned): ~≤$50K household income of the *payer group's median contributor* → 50% off; ~$50–80K → 25% off. The parent's income/assets are **not** the basis — the payers are the customers; a wealthy parent with strapped children is exactly who this serves.
- **Application flow:** self-attestation + lightweight verification (prior-year 1040 first page or two pay stubs, reviewed by billing ops, deleted after decision — we retain the *decision*, never the documents). Decision in ≤3 business days; applies from next cycle with a one-cycle retroactive credit if approved. Annual light re-attestation (one click "still accurate"), full re-verification every 24 months. Denials get a human-written note and a scholarship pointer.
- **Split interaction:** scaling can apply **per payer** — Mike's hardship (§3.3) can scale *his share* without touching his siblings' prices. This is the dignified exit ramp made concrete: the family sees the split percentages they agreed to; scaled dollar amounts per payer are between that payer and Harbor. (Ledger shows the household total as met; per-payer scaled amounts render only to that payer and billing ops.)
- **Anti-gaming posture:** deliberately trusting. We verify lightly, audit a random sample, and accept some abuse as the cost of the program's dignity. The program's economics are capped at a budgeted % of revenue, reviewed quarterly (Finance owns the dial, not the flow).

## 5. Scholarships

- **What:** 100% subsidized Supported-tier service (human onboarding included — trust requires the human most where money is tightest), 12-month renewable terms, funded initially from revenue (target: 1 scholarship household per 25 paying, reviewed quarterly; later a partner/donor program).
- **Who:** application (10 minutes, plain language) + referral routes — social workers, Area Agencies on Aging, discharge planners, faith communities. Criteria weight care complexity and absence of alternatives over paperwork perfection. FSR interview replaces documentation where documentation is the barrier.
- **Experience parity is absolute:** identical product, identical FSR quality, no "scholarship" label on any family-visible surface, no separate queue. Internal flag exists solely for billing suppression and program reporting.
- Renewal is FSR-initiated ("let's re-up your program year"), never a lapse-and-lockout.

---

## 6. *(merged into §4–5 above — section number retained to keep reviewer cross-references stable; remove on v2 renumber)*

## 7. Dunning — compassionate by specification

Standard dunning (non-split single-payer, or a household-level unresolved fraction per §3.3.4):

| Day | Event | Copy register |
|---|---|---|
| 0 | Charge fails; smart retry scheduled | None (silent) |
| 3, 7 | Retries + notice to payer | "Your card on file didn't go through — usually it's an expired card. One tap to update. Nothing changes for your family." |
| 14 | Second notice; FSR flag on Supported/Managed (Dana may simply *call* — a human call collects better than any email and is also just kinder) | Same register; adds hardship/income-scaling door explicitly |
| 21 | Proposed soft landing: downgrade offer (e.g., Supported→Connected) or pause (§8) presented as *choices*, pre-computed | "If money's tight this season, here are two ways to keep everything without the current price." |
| 30 | Service restriction **to read-only** — never deletion, never lockout from the family's own record; connections pause; digests continue monthly | Factual, warm, no red banners |
| 90 | Account archived (read-only export available for 12+ months); data-deletion only per user request or retention policy | — |

**Hard rules:** no late fees, ever. No collections agencies, ever. No dunning emails to anyone but payers. **Dunning freezes automatically** while the household is in pause (§8), memorial (§9), or an active hospitalization flag — an FSR or an in-product flag ("we're in the hospital with Mom") halts the entire sequence for 30 days, no questions, no documentation. Abuse of that button is a cost we accept; dunning a family at an ICU bedside is a brand-ending event we do not.

## 8. Pausing — hospitalization, hospice, respite

- **Pause states:** *Hospitalization pause* (up to 60 days) and *Hospice/comfort-care pause* (unlimited duration). Self-serve or FSR-set. Billing stops at the next cycle boundary (mid-cycle pause credits the remainder); **product access continues in full during pause** — pausing payment must not remove the tool precisely when the family needs it most. (Yes, this is deliberately generous; the LTV math of a family we stood by during a hospitalization justifies it, and Dana's meeting line — check-ins are the retention product — applies doubly here.)
- During hospice pause on Supported/Managed, FSR check-ins *continue*, reframed to the season (care logistics, family support, gentle preparation for §9). This is the moment the brand promise is either real or it isn't.
- Un-pause: automatic prompt after the stated period with a one-tap extend; never an automatic silent resumption of charges without a 7-day notice.

## 9. Cancellation & memorial mode

### 9.1 Ordinary cancellation

One screen: effective end of cycle, what's retained (everything, read-only, 90 days, exportable always), one optional reason question, a downgrade/pause alternative shown once without begging. Annual prepay refunds pro-rata. Split payers are all notified of a household cancellation with 30 days' notice (a Care Lead cancels the household; a payer leaving the split is §3.1 and does not cancel the household).

### 9.2 Memorial mode (death of the care recipient)

Extends doc 03 §9.3 with the money rules:

- **All billing stops immediately upon verified death — mid-cycle, no proration games: the final cycle's already-paid fees stand, nothing further is charged, and any annual prepay remainder is refunded pro-rata to each payer automatically.**
- **The product goes read-only and free for 12 months.** The record — every visit note, decision, photo, document, the whole ledger — is preserved and exportable. The estate workspace (doc 03 §9.3) is included free: executor tools, account-notification checklists, document access for probate.
- No payment method is retained in chargeable state during memorial mode (methods are detached from billing; ledger history remains).
- Month 11: one gentle notice offering export, permanent archive (one-time keepsake fee ≤$49, waivable by any FSR without approval), or deletion. Month 12+: default is archive-frozen (recoverable), never silent deletion.
- If the household has a *second* CareRecipient still living (doc 03 two-parent support), billing continues for the living parent's care at a single-recipient rate with an FSR-guided transition — handled as a plan change conversation, never an automated repricing email in the week of a death. **Any communication in the 30 days following a death is FSR-reviewed on Supported/Managed and template-minimal on Connected.**

**US-MEM-1 — The month everything stopped**
*As Sarah, in the week after Mom's death, I want Harbor to stop charging us and stop nudging us without my having to do anything, so that the product grieves with us instead of billing through it.*
Acceptance criteria:
- [ ] Death verification (FSR attestation or document) flips BillingState to memorial; all future charges cancelled the same day; prepay remainders refunded per payer within 5 business days
- [ ] All proactive notifications/tasks/assistant nudges cease immediately (doc 03 §9.3 tone-shift requirement — jointly tested with billing state)
- [ ] Every payer receives one plain, human notice confirming: no further charges, 12 months read-only free, export always available, Dana's direct line (Supported/Managed)
- [ ] Estate workspace available with no paywall; keepsake-archive pricing not shown until month 11

## 10. Receipts, invoices & FSA/dependent-care documentation

- Every charge produces a per-payer receipt (email + archive): payer, household (parent's name optional per privacy preference), plan, period, amount, and **itemization separating service categories** (care-coordination services vs. software subscription) — structured so that families pursuing FSA/HSA or dependent-care reimbursement, or the medical-expense / dependent-care tax analyses their accountants run, have clean documentation. **We do not advise on eligibility** (it varies by administrator and by the parent's tax-dependent status); receipts carry a neutral line: "Some families' benefit plans reimburse care-coordination expenses; provide this itemized receipt to your administrator. Ask us for a Letter of Medical Necessity template if yours requires one." — the LMN template (for the family's clinician to complete, where a clinician deems coordination medically necessary) ships at launch because it costs us nothing and saves some families $30+/mo effectively.
- Annual per-payer statement (calendar-year totals, itemized) auto-issued each January — accountant-ready.
- Invoices (vs. receipts) available for the advisor/professional channel and for the health-plan channel (plan-level invoicing per contract; families in plan-sponsored households see "covered by [Plan]" and no charge surfaces).

## 11. Payment security posture

- **No card data touches our servers:** PCI DSS SAQ-A posture via a hosted-fields processor (Stripe-class); tokens only; per-payer payment methods are isolated per Person (a sibling can never see another's card details — only last-4 in their own view, and not even that across payers).
- 3-D Secure/SCA where applicable; smart retries within card-network rules; ACH offered for annual plans (lower fees fund the scholarship budget line — say so on the pricing page; mission legibility is free marketing).
- Billing events are part of the household audit architecture (doc 03 §8) with the §3.3 neutral-phrasing rules; billing ops staff access follows the same time-boxed, logged support-session model as FSR data access.
- Fraud posture tuned for our reality: the common fraud in eldercare is *against the parent*, not against us — payer-method anomalies (sudden method change on a payer + address change) get review, and the parent's payer seat (if she holds one, §3.1) gets the same anomaly protection the product gives her bank accounts.

## 12. Instrumentation

- Split adoption: % households with ≥2 payers at day 30 / day 90 (doc 02 target ≥60%); policy mix; revision frequency (healthy nonzero)
- Payment-failure funnel: % resolved privately in ≤14 days (target ≥85%); % escalating to family visibility; hardship-flag usage; zero-tolerance audit that no family surface ever named a failing payer
- Income-scaling: application→decision time; approval rate; program cost vs. budget cap; churn of scaled households vs. cohort (hypothesis: lower)
- Dunning: recovery rate by day; downgrade-save rate at day 21; pause-instead-of-cancel take rate
- Memorial: time-to-billing-stop after verification (target: same day, 100%); post-memorial export rate; month-11 archive vs. delete elections
- Refund/complaint rate on any billing surface (target: ~0; every instance FSR-reviewed)

---

*Related docs: `02-...buyer-perspective.md` (why the split is a conversion feature) · `03-feature-spec-accounts-identity-permissions.md` (BillingGroup within the household model; memorial mode's non-billing half) · `05-mvp-scope-and-release-plan.md` (which billing capabilities the first 10 families get vs. what's concierge-manual at first).*
