# Feature Spec — Accounts, Identity & Permissions

*Product definitions series, doc 3 of 5*
*Status: Draft v1 for internal review · 2026-07-06*
*Working product name: **Harbor** (brand under evaluation)*
*Owner: Product · Reviewers: Compliance (Elena), Engineering, FSR Ops (Dana), Legal*

---

## 1. Why this spec exists

The stakeholder meeting concluded that the "boring" screens — accounts, permissions, consent — are where trust is won or lost ("trust is visual before it's contractual"). The positioning work identified delegated trust as a potential moat ("explicit roles, visibility controls, action approvals, audit trails, secure document authority — built for real family dynamics, not just a single login"). This spec defines that machinery.

**Design tenets** (each requirement below traces to one):

- **T1 — The household is the tenant.** Not the user. Everything belongs to a household; people hold roles within it.
- **T2 — Consent is a first-class object,** with a lifecycle (proposed → ceremonially granted → active → amended → revoked/superseded), not a checkbox.
- **T3 — Authority is proven, not claimed.** Legal authority (POA, guardianship) is verified, scoped, and displayed with its verification status everywhere it is exercised.
- **T4 — Visibility is per-domain** (medical / physical / financial), because real families share unevenly.
- **T5 — Sensitive actions are governed** (approvals, two-person rules), not merely logged.
- **T6 — Everything is logged, and the log is readable by the people it's about** — including, especially, the parent (Dignity Principle P2, doc 01).
- **T7 — Transitions are protocols, not switches** (Dignity Principles P3/P4): capacity changes and death are designed-for states with their own flows.

---

## 2. Object model

### 2.1 Entity diagram (conceptual)

```
Organization (Harbor internal)
 └── FSR (internal user) ──────────────┐ assigned to
                                       ▼
Household ─── has one or two ──► CareRecipient (the parent)
   │                                   │
   ├── Membership (person × role × domain-visibility grants)
   │      └── Person (global identity: login, MFA, contact prefs)
   ├── ConsentRecord (grantor, scope, ceremony evidence, status)
   ├── AuthorityRecord (POA/guardianship/etc.: type, scope, trigger,
   │      verification status, documents, expiry/supersession)
   ├── DomainSpace ×3 (Medical / Physical / Financial)
   │      └── Resources (accounts, records, documents, tasks, notes…)
   │            └── VisibilityOverride (resource-level carve-outs)
   ├── ActionPolicy (which actions need which approvals)
   ├── DecisionLog / AuditLog (append-only)
   └── BillingGroup (see doc 04)
```

### 2.2 Key objects

| Object | Definition | Notes |
|---|---|---|
| **Person** | A global identity: one human, one login, MFA required for any role touching PHI/financial data | A Person can belong to multiple Households (Sarah managing Mom and later her father-in-law) with independent roles in each |
| **Household** | The tenant. One or two CareRecipients + memberships + data + policies + billing | Two-CareRecipient support (married parents) is v1: shared physical domain, separable medical/financial per recipient |
| **CareRecipient** | The parent. Always *also* a Person with a Membership (Parent role) — never merely a data subject | Tenet T1 + Dignity P5. Even a recipient who never logs in has the role, so consent and the mirror view attach to a real identity |
| **Membership** | Person × Household × Role + per-domain visibility grants + notification profile | The atom of access control |
| **ConsentRecord** | A grant by the CareRecipient (or documented POA substitution) of specific visibility/connection scope, with ceremony evidence attached | §6 |
| **AuthorityRecord** | Verified legal authority: type (financial POA, healthcare POA/proxy, springing vs. durable, guardianship/conservatorship, trustee, rep-payee), scope, activation trigger, verification tier, documents | §5 |
| **DomainSpace** | The medical / physical / financial partition. Every resource lives in exactly one domain (documents may be linked into several) | T4 |
| **ActionPolicy** | Household-level rules mapping action classes to approval requirements | §7 |
| **AuditLog** | Append-only, immutable, per-household; every read of sensitive resources and every write, with actor, authority-basis, timestamp, and surface | §8 |

### 2.3 Roles

