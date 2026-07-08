# Product Mockup Notes — Harbor Account, Login, Payment & Trust Surfaces

*Companion to the five HTML review boards in this folder. Direction A ("Harbor") — the lead brand candidate.*
*Demo data: the fictional Reyes family — Elena Reyes, 79, Tucson; Marisol (Chicago, Care Lead), Daniel (Seattle, Care Partner), Ana (Austin); FSR Grace Whitfield.*

---

## Why these screens, and why now

The stakeholder synthesis was explicit (decision #4): **account, login, payment, and permission flows get designed now**, because — as Elena-the-compliance-lead put it — *"trust is visual before it's contractual."* These are the screens where a family decides whether to hand over bank credentials and MyChart access. They are not plumbing; they are the product's first and most repeated trust argument.

Each HTML file is a self-contained design-review board: labeled frames (screens) with short annotations explaining intent, so reviewers can evaluate the flow the way a family will experience it — sequentially, under stress.

## File map

| File | Surface | Trust question it answers |
|---|---|---|
| `01-signup-onboarding.html` | Account creation → parent consent → FSR call | "Will this respect my mom before it ever touches her data?" |
| `02-login-security.html` | Login, 2FA, magic link, parent login, new-device notice | "Is my family's most sensitive information actually guarded?" |
| `03-plans-payment.html` | Tiers, sibling cost-split, payment, invoice, billing settings | "Is this company honest about money — with us and between us?" |
| `04-family-permissions.html` | Roles, visibility matrix, approvals, consent dashboard, audit trail | "Who can see what, who can do what, and does Mom get a say?" |
| `05-account-settings.html` | Profile, connected accounts, security, care team, data & privacy | "Do we stay in control after we've said yes?" |

---

## How trust is expressed visually

1. **Trust signals on every sensitive screen, never as decoration.** Every screen that touches PHI, money, or credentials carries a lock-icon trust bar ("Bank-level encryption · HIPAA-aligned · You decide who sees what") placed *in the reading path*, not the footer basement. The claim is always paired with a control the user can actually exercise — a "who can see this" note, a toggle, an audit link. Trust language without an affordance reads as marketing; trust language next to a working control reads as policy.

2. **A named human beside every hard moment.** 2FA trouble, consent conversations, billing questions, urgent changes — each surfaces Grace (the FSR) or a real phone number, not a support queue. Per Dana's insight in the synthesis: the human is the retention product. Visually this appears as a recurring warm card pattern: avatar + name + role + direct contact.

3. **Calm, not sterile; serious, not scary.** Cream (#f7f4ee) and soft white grounds, sage/teal accents, deep trust blue (#4e7a86) reserved for primary actions. Serif (Georgia) headlines carry warmth and institutional permanence; system sans carries the working UI. Destructive and warning states use a warm terracotta (#a65b4b) rather than alarm red — families in a hard season don't need the interface to shout.

4. **Transparency as architecture.** The visibility matrix, the who-pays-what ledger, the audit trail, and the "everyone was notified" strips all make the same argument: nothing here happens silently. The audit trail is deliberately symmetric — the parent can see who looked at her records, and the remote sibling never has to interrogate the Care Lead. It is the anti-resentment machine.

5. **Honesty as a visual pattern in payment.** Equal visual weight for upgrade *and* downgrade. The Connected tier openly states what it lacks. The scholarship/income-scaled entry point sits at the decision point (plan selection and billing settings), not buried in an FAQ. Pause-for-hospitalization is one calm card. These are deliberate anti-dark-pattern signals: retention through decency, not friction.

6. **Security framed as a family practice.** New-device sign-ins notify the whole family — including Elena, in her large-print format. In an eldercare context, unusual access is a trust event and an elder-financial-abuse vector, so the perimeter is social, not just technical. Two-person confirmation for money moves protects the parent from exploitation *and* the Care Lead from suspicion.

---

## Accessibility choices

- **Large type as default, not a mode.** Body copy runs 17–18px minimum on family screens; the assumed user is stressed, tired, and often 45–60. Parent-facing screens step up to 20–24px with 56–64px touch targets.
- **The parent's login has no password.** Elena signs in via a texted code or an optional large-keypad PIN. Help routes to a named family member and a human phone line. Nobody should ever feel locked out of their own life by a credential.
- **One idea per screen in flows.** Onboarding steps ask a handful of questions each, with a persistent "why we ask" sidebar so nothing feels extractive.
- **Structural accessibility.** Semantic HTML throughout: real tables (with scoped headers) for the visibility matrix and audit trail, labels above inputs, checkbox-backed toggle switches, visible 3px focus rings keyed to the trust blue, aria-labels on icon-only buttons, and WCAG-AA contrast (secondary text never lighter than #5e6d76 on cream).
- **Forgiving, blame-free copy.** "It happens to everyone — especially in a stressful season." No "invalid credentials," no red-alert lockout language, resend/fallback paths on every auth screen, and a phone-a-human escape hatch at each potential abandonment point.
- **Responsive without reflowing the mental model.** Grids collapse to single columns; wide tables scroll inside their own containers; nothing hides behind hover.

---

## The parent-dignity thread ("I'm not a project — ask me first")

Ruth's line from the research is the moral constraint on the whole system, and it is made *operational*, not ceremonial, across the five boards:

- **Sign-up (board 1):** Step 2 asks "what should we call her," offers no clinical diagnosis dropdowns, and states that nothing is shared until Elena is asked. Step 4 — "Asking Mom first" — is a full, unskippable step with three consent channels sized to her comfort: her own large-type invitation, a **printed letter** with a reply card, or a **phone call** with Grace at a time she chooses. The POA path exists but is document-verified by a human, not a checkbox.
- **Login (board 2):** Elena gets her own first-class sign-in — large type, one big button, plain words, help from named people. She is a user, not a subject.
- **Payment (board 3):** "Elena never pays and never sees a bill unless she asks to." Money friction stays between the siblings, by design, and each sibling pays their own share so no one fronts money or chases family.
- **Permissions (board 4):** The centerpiece. Elena has her own consent dashboard — "What my family can see" — with large revoke controls and a promise that changing her mind is blame-free. Financial visibility changes require her okay; payments over the family's threshold route to *her* for approval in plain language ("Marisol wants to pay your home-care team $1,240. Okay?"). Consent is re-confirmable, revocable, and logged.
- **Settings (board 5):** She sets her own notifications on her own device. Disconnect flows preserve her consent lineage ("Elena approved this connection"). Deleting the workspace notifies her — it's her information too. And **Memorial mode** ends the relationship the way it was conducted: billing stops the day the family tells us, records stay available for estate needs, and Grace reaches out once, personally. No upsells, no automated cheerfulness.

The test we applied to every frame, from the brand strategy's evaluation criteria: *Would Sarah trust it at 11pm after a bad phone call? Would Ruth feel dignified seeing her family use it?* Each annotation on the boards records how that frame earns its yes.

---

## Implementation notes for the build team

- Every board is a single self-contained HTML file: inline CSS, inline SVG icons/avatars, minimal vanilla JS used only for tab/step/toggle interactions and the live cost-split calculator. No external fonts, CDNs, or images — the boards can be reviewed offline or attached to an email.
- Shared tokens across all five files: cream #f7f4ee, soft white #fffdf9, sage #8fae9d, teal #7ea9b3, trust blue #4e7a86, sand #d7c1a6, ink #23313a, slate #5e6d76; Georgia serif headlines, system sans body; 22px-radius screen frames, 16px-radius cards, 12px-radius inputs.
- Demo data is consistent across boards so a stakeholder can follow the Reyes family end-to-end from sign-up through settings.
