# Product Definition — The Family's Perspective

*Product definitions series, doc 1 of 5*
*Status: Draft v1 for internal review · 2026-07-06*
*Working product name: **Harbor** (brand direction still under evaluation — see `branding/01-brand-strategy.md`; "Harbor" used throughout as placeholder)*

---

## Purpose of This Document

Every other document in this series describes Harbor from the company's seat — architecture, billing, go-to-market. This one describes it from the seats that actually matter: the three chairs at the family's kitchen table.

Harbor serves one family unit with (at least) three distinct users who have **different jobs, different anxieties, different definitions of success, and different reasons to quit**. If we design for "the caregiver" as a single persona, we build the wrong product. The stakeholder meeting made this unmistakable:

> Sarah: "I spend 10 hours a week logging into portals. My brothers think I'm hiding things."
> Mike: "I find out about Mom's ER visit three days later in a group text."
> Ruth: "I'm not a project. Ask me first."

The product must resolve all three sentences simultaneously. That is the whole product.

---

## The Family Unit as the Product's Atom

Harbor's unit of value is not a user account — it's a **household**: one aging parent (or couple), 2–5 adult children distributed across geographies, and the surrounding care ecosystem (providers, facilities, aides, advisors). The reference family for this document:

| Person | Age | Location | Role in family | Harbor role |
|---|---|---|---|---|
| **Ruth** | 81 | Phoenix, AZ | The parent. Widowed 3 years. Early cognitive decline (MCI diagnosis, Feb 2026). Lives alone, still drives locally. | **Parent** (own consent surface) |
| **Sarah** | 52 | Chicago, IL | Eldest. De facto coordinator — the "unpaid COO." Has healthcare + financial POA (springing). | **Care Lead** |
| **Mike** | 48 | Portland, OR | Middle child. Wants to help, chronically out of the loop. Handles what he's asked to, when he knows to. | **Care Partner** |
| *(Jenny)* | 45 | Phoenix, AZ | Youngest, lives 20 min from Ruth. Does the physical drop-ins. Not in the founding personas but present in most real families — included in scenarios where sibling load-balancing matters. | **Care Partner** |
| **Dana** | — | Harbor | Family Success Representative. Onboarded the family, does monthly check-ins (Supported tier). | **FSR** (internal role) |

The family is on the **Supported tier ($149/mo)**, split three ways between the siblings (see `04-feature-spec-billing-payments.md`).

---

## Persona 1 — Sarah, the Care Lead

### Who she is when she opens the app

Sarah opens Harbor at 6:40am before work, at lunch, and at 10:30pm after her own kids are asleep. She is not exploring software; she is triaging. Her emotional state on open is some blend of *worried, behind, and quietly resentful*. She has been the family's single point of failure for two years.

### Jobs-to-be-done

| # | Job statement | Underlying anxiety | Today's workaround |
|---|---|---|---|
| S1 | When something changes in Mom's health, finances, or daily life, I want to know within hours, so that I'm never the last to find out about something I'm responsible for. | "What am I missing right now?" | 7 portal logins, calls to Jenny, hoping the facility calls |
| S2 | When my brothers ask "what's going on with Mom," I want them to already have the answer, so that I stop being the family's information API. | "They think I'm hiding things." | 40-message group texts, forwarded PDFs, a shared Google Doc no one updates |
| S3 | When a task needs doing (refill, bill, appointment, follow-up), I want it assigned to a named person with a due date, so that work stops defaulting to me by proximity of guilt. | "If I don't do it, no one will." | Her own to-do app; asking, nagging, then doing it herself |
| S4 | When I take a financial action on Mom's behalf, I want a record my siblings can see, so that no one can ever question my integrity. | "One day someone will ask where the money went." | A spreadsheet she maintains defensively |
| S5 | When Mom has a medical event, I want the full picture (meds, history, recent notes, insurance status) in one place I can pull up from an ER waiting room, so that I can advocate competently from 1,700 miles away. | "The 11pm phone call." | A binder in Chicago, a fatter binder in Phoenix, and her memory |
| S6 | When care decisions loom (driving, moving, memory care), I want a shared factual baseline and a decision trail, so that family arguments are about values, not about whose facts are right. | "The Thanksgiving fight." | Nothing. This is where families break. |