| Role | Held by | Summary of capabilities |
|---|---|---|
| **Care Lead** | 1–2 members (Sarah) | Full visibility (subject to parent carve-outs §6.5); manages memberships and invitations; edits ActionPolicies (some changes require co-approval, §7.4); initiates transitions; primary FSR contact. **Care Lead ≠ superuser:** cannot read carved-out resources, cannot suppress audit entries, cannot unilaterally remove the other Care Lead or the Parent role |
| **Care Partner** | Siblings and equivalents (Mike, Jenny) | Read/write within granted domains: tasks, notes, timeline; can claim tasks, upload documents, participate in approvals and decisions |
| **Viewer** | Extended family, family friend, a parent's sibling | Read-only within granted domains; no task ownership; no approval standing |
| **Parent** (CareRecipient) | Ruth | Own surface ("My Harbor": calendar, people, rides); the consent surface and who-sees-what mirror; "Ask me first" flags; revocation rights; full read access to her own data always (this right is not grantable away while she has capacity) |
| **Professional Member** | External GCM, aide agency lead, attorney (optional, Phase 2) | Scoped like Viewer + domain-limited write (e.g., GCM writes to medical/physical notes); clearly badged as non-family |
| **FSR** (internal) | Dana | Support-scoped access: sees structure, tasks, timeline, alerts, and consent/authority status; **does not see raw financial transaction detail or full medical record content by default** — elevated access requires a family-approved, time-boxed, audited grant (support session). All FSR access is visible in the family's audit log, identically to family access |

Role changes are themselves audited events with actor + reason. Every Household must have ≥1 Care Lead and exactly one Parent membership per CareRecipient at all times (enforced invariant).

### 2.4 Per-domain visibility grants

Each Membership carries a grant level per domain:

| Level | Meaning |
|---|---|
| **None** | Domain invisible: not in nav, not in digests, excluded from search and assistant answers to this member |
| **Summary** | Aggregates only — e.g., financial: "bills current, balances healthy, 1 flag"; medical: appointment existence, not clinical content |
| **Full** | All resources in the domain, minus resource-level carve-outs |
| **Full + Act** | Full, plus standing to take governed actions in this domain (subject to ActionPolicy approvals) |

Worked example (the reference family): Sarah F+Act/F+Act/F+Act · Mike Full/Full/Full · Jenny Full/F+Act(physical)/Summary — Jenny and money have history; the family set financial to Summary at onboarding, calmly, with Dana, instead of fighting about it at a crisis. **The assistant enforces grants in its answers:** if Mike asks the assistant a financial question while holding Summary, he gets the summary and a note that detail requires a grant change — never a leak through the chat surface.

---

## 3. Invitation flows

### 3.1 Founding flow (household creation)

1. Founding member (usually the future Care Lead) creates account → identity verification (email + phone; ID verification deferred to authority claims, §5).
2. Creates Household + CareRecipient(s) — minimal data until consent posture is established.
3. **Consent path fork (immediately, before data connection):**
   - *Parent has capacity* → parent consent ceremony is scheduled/completed (§6) — self-serve guided flow on Connected; FSR-conducted on Supported/Managed.
   - *Parent lacks capacity* → AuthorityRecord flow (§5) substitutes, and the record says so honestly (P1).
4. Sibling invitations (§3.2) + billing setup (doc 04) in either order.

### 3.2 Member invitation

- Care Lead (or Care Partner, if policy allows proposing) invites by email/phone: proposed role + per-domain grants shown *at send time* — the invitee sees exactly what they will and won't see before accepting. No surprise asymmetries; asymmetry disclosed is family policy, asymmetry discovered is family war.
- Invitation to the **Parent role** is special: it is a consent-ceremony scheduling act, not a normal invite.
- Invites expire in 14 days; re-sendable; every send/accept/decline/expiry audited.
- **Parent notice:** when any new member joins, the parent's who-sees-what mirror updates and (if capacity) she is notified in plain language: "Your niece Karen can now see your calendar. She cannot see medical or financial information."

### 3.3 User stories — invitations

