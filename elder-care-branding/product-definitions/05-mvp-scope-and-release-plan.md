# MVP Scope & Release Plan

*Product: Harbor (working name — brand under evaluation, see `../01-brand-strategy.md`)*
*Status: Concept spec · Companion to `01`–`04` in this folder*
*Phasing mirrors the strategy in `research/competitive-landscape/04-competitive-positioning.md`: coordination first → data connectivity → proactive household intelligence.*

---

## The One-Sentence MVP Test

After the first onboarding session, the family should say:

> **"Finally, everything is in one place and we know who's doing what."**

If a feature doesn't serve that sentence for the first 10 families, it is out of the MVP.

---

## Phase 0 — First 10 Families (Months 0–3): "Concierge MVP"

**Goal:** validate that distributed siblings will adopt a shared workspace, grant real data access, and feel relief within 30 days. Ten families, hand-recruited from personal networks, each with 2+ siblings in different metros.

### In scope
| Area | What ships | Notes |
|---|---|---|
| Family workspace | One household per family; dashboard answering *what changed / what needs action / who's handling it* | Per care-platform wireframe |
| Roles & permissions | Care Lead, Care Partner, Viewer, Parent — with per-domain visibility (medical/physical/financial) | Simplified from spec 03; audit trail from day one (it's cheap now, impossible to retrofit credibly) |
| Parent consent | The consent ceremony (digital + printed-letter/phone path) | Non-negotiable even at n=10 — it's the moral spine and a differentiator to test |
| Tasks & timeline | Shared tasks with named owners and due dates; unified event timeline | The anti-group-text |
| Document vault | POA, insurance cards, med lists, advance directives; tagged, searchable | Storage, not intelligence |
| Directory | Providers, facilities, pharmacies, key contacts | |
| AI summaries | Weekly family brief + on-demand Q&A over the family's own records | Retrieval over *entered/uploaded* data only — no external integrations yet |
| Human layer | Founder-led white-glove onboarding (this is Blake/Spencer + first FSR); monthly check-in call | We are the FSRs; every hour is discovery research |
| Billing | Single tier ($149 equivalent, founders' pricing at $99), one payer, manual Stripe links | Split billing is *manual concierge* if a family asks — validates demand before we build it (per spec 04) |

### Explicit non-goals for Phase 0
- No bank/MyChart/Medicare integrations (data is entered or uploaded; the AI guide-through comes in Phase 1)
- No mobile app (responsive web + SMS/email notifications)
- No self-serve signup, no Connected tier, no marketplace, no health-plan features
- No automated cost-splitting, dunning, or memorial mode (handled by hand with grace if they occur)

### Riskiest assumptions this phase must test
1. **Multi-sibling adoption:** do the *remote* siblings actually log in weekly, or does the Care Lead remain the only user? (Kill signal: <2 active members per family at week 8.)
2. **Data-sharing willingness:** will families upload financial documents and grant medical visibility to each other at all?
3. **Relief is real:** does the weekly brief measurably reduce "status update" traffic in the family's group text?
4. **Willingness to pay:** do 7+ of 10 convert from founders' pricing to full price at month 4?
5. **Parent dignity:** does the consent ceremony land as respectful (parent NPS) or as bureaucracy?

### Success metrics
- ≥2 weekly-active family members per household (median)
- ≥70% of families upload documents in all three care domains by day 30
- Weekly brief open rate ≥80%; "this saved me time this week" pulse ≥4/5
- 7/10 families still active and paying at month 4
- Qualitative: at least 5 unprompted utterances of the one-sentence test (or equivalent)

---

## Phase 1 — First 100 Families (Months 3–9): "Connected"

**Goal:** kill the manual-entry ceiling and prove tiered self-serve economics.

### Ships
- **Guided portal connections** — the Clicky-style AI screen companion (`product/02-guided-onboarding-clicky-concept.md`) walking families through bank read-access, MyChart proxy access, and Medicare.gov sharing; FSR as backup. Target: human onboarding time from 3–6 hrs → ~1 hr.
- **Financial visibility v1** — connected balances, transaction feed, bills-due, simple spending bars (read-only, per financial-view wireframe decisions).
- **Medical visibility v1** — appointments and medication list pulled from connected portals; refill status.
- **Tiering goes live** — Connected $79 (self-serve) / Supported $149; Managed remains waitlist. Sibling cost-splitting ships as software (equal + one-payer models first).
- **Mobile app v1** — notifications, brief, chat, approvals (the four things people need on the move).
- **FSR tooling v1** — caseload dashboard, check-in scheduling, escalation queue (Dana's requirements from the synthesis).
- Income-scaled pricing + scholarship application flow.

### Success metrics
- ≥60% of new families complete ≥2 portal connections in week 1
- Human onboarding hours/family ≤1.5 (from 3–6)
- Connected→Supported upgrade ≥15% within 90 days (validates the tier ladder from `business/10-pricing-and-ramp-analysis.md`)
- Monthly logo churn ≤2%; ≥50% of multi-sibling families adopt split billing
- CAC on first paid channels ≤3 months' contribution margin

## Phase 2 — Scale Foundations (Months 9–18): "Supported"

- Managed tier GA with dedicated FSRs; quarterly care-plan reviews productized
- Deeper connectivity: insurance claims, facility update ingestion, pharmacy
- Full billing machinery from spec 04 (custom splits, failure ladder, pause/hospice/memorial modes as software)
- Two-person approvals + full audit surfaces from spec 03
- Advisor referral program (elder law, wealth managers, GCMs) — first channel beyond D2C
- Begin health-plan conversations (6–18 month cycles; per the growth strategy this is pipeline-building for Year 3+, not Year 2 revenue)

## Phase 3 — Household Intelligence (Months 18+): "Managed at scale"

The moat phase — from coordination tool to indispensable operating system:
- Proactive signals: "Mom missed two follow-ups since discharge" · "Utility bill up 40%, pharmacy spend down — possible adherence issue" · "Facility changed medications; family lead not yet notified" · "POA on file, but bank beneficiary forms missing"
- Anomaly/fraud watch on connected financial accounts
- Care-transition playbooks (hospital→rehab→home; home→assisted living)
- Health-plan B2B2C pilot with utilization reporting (Marcus's asks from the synthesis)
- Marketplace exploration: vetted vendors coordinated through the platform — only after trust is unquestionable, and never commission-opaque

---

## Sequencing Logic (why this order)

1. **Coordination before connectivity:** the wedge pain is sibling chaos, which needs zero integrations to solve; integrations are expensive and only compound value once the family already lives in the workspace.
2. **Trust surfaces before intelligence:** permissions, consent, and audit ship embarrassingly early because retrofitting trust is impossible; proactive AI that surprises a family *before* trust is established would be brand damage.
3. **Humans before automation:** founders do onboarding manually until the guided-companion can beat their time — the manual sessions are the training data for what to automate.
4. **D2C before B2B2C:** the health-plan channel needs outcome data D2C generates; per the organic growth strategy, plans are a Year 4 accelerant, not a Year 2 dependency.

## Cross-Phase Instrumentation (the drivers dashboard)

- Weekly active members per household (the adoption truth-teller)
- Portal connections per family (the moat-depth metric)
- Human hours per family per month, by tier (the margin driver from the financial model)
- Time-to-relief: days from signup to first "brief opened by all siblings"
- Churn by tier and by life-stage event (validating `business/13-churn-validation-analysis.md`)
- Referral rate — including from families in memorial mode (the ultimate trust metric)

---

*The through-line: every phase must deepen the answer to "why would a family trust us with this?" before it widens what we can do with that trust.*