### A day in the life

**Before Harbor — Tuesday, March 2026**

- 6:15am — Logs into MyChart to check whether Mom's cardiology follow-up got scheduled. It didn't. Adds "call cardiology" to her list.
- 12:30pm — On lunch break, calls Mom's bank about a $340 charge she noticed Sunday. 25 minutes on hold. Can't resolve it — she's an authorized viewer, not a signer, on this account.
- 3:00pm — Text from Jenny: "Mom seemed off today, kept asking about Dad." Sarah screenshots and forwards to Mike, who replies at 7pm with "should we be worried?" She doesn't have an answer.
- 9:45pm — Logs into Medicare.gov to check a claim denial. Password reset required. Gives up.
- 10:30pm — Updates her spreadsheet. Answers Mike's second text ("did you deal with the bank thing?") with more edge than she intended. Lies awake doing an inventory of everything she might have missed.

**Time spent: ~2.5 hours. Items actually resolved: zero. Family trust: net negative.**

**After Harbor — the same Tuesday**

- 6:40am — Opens Harbor. Dashboard summary: *"2 items need attention. Cardiology follow-up not yet scheduled (due within 14 days of discharge — 9 days left). Unusual charge of $340 at [merchant] flagged on the Chase checking account."* Both already exist as tasks.
- 6:44am — Assigns "schedule cardiology follow-up" to the AI assistant, which drafts the outreach; assigns "investigate $340 charge" to Mike with the account context attached — Mike has financial visibility and it's his turn. Done before coffee.
- 3:00pm — Jenny logs a visit note from her phone: "Mom seemed off, kept asking about Dad." It lands in the shared timeline, tagged to the cognitive-health thread, visible to everyone at once. The assistant notes it's the second such observation in three weeks and suggests mentioning it at the cardiology visit; Sarah accepts the suggestion, which adds it to the appointment prep sheet.
- 9:30pm — Checks Harbor once. Mike resolved the charge (a legitimate but forgotten annual insurance premium — he called, confirmed, and left a note). Cardiology appointment is confirmed for the 19th; it's on the family timeline, and Jenny already claimed the "drive Mom" task.
- Goes to bed. Does not text anyone. Does not update a spreadsheet.

**Time spent: ~20 minutes. Items resolved: 2 of 2. Mike did real work. Jenny's observation reached everyone instantly and became clinically useful.**

### Features Sarah touches (frequency-ordered)

1. **Dashboard / "What changed, what needs action, who's handling it"** — every session
2. **Alerts & anomaly flags** (financial anomalies, missed refills, appointment gaps) — daily
3. **Task assignment with named owners and due dates** — several times/week
4. **AI assistant chat** — "summarize the discharge notes," "what meds is Mom on and when do refills hit," "draft a message to Dr. Okafor" — several times/week
5. **Shared family timeline** (visits, events, notes) — daily read, weekly write
6. **Financial view** — balances, bills due, claims, the transparency ledger — 2–3x/week
7. **Appointment prep sheets** — before every appointment
8. **Decision log** — at every major fork (driving, home care hours, facility research)
9. **Dana (FSR) check-ins and escalation** — monthly, plus crises
10. **Permissions administration** — rarely, but she is the one who does it

### What success feels like to Sarah

- She checks Harbor **instead of** seven portals — the login count is the metric she'd cite unprompted.
- Sunday-night dread is replaced by a five-minute review.
- The sentence "just look in Harbor" ends conversations that used to take an hour.
- Her brothers do 30–40% of tasks by count, visible in the task ledger — and she didn't have to assign guilt to get there.
- At Ruth's next hospitalization, she answers the ER physician's medication question in 30 seconds from her phone, and Mike knows within the hour without her sending a single text.
- She would say: **"I'm still the lead, but I'm no longer alone, and no one wonders what I'm doing anymore."**

### What would make Sarah churn