**US-INV-1 — Transparent asymmetric invite**
*As Sarah (Care Lead), I want to invite Jenny with financial visibility set to Summary, so that a known family fault line is handled by policy instead of by fight.*
Acceptance criteria:
- [ ] Invite composer requires explicit per-domain levels (no hidden defaults; a suggested default is shown and editable)
- [ ] Jenny's invite screen displays her grants in plain language, including what she will NOT see
- [ ] On accept, Ruth's mirror updates; if Ruth has capacity, she receives the plain-language notice
- [ ] Jenny can request a grant change in-product; the request routes to Care Lead(s) and is logged, whatever the outcome

**US-INV-2 — Invitee declines but stays reachable**
*As Mike, I want to decline the app but still receive the weekly family digest by email, so that non-adoption doesn't equal exile.*
Acceptance criteria:
- [ ] Decline flow offers "digest-only" standing (a Viewer-lite Membership with no login), honoring the member's chosen domains at Summary level
- [ ] Digest-only members can upgrade to full membership at any time via a link in any digest
- [ ] Digest-only standing is visible to the family in the members list (no ghost members)

---

## 4. Identity & authentication (summary requirements)

- Email or phone + password with mandatory MFA for any member holding Full/F+Act on medical or financial domains; WebAuthn/passkeys supported at launch (this audience loses phones and shares computers).
- **Parent-appropriate auth:** the Parent role supports simplified auth on her own devices (device-bound passkey, long sessions on a registered tablet) — security calibrated to her threat model without making her surface unusable (P5). Phone-only parents are first-class: Dana can act as a verified proxy for consent conversations with recorded voice confirmation where permitted.
- Session and device management visible per member; Care Lead can see member device *counts*, never their sessions' content.
- No shared logins, ever — the entire trust model depends on actor identity. Onboarding explicitly migrates families off the "we all use Mom's MyChart password" pattern by replacing its convenience.

---

## 5. Legal authority: POA & verification

### 5.1 Authority types supported at v1

Financial POA (durable / springing), Healthcare POA / healthcare proxy / HIPAA authorization, guardianship & conservatorship (court-ordered), trustee (revocable living trust), Social Security representative payee. Each AuthorityRecord carries: holder, scope (enumerated powers), activation condition (immediate vs. springing + trigger evidence), jurisdiction/state, document set, verification tier, expiry/review date.

### 5.2 Verification tiers

| Tier | What it means | How achieved | What it unlocks |
|---|---|---|---|
| **V0 — Claimed** | Member asserts authority; no docs | Self-attestation | Nothing sensitive. Display-only badge "claimed, unverified" |
| **V1 — Documented** | Executed documents uploaded; automated checks (completeness, execution formalities, dates) + human review checklist | Upload + FSR-assisted review with legal-ops checklist (we verify *documents*, we do not practice law — reviewed language must say "documents on file and reviewed for completeness," never "legally valid") | Enables connection flows that require demonstrating authority to institutions; unlocks POA-based consent substitution (§6.6) |
| **V2 — Confirmed** | Third-party confirmation where available (attorney of record attestation, court registry for guardianship, institution acceptance on file) | Attorney e-attestation flow; court document verification | Highest badge; required for high-value governed actions if the family's ActionPolicy says so |

**Springing POA handling:** a springing financial POA (like Sarah's) is stored at V1 but shows status **"on file — not in effect"** until the trigger evidence (typically physician letters per the document's own terms) is uploaded and reviewed; then and only then does the product treat it as active authority. This distinction — on file vs. in effect — is displayed everywhere the authority is referenced, because families routinely misunderstand it and institutions routinely litigate it.

### 5.3 User stories — authority

**US-AUTH-1 — POA on file, honestly labeled**
*As Sarah, I want to upload Mom's springing financial POA and have Harbor track that it is not yet in effect, so that I neither overreach nor scramble during a crisis.*
Acceptance criteria:
- [ ] Upload flow captures type, scope, springing trigger as written, jurisdiction
- [ ] Status renders "On file — springs on [condition]; not currently in effect" on Sarah's authority badge and in Ruth's mirror
- [ ] Activation flow requires trigger-evidence upload + review; activation notifies all members and Ruth per capacity; activation is a prominent audit event
- [ ] The assistant answers "can I move money from Mom's account?" with the authority status, not legal advice, plus escalation to Dana/attorney referral

