# Segment rulebook template

Use this structure for each segment. Replace bracketed parameters with values from the user or the Finance Profile. Any value the user has not confirmed is labelled `Proposed`.

## Fields per segment

| Field | Content |
|---|---|
| Segment ID | Short stable code, for example `HV-HR` (high value, high risk) or `OV-DSP` (overlay, dispute-led). |
| Entry rule | Exact rule in plain notation, for example `Value tier = High AND Risk band = High AND no overlay`. |
| Channel | Primary and secondary channel: phone call, email, customer portal message, statement, account-manager contact. |
| Pre-due action | Optional courtesy reminder at due date minus [n] days, for high-value or new accounts. |
| Cadence | Touch points in days relative to the due date, for example D+3 reminder, D+10 call, D+20 past-due notice, D+35 final notice. |
| Tone | One of `Courteous reminder`, `Firm and factual`, `Formal`. No tone may threaten, mislead or pressure. |
| Escalation triggers | Days past due and amount at which the policy actions apply: senior collector review, credit hold recommendation, final notice, referral package. |
| Owner | Collector team, senior collector, dispute analyst, or account manager jointly with a collector. |
| Contact limits | Maximum touches per week, permitted hours in the customer's local time, preferred channel honored. |
| Exit rule | When the customer leaves the segment, for example all items current for 60 days. |

## Typical grid (parameters from the user)

| Value \ Risk | Low | Medium | High |
|---|---|---|---|
| High | Account-managed; pre-due reminder; call at D+[n] | Call at D+[n]; senior collector at D+[n] | Call at D+[n]; daily follow-up on promises; credit hold review at D+[n] |
| Medium | Email reminders; call at D+[n] | Email then call; past-due notice at D+[n] | Early call; final notice at D+[n]; referral review at D+[n] |
| Low | Automated reminders and statements | Automated reminders; call if over [amount] | Reminders; final notice at D+[n]; small-balance policy review |

## Overlays (evaluated before the grid, in this order)

1. `Compliance review` — debtor is an individual or sole proprietor; no strategy assigned until the user's compliance review confirms the applicable consumer-debt rules.
2. `Insolvency or legal` — no collection contact; counsel or the insolvency practitioner is the channel.
3. `Payment plan` — contact only on installment due dates and missed installments.
4. `Dispute-led` — dispute analyst owns; collector pursues only the undisputed balance.
5. `Strategic` — account manager informed before any escalation step.
6. `Current only` — pre-due reminders only if the profile asks for them.

## Capacity formula

`Weekly touches required = sum over segments (Accounts in segment x Touches per account per week)`.
`Weekly touches available = Collectors x Productive days x Touches per day` (from the profile).
`Shortfall = Required - Available`; positive values need a cadence or automation decision by the user.