| Churn driver | Mechanism | Design countermeasure |
|---|---|---|
| **Stale data** | One wrong medication list or missed balance update and she reverts to checking source portals "just to be sure" — at which point Harbor is a duplicate chore, not a replacement | Freshness timestamps on every synced datum; explicit "last verified" labels; degrade honestly ("we couldn't reach MyChart since Tuesday") rather than silently |
| **Harbor becomes another inbox** | If notifications are noisy, Harbor joins the group text as a source of stress | Severity-tiered alerts; digest-by-default; "urgent" reserved for genuinely urgent |
| **Siblings don't adopt** | If Mike never logs in, Sarah is paying to maintain a dashboard for an audience of one | Onboarding is a *family* ceremony, not a solo signup; sibling-specific digest emails that deliver value without login; FSR check-ins ask about sibling engagement explicitly |
| **The crisis passes** | Post-crisis, the perceived need drops (Dana: "they churn when the crisis passes") | Proactive-monitoring value between crises; monthly FSR check-in as the retention product; pause option instead of cancel (see billing spec) |
| **Trust breach** | Any security incident, any surprise about who saw what, any hint her data trains something | Visible audit trail, plain-language privacy posture, no dark patterns anywhere near PHI/financial data |

---

## Persona 2 — Mike, the Care Partner

### Who he is when he opens the app

Mike opens Harbor two or three times a week, usually from a push notification or the weekly digest. His emotional state is *guilty, willing, and wary of being managed*. He loves his mother, trusts his sister about 85%, and hates that the remaining 15% exists.

### Jobs-to-be-done

| # | Job statement | Underlying anxiety | Today's workaround |
|---|---|---|---|
| M1 | When something significant happens with Mom, I want to know at the same time Sarah does, so that I'm a participant, not an audience. | "Three days later, in a group text." | Refreshing the group text; calling Mom, who says "I'm fine, honey" |
| M2 | When I have 2–4 hours a week to contribute, I want concrete tasks I can complete from Portland, so that helping doesn't require plane tickets or mind-reading Sarah. | "I want to help but I don't know how." | Asking "what can I do?" and getting "nothing right now" (which both of them know is false) |
| M3 | When money moves in Mom's accounts or care costs come up, I want to see the same numbers Sarah sees, so that I never have to choose between auditing my sister and trusting her blind. | "I'm not accusing anyone, I just want to see it." | Not asking, and letting the not-asking curdle |
| M4 | When I talk to Mom on Sundays, I want enough context to have a real conversation, so that she doesn't have to be my news source about her own decline. | "I asked about the doctor and she couldn't remember going." | Debriefing Sarah before or after calls |
| M5 | When family decisions come up, I want the facts before the family call, so that I can weigh in as an informed equal rather than either rubber-stamping or reflexively pushing back. | "By the time I hear about it, it's already decided." | Contrarianism as a proxy for participation |

### A day in the life

**Before Harbor — a Thursday**

- 8:00am PT — Group text from Jenny, sent 10:47pm the previous night: "FYI mom went to urgent care yesterday, she's fine, UTI." Mike reads it in the elevator. *Yesterday?* He texts three questions. Jenny is at work; answers trickle in until 2pm.
- 12:15pm — Calls Mom. She says the doctor was "very nice" but can't say what was prescribed. Mike doesn't know if that's the MCI or normal 81-year-old vagueness. This distinction — which he can never make — is quietly eating him.
- 6:30pm — Calls Sarah. She's at his nephew's game; the call is short and logistical. He hangs up knowing slightly more and feeling slightly worse. He offers to "take something off her plate." Neither of them can name what.

**After Harbor — the same Thursday**

- 7:15am PT — Push notification (family-visible event, high tier): *"Ruth had an urgent care visit yesterday, 3:40pm. Diagnosis: UTI. Prescribed nitrofurantoin, 5 days. Jenny drove her; visit note attached. The assistant checked for interactions with her current medications: none. Follow-up: none required unless symptoms persist past Monday."* Mike knows the same facts, at the same time, in the same words as everyone else.
- 7:18am — Taps the open question in the thread — *"pharmacy pickup for Saturday refill, Jenny has a conflict"* — and claims it: he arranges pharmacy delivery from his phone in six minutes. A real contribution, executed from 1,300 miles away, before breakfast.
- 12:15pm — Calls Mom. He knows about the UTI but lets her tell it her way. Because he isn't interrogating her for facts he can get elsewhere, the call is just a call. She tells a long story about the urgent-care nurse's tattoos. It's the best conversation they've had in a month.
- Sunday — Weekly digest: 2 appointments upcoming, finances quiet, one task open (his, done), a note from Dana about the next check-in. Five-minute read. He goes back to his weekend.