**US-AUTH-2 — The attorney's document-status view**
*As the family's elder law attorney (Professional Member, Viewer scope), I want to see which of the documents I drafted are on file and operationalized, so that my work actually protects the family.*
Acceptance criteria:
- [ ] Document-status panel: POA(s), proxy, HIPAA auth, trust — each with on-file / verified / in-effect state and gaps flagged ("beneficiary forms missing at Chase")
- [ ] No clinical or transaction detail exposed at this scope
- [ ] Attorney's every view is in the family audit log

Edge cases: conflicting POAs (two documents, different children — surface both, flag conflict, require FSR + recommend attorney resolution before either unlocks anything); revoked POA (parent with capacity may revoke; revocation ceremony parallels consent revocation and downgrades the AuthorityRecord immediately); out-of-state documents (jurisdiction flagged; no validity opinion rendered).

---

## 6. Parent consent: ceremonies, mirror, revocation

### 6.1 The consent ceremony

A **ceremony** is a structured, evidenced session in which the CareRecipient grants specific scopes. Format scales by tier: guided self-serve flow with the parent present (Connected) or FSR-conducted video/phone/in-person session (Supported/Managed — Dana onboards Ruth personally).

Ceremony contents, in order:
1. **Orientation** — what Harbor is, in her language, ≤2 minutes, no jargon.
2. **Scope walk** — each proposed grant presented singly and concretely: "Sarah and Mike would see the balance of your Chase checking — the number, updated daily. Not what you bought." Accept / decline / modify per item. Declines are honored *silently in structure* (the family sees the resulting permission map, not a list of her refusals — no shaming surface).
3. **The mirror preview** — she is shown the who-sees-what panel her choices produce.
4. **Revocation rights** — explicitly stated: any grant, any time, one conversation, effective immediately.
5. **"Ask me first" flags** — she designates decision types requiring her voice (§6.4).
6. **Evidence capture** — per-item choices recorded; signature/verbal confirmation per modality and state law; ceremony record sealed into the ConsentRecord and audit log.

Re-ceremonies occur at FSR check-ins (light touch: "anything you want to change?"), on any material scope expansion, and on any new data-source class.

### 6.2 The mirror ("Who sees what about me")

Always-current, plain-language, parent-facing panel: members and their domain levels; data sources connected in her name; **access recency** ("This week: Sarah viewed your medication list twice"); pending requests awaiting her. Available in-app on her surface, in large print by mail on request, and readable to her by Dana on any call. The mirror is the physical embodiment of Dignity P2 and is a launch-blocking feature, not an enhancement.

### 6.3 User stories — consent

**US-CON-1 — Granular grant with a carve-out**
*As Ruth, I want my children to see that my bills are paid without seeing my transaction detail, so that I keep a private interior (P6).*
Acceptance criteria:
- [ ] Financial sources support Summary-level connection (balance + bill-status + anomaly flags, no line items) as a ceremony choice
- [ ] Anomaly detection still runs on full data server-side; alerts expose only the minimum ("unusual charge flagged — Ruth has been notified and can share detail")
- [ ] Ruth's own view of her account is always full detail
- [ ] Upgrading the grant to Full requires a new ceremony item, not a settings toggle by a child

**US-CON-2 — Revocation that actually works**
*As Ruth, I want to withdraw Mike's medical visibility after a family argument, so that my consent is real and not decorative.*
Acceptance criteria:
- [ ] Revocation available via her surface AND via a call to Dana (evidenced verbally) — never app-only
- [ ] Effective immediately: Mike's medical domain drops to None; cached/digest content stops; assistant answers respect the change from the next message
- [ ] Family notified *that* a grant changed and its new state — not Ruth's reasons
- [ ] Mike's standing to request restoration exists and routes through Ruth (with FSR mediation offered), not through Sarah
- [ ] Revocation cannot be reversed by anyone but Ruth while she has capacity

### 6.4 "Ask me first" flags

Ruth designates decision classes — housing changes, driving, financial actions over $X, new caregivers in her home — where the decision log **cannot be closed** without a recorded "parent consulted" step (her comment, Dana's attested summary of a conversation with her, or a documented capacity-based exception with reason). This makes P1 mechanical instead of aspirational.

### 6.5 Parent carve-outs

Resource-level VisibilityOverrides that exclude specific resources from all family visibility (therapist notes; one checking account's detail). Carve-outs are visible *as existing* to Care Leads ("1 private resource exists in Financial") without content or identification beyond category — the family knows the map has a private room; they don't get a keyhole.

### 6.6 When consent can't be given

Where the parent lacks capacity at onboarding (or loses it later), verified authority (§5) substitutes — and the product labels every such grant "authorized under [instrument] by [holder]," never as parent consent (P1). If capacity is partial/fluctuating, consent is still sought for what she can meaningfully decide, with authority backstopping only the remainder; the FSR is trained to run mixed ceremonies.

---

## 7. Governed actions & the two-person rule

### 7.1 Action classes

| Class | Examples | Default policy (family-adjustable within floors) |
|---|---|---|
| **A — Routine** | Task edits, notes, uploads, appointment scheduling | Actor alone; logged |
| **B — Sensitive read** | First view of a newly connected source; export/download of records | Actor alone; logged with prominence; parent-mirror surfaced |
| **C — Financial action** | Bill-pay initiation, transfer requests, closing/opening products, engaging paid services | **Two-person rule: initiator + one other approver with Financial F+Act** (see floors) |
| **D — Structural** | Membership changes, grant changes, ActionPolicy edits, authority activation | Care Lead + notice to all; some subtypes require second approver (§7.4) |
| **E — Care-critical** | Facility applications, home-care contracts, transition protocol initiation | Care Lead + decision-log entry + "Ask me first" compliance |

### 7.2 The two-person rule (Class C)

Any Class C action requires a second approver before execution: initiator proposes (amount, payee, source, reason auto-drafted by the assistant with provenance links) → eligible approvers notified → approve/decline with comment → execution and receipt to the ledger and audit log. **Design intent is protective, not bureaucratic:** the approval-request artifact doubles as the transparency artifact — the same object that governs the action *is* the record that keeps siblings from wondering about it later.

**Floors (non-negotiable minimums):** two-person rule cannot be disabled for actions above $500 or for any change to payee/beneficiary/ownership structures; below that, families may set single-actor thresholds (e.g., "Sarah alone up to $200 for routine bills"). Sole-child households (§9.6) substitute FSR-acknowledgment or a designated non-family second (attorney, trusted contact) for the second signature above floors — the rule adapts; it never simply vanishes.

**Emergency path:** a genuine emergency payment (e.g., securing a rehab bed same-day) can proceed on one signature above floor **only** via the emergency override: mandatory reason, prominent non-suppressible audit entry, automatic FSR follow-up within one business day, and after-the-fact review by the second approver. Overrides are rare by design and their rate is a monitored health metric per household.

### 7.3 User story — two-person rule

**US-ACT-1 — Approval without friction-poisoning**
*As Sarah, I want routine bill payments to flow without turning my siblings into a bureaucracy, so that governance doesn't make me slower than the spreadsheet was.*
Acceptance criteria:
- [ ] Recurring approved payees can be pre-authorized by a one-time two-person approval covering the series (amount band + payee), reviewed quarterly
- [ ] Novel Class C actions reach approvers with full context in one screen; approve is one tap post-auth
- [ ] Median approval latency surfaced to the family; stale requests (>48h) escalate to all eligible approvers and Dana
- [ ] Declines require a comment and open a discussion thread — a decline is a conversation starter, not a silent veto

### 7.4 Guarding the guards

ActionPolicy edits that *loosen* controls (raising thresholds, removing an approver requirement) are themselves Class D events requiring a second Care Lead/Partner approval and parent notice per capacity. No actor can edit their own grant upward. No actor — including Harbor staff — can edit or delete audit entries.

---

## 8. Audit trail

- **Append-only, immutable, complete:** every read of sensitive resources (medical/financial detail, documents), every write, every permission/consent/authority event, every FSR access, every assistant answer that drew on sensitive data (logged as an access by the asking member), every export. Actor, role, authority basis, timestamp, surface, and — for reads — what was seen at what granularity.
- **Readable by design, three renderings:** the **family activity feed** (human sentences: "Mike viewed October bank statements — yesterday, 9:14pm"), the **parent mirror** (§6.2, her subset in her language), and the **compliance export** (structured, timestamped, suitable for attorneys, courts, and institutional disputes).
- **Non-weaponization guardrail:** the feed shows facts, never inferences or scoring ("Mike hasn't logged in for 30 days" is not a feed item; contribution comparisons are not a surface — doc 01, Mike's churn table).
- Retention: life of household + statutory horizon; survives memorial mode; exportable by Care Lead and by the Parent (her own slice) at any time.

---

## 9. Transitions & hard states

### 9.1 Cognitive-decline transition (the graceful handover)

Per-domain, protocol-driven (Dignity P3/P4). Trigger sources: family concern raised at check-in, pattern flags (missed bills, medication gaps), or clinical documentation. Protocol:

1. **Raise** — any member or the FSR opens a transition case in a domain; opening is logged and, per "Ask me first," Ruth is part of the conversation from the start where possible.
2. **Assess** — evidence gathered (never covertly: Ruth knows the question is open); clinical input required for authority-activation paths (springing POA terms govern).
3. **Smallest increment** — the case must propose the *minimum* change that addresses the concern (e.g., "add two-person rule to Ruth's own outbound transfers" long before "remove Ruth's financial access"). The UI literally orders options from least to most restrictive and requires justification to skip levels.
4. **Decide with her voice** — decision-log entry must include her words (agreement, terms, or dissent — dissent is recorded, not overwritten).
5. **Review date mandatory** — every restriction carries a scheduled review; restrictions do not silently become permanent.

Ruth's **own access to her own information is never reduced** by transition; what changes is her *unilateral action* scope and others' *authority*. Her mirror continues to work at every stage — arguably it matters most at the end.

**US-TRN-1 — The forgotten-bills transition**
*As the family, we want to respond to Mom's missed utility payments without taking her checkbook away, so that a real problem is solved at the smallest dignified increment.*
Acceptance criteria:
- [ ] Transition case in Financial opens with pattern evidence attached; Ruth notified in her terms
- [ ] Option list ordered least→most restrictive; family selects "auto-pay + Summary→Full family visibility on the bills account + no change to Ruth's authority"
- [ ] Ruth's voice recorded ("fine, but I keep the garden-club account private" — carve-out preserved)
- [ ] 90-day review auto-scheduled; reminder fires; review recorded

### 9.2 Incapacity (sudden)

Stroke/ICU scenarios: verified springing authorities activate via §5.3; a household banner states the changed basis of authority ("decisions currently under healthcare POA — Sarah"); "Ask me first" flags convert to "document why consultation wasn't possible" requirements; if capacity returns, authorities de-activate and consent standing is restored — the system treats incapacity as potentially temporary because it sometimes is.

### 9.3 End of life: memorial / estate mode

On a verified death (FSR-confirmed or documented), the household enters **Memorial mode**:

- **Tone shift first:** all nudges, alerts, tasks, and assistant proactivity stop immediately. No "Ruth's refill is due" ghosts. This is an engineering requirement (every scheduled job must respect the state) and the most important requirement in this section.
- **Read-only preservation:** the record — timeline, documents, decisions, ledger — is preserved read-only, free, for 12 months (billing spec §8). Families consistently describe the record as suddenly precious; we do not paywall grief.
- **Estate workspace:** a purpose-built, limited-write surface opens: executor designation (verified like authority), estate task templates (accounts, Social Security, insurance, subscriptions — the assistant pre-drafts the notification list from connected-source history), document access for probate, compliance export.
- **Authority re-basis:** POAs die with the principal — the product *says so* ("Sarah's financial POA ended at Ruth's death; estate authority now governs") because families dangerously assume otherwise; executor/trustee records replace them.
- **The parent's carve-outs:** honored per her recorded election at ceremony time ("release to executor at death" / "release to all" / "delete"). Default if unelected: release to executor only.
- After 12 months: export everything, archive (small keepsake fee at most), or delete permanently. Deletion honors statutory retention on audit/compliance data only.

### 9.4 Edge cases (required behaviors)

| Edge case | Scenario | Required behavior |
|---|---|---|
| **Estranged sibling** | A sibling exists but the family doesn't invite him; later he demands access, claiming his POA | Harbor takes no side: access is governed by Ruth's consent (capacity) or verified authority (not). His V0 claim unlocks nothing; if he produces documents, §5 verification runs, conflicts flag (§5.3), FSR escalates, attorney referral offered. The audit trail protects the family either way — and protects *him* from suspicion if he's granted access later. The product never adjudicates estrangement; it makes authority factual |
| **Blended family / second marriage** | Ruth remarried; husband Gerald has his own adult children; Sarah's siblings distrust Gerald's access to finances | Gerald joins as Care Partner with family-set grants (e.g., medical Full, financial Summary) — asymmetry disclosed at invite (US-INV-1). Spousal *legal* rights are represented via AuthorityRecords, not assumptions. If Gerald is also aging, see two-recipient support: his children can form *their own household* for him; Gerald-as-recipient and Gerald-as-member are distinct memberships, and the two households share nothing without explicit cross-grants |
| **Two households, one parent** | Ruth winters in Phoenix, summers near a nephew in Minnesota; different aides, pharmacies, and providers per location | One Household, one CareRecipient, **two Location profiles** under the physical domain (contacts, aides, home tasks per location) with a season toggle; medical/financial domains remain unified (the body and the money travel with her). Location-scoped Viewer grants supported (the nephew sees Minnesota physical only) |
| **Two parents, diverging trajectories** | Both parents alive; father declines fast, mother has full capacity and is *also* a caregiver | Household with two CareRecipients: mother holds Parent role for herself AND Care Partner (or Lead) standing for father's care; per-recipient consent and authority; her dignity surface and his transition protocol coexist |
| **Divorced parents** | Both of Sarah's parents need help; they can't be in one workspace and shouldn't be | Two Households; Sarah holds memberships in both; her global account switches context; strict no-bleed of data between households; billing separate (doc 04 handles multi-household discounting) |
| **Care Lead becomes incapacitated or dies** | Sarah has the crash we all fear | Second Care Lead promotion flow (pre-designated successor encouraged at onboarding — "who's your backup?" is a Dana question); if none, Care Partners can invoke an FSR-mediated succession requiring majority of Full-grant members; nothing is orphaned |
| **Family schism / contested control** | Siblings at war; both claim Lead | Product freezes structural changes (Class D lockout) on contested-control flag, preserves everyone's existing read access, escalates to FSR + recommends mediation/attorney; the audit trail and decision log become the neutral record. Harbor is Switzerland with a very good notary |
| **§9.6 Sole child** | No siblings at all | Full model still works: Viewer invites for a trusted friend/relative; two-person floors satisfied per §7.2 substitutes; Parent mirror unchanged. Marketing wedge is siblings; the architecture never assumes them |

---

## 10. Compliance & security posture (summary; full doc owned by Elena)

HIPAA: BAA-backed handling of PHI, minimum-necessary as an *architectural* property (per-domain grants are exactly this), access accounting satisfied by §8. Financial data: credential-less aggregation (OAuth/aggregator rails) wherever supported; read-only scopes by default; write/payment rails only via governed actions. GLBA-aligned safeguards; SOC 2 Type II on the roadmap ahead of health-plan sales (doc 02, Part B). State-law matrix for consent/recording/POA formalities maintained by legal ops. Encryption in transit and at rest; per-household key scoping; staff access governed identically to §2.3 FSR rules (support sessions, time-boxed, family-visible).

---

## 11. Instrumentation (what we watch to know the model works)

- % households with parent consent ceremony completed within 14 days of creation (target: 100% where capacity exists)
- Parent mirror engagement (any modality — including Dana-read-aloud) at 30/90 days
- Grants declined or modified by parents at ceremony (healthy nonzero — 0% means ceremonies are rubber stamps)
- Revocations: count, and *calm vs. conflict* classification from FSR follow-up (doc 01 metric: zero in-anger)
- Two-person approval latency; override rate per household (rising rate = policy misfit or emerging crisis; Dana dashboard flag)
- Audit-feed weekly views by non-Lead members (transparency being *consumed* is the trust metric)
- Transition cases: % using smallest-increment option; % with parent voice recorded; % with completed scheduled reviews

---

*Related docs: `01-...family-perspective.md` (Dignity Principles P1–P6 this spec implements) · `04-feature-spec-billing-payments.md` (BillingGroup, memorial-mode pricing) · `05-mvp-scope-and-release-plan.md` (which slices ship to the first 10 families).*