### Features Mike touches

1. **Weekly digest** (email/push) — his primary surface; must deliver standalone value
2. **Event notifications with full context** — the "same facts at the same time" mechanism
3. **Claimable task queue** — remote-executable tasks (calls, research, admin, bill wrangling) surfaced to him specifically
4. **Financial view (read)** — the passive transparency that dissolves the 15%
5. **Timeline / visit notes** — read-mostly; pre-call context before Sunday calls
6. **AI assistant** — occasional: "catch me up on the last month," "explain this Medicare denial"
7. **Decision log** — participates in structured decisions; sees rationale, not just outcomes

### What success feels like to Mike

- He finds out about events in **minutes, not days**, from the system, not from a sibling's discretionary text.
- He completes 2–5 real tasks a month that Sarah never had to think about.
- He has looked at the finances four times, found them boring, and stopped worrying — *transparency consumed passively is the product working.*
- Sunday calls with Mom are about her, not about extracting a status report.
- He would say: **"I finally know what's going on, and I finally have a way to actually help."**

### What would make Mike churn (or disengage, which precedes churn)

| Driver | Mechanism | Countermeasure |
|---|---|---|
| **Feeling surveilled into service** | If Harbor becomes Sarah's tool for assigning him work and tracking his compliance, he'll resent it and lapse | Tasks are *claimable* first, assignable second; contribution stats visible to self by default, never weaponized in-product (no leaderboards, no "Sarah completed 34 tasks, you completed 3" framing) |
| **Notification fatigue** | Over-notify and he mutes; mute and he's back to three-days-later | Tiered severity with sane defaults; urgent = ER/safety/fraud only |
| **Read-only theater** | If everything meaningful still routes through Sarah and Harbor is just her spreadsheet with a login, he stops opening it | Remote-executable tasks as a first-class object; assistant can execute legwork *he* initiates |
| **Paying his split for something he doesn't use** | The cost-split makes him a payer; unused payments get cancelled | The digest must justify his $49.67/mo by itself, even in months he never logs in |

---

## Persona 3 — Ruth, the Parent

### Who she is when she encounters the product

Ruth did not buy Harbor and would not have. She encounters it in three ways: **the consent conversations** (with Dana and with her children), **her own surface** (a radically simplified view — large type, her calendar, her people, and a "who can see what about me" panel), and **its side effects** (children who visit her life instead of auditing it).

Ruth is not a "user" in the engagement-metrics sense, and we should never measure her like one. **She is the person the product is about, and the person with the strongest moral claim on its design.** Her MCI is early: she manages her days, forgets recent conversations, has stopped driving at night by her own choice, and is acutely aware of — and frightened by — the trajectory. Her fear is not death. It is being *managed*: talked over, decided about, turned into a project run by her children.

> "I don't want my kids reading my bank statements behind my back. Ask me first."

### Jobs-to-be-done

| # | Job statement | Underlying need |
|---|---|---|
| R1 | When my children coordinate my care, I want to be asked before, not informed after, so that I remain the author of my own life. | Agency |
| R2 | When someone accesses my medical or financial information, I want to know who and what, so that transparency runs in *both* directions. | Reciprocity — the audit trail is for her too |
| R3 | When I'm still capable of a decision, I want to make it — even if my kids would decide differently, even if I decide slowly. | The right to her own risk |
| R4 | When my capabilities decline, I want the handover to happen gradually, per-domain, with my participation, so that one bad day doesn't become a coup. | Graceful transition, not a switch |
| R5 | When my kids talk to me, I want to talk about life, not logistics, so that I'm still their mother and not their case. | Relationship preservation |
| R6 | I want some things to stay private — my spending on small pleasures, some conversations with my doctor — for as long as possible. | A private interior, at any age |

### A day in the life

**Before Harbor**

Tuesday. Jenny drops by, casually opens the mail "to help," and asks about a bill in a tone Ruth doesn't like. Sarah calls at 6; the call is fourteen questions long — the doctor, the pills, the bank, the car. Ruth answers what she remembers and improvises the rest, because saying "I don't remember" out loud to her daughter costs more than a small lie. After the call she sits with the specific loneliness of being loved as a problem. She has started keeping some mail in a drawer, unopened, so there's less to be asked about. (This — the drawer — is the exact behavior that gets her into real trouble in eight months, and it is *caused* by the surveillance, not solved by it.)

**After Harbor**

Tuesday. Jenny drops by and they do a crossword; the mail is boring now because bills are visible to the family through channels Ruth *agreed to*, in a ceremony where Dana walked her through every toggle and Ruth said no to two of them (her personal checking's transaction detail — the kids see the balance is healthy, not what she buys — and her therapist's notes). Sarah calls at 6 and asks zero logistics questions, because she doesn't need to. They talk about Sarah's daughter's college essay. Ruth's tablet shows tomorrow: "Dr. Okafor, 10:30. Jenny is driving you. She'll arrive 9:45." When Ruth opens her "My Harbor" view, a plain-language panel tells her: *"This week: Sarah viewed your medication list (twice) and your Chase balance. Mike viewed your calendar. Nobody viewed anything you haven't shared."* She checks it the way you check a lock you already know is locked. It is hers.

### Features Ruth touches

1. **Consent ceremonies** — the structured, witnessed, revocable grants of visibility (see `03-feature-spec-accounts-identity-permissions.md`); performed with Dana at onboarding and revisited at each check-in
2. **"Who sees what about me"** — her plain-language mirror of the permission model, always current, always available, on paper too if she prefers
3. **My Harbor view** — her calendar, her people, her rides, big type, no dashboards, no metrics, nothing that scores her
4. **The "Ask Ruth first" flag** — decision types she has marked as requiring her voice before family discussion concludes (housing, driving, spending over a threshold she set)
5. **Revocation** — one conversation (with Dana or in-product) withdraws any grant; the family is notified *that* a grant changed, and the system honors it immediately
6. **Voice/phone access** — she can call Dana; the product must never assume she'll use an app

### Parent-Dignity Design Principles

These are product law, not aspirations. Every feature spec in this series must state its compliance with them. They operationalize the meeting's moral constraint ("the parent's dignity is non-negotiable").

**P1 — Consent-first, and consent means asked, not notified.**
No data source about Ruth is connected, and no visibility granted, without her explicit consent while she has capacity — captured in a ceremony she understands, in language she'd use, revocable by her at any time. Where a POA is exercised *instead of* consent (because capacity is gone), the product says so honestly in the record: "authorized under POA" is never dressed up as "Ruth agreed."

**P2 — Visibility runs both ways.**
Every access to Ruth's information is logged, and the log is *hers to read* in plain language. The children see her accounts; she sees them seeing. Asymmetric surveillance is what the drawer-full-of-mail was defending against. Reciprocal transparency is what replaces it.

**P3 — Agency preserved as long as cognition allows — per domain, not globally.**
Capacity is not binary and not global. Ruth may lose track of bills years before she loses the ability to choose where she lives. Permissions, defaults, and decision rights are scoped per domain (medical / physical / financial) and transition independently. The product never offers a single "take over everything" switch.

**P4 — Graceful transition, not a coup.**
Decline-driven transitions follow a protocol: raised at an FSR check-in or by documented clinical trigger → discussed with Ruth present and participating to her ability → changed in the smallest increment that solves the actual problem → recorded in the decision log with her voice included (her words, even dissenting, are part of the record). One-click emergency overrides exist for genuine safety events — and generate a prominent, non-suppressible audit entry plus a mandatory FSR follow-up.

**P5 — Never the product's subject, always its member.**
Ruth is a member of the household with a role, a surface, and standing — not a "care recipient" data object. Copy rules: the product never describes her in the third person on screens she can see ("Ruth's compliance" is banned; "Mom's medication schedule" appears only on the children's surfaces, never hers). No engagement scoring, no gamification, no "senior-proofing" condescension in her UI. Marketing may never depict her as a burden or a data source.

**P6 — A private interior is honored to the end.**
The permission model must support carve-outs (specific accounts, specific note types) that remain outside family visibility. The system does not treat maximal transparency as maximal virtue. Some drawers stay hers.

### What success feels like to Ruth

- Conversations with her children measurably shift from logistics to life. (We will actually ask her this — the FSR check-in includes the parent by design.)
- She has said "no" to something in the permission model, the "no" held, and nobody fought her about it.
- She knows — with the certainty of having the panel in her hands — who sees what.
- Nothing about her situation is a surprise to her.
- She would say: **"They ask me first. I'm still me."**

### What would make Ruth revoke, resist, or sabotage

(Ruth doesn't "churn" — she *withdraws consent*, or quietly defeats the system: the drawer, the improvised answers, refusing the tablet. Parent sabotage is the failure mode that kills the household account from the inside.)

| Driver | Mechanism | Countermeasure |
|---|---|---|
| **Discovering surveillance she didn't grant** | One "how did you know that?" moment from a child and all trust in the system is gone, unrecoverable | Consent ceremony completeness; both-ways visibility (P2); FSR verifies her understanding at check-ins |
| **Being talked about, not with** | Overhearing herself described as a dashboard | Copy rules (P5); "Ask Ruth first" flags; her presence in check-ins |
| **A transition that felt like a coup** | Waking up one day with financial access removed after one forgotten bill | Transition protocol (P4); smallest-increment rule; her voice in the decision log |
| **Condescension in her own UI** | Cartoon oldsters, "great job!" confetti, baby-talk copy | Dignity review as a release gate for any parent-facing surface |
| **Complexity that exposes her decline** | An interface that makes her feel her deficits every time she uses it | My Harbor view designed for her *current* self; phone/Dana as an always-available modality; no feature of hers ever requires remembering a prior session |

---

## Cross-Persona Requirements (What the Family Needs *Together*)

1. **One ground truth.** Every family member — and the FSR — sees the same facts, timestamped, with provenance. Disagreements about facts should become structurally impossible; only disagreements about judgment remain, and those get the decision log.
2. **Provenance and freshness on everything.** "Chase, synced 2h ago." "MyChart, synced Mar 12 — connection needs re-auth." Trust is earned by admitting staleness, not by hiding it.
3. **Asymmetric surfaces, symmetric truth.** Sarah gets an operations console; Mike gets a digest and a task queue; Ruth gets a calendar and a mirror. Same data, three radically different products — by design, not by feature-flagging an afterthought.
4. **The FSR is in the product, not behind it.** Dana is visible in the sidebar, schedulable, escalatable, and present at the moments the family would otherwise fight (onboarding grants, decline transitions, the first financial anomaly). Per the meeting: her check-ins *are* the retention product.
5. **Emotional register: calm hand on the shoulder.** Alert copy, empty states, error states — all written for someone reading them scared at 11pm. No red unless something is truly urgent. No cheerfulness where cheerfulness would be obscene.

---

## Success Metrics from the Family's Seat

| Persona | Metric | Target (first 10 families, 90 days) |
|---|---|---|
| Sarah | Self-reported weekly coordination hours | ≥50% reduction from onboarding baseline |
| Sarah | Source-portal logins/wk (self-reported) | From ~7 to ≤2 |
| Mike | Time-to-awareness of significant events | <4 hours (vs. days) |
| Mike | Tasks completed by non-lead siblings | ≥30% of household task volume |
| Ruth | "I know who sees my information" (check-in question, 1–5) | ≥4.5 |
| Ruth | "My family asks me before deciding" (check-in question, 1–5) | ≥4.0, non-declining |
| Family | "We argue less about Mom's care" (all siblings, 1–5) | ≥4.0 |
| Family | Consent grants revoked in anger (vs. adjusted calmly) | 0 |

---

*Related docs: `02-product-definition-buyer-perspective.md` (who pays and why) · `03-feature-spec-accounts-identity-permissions.md` (the machinery behind P1–P6) · `05-mvp-scope-and-release-plan.md` (what the first 10 families actually get).*
