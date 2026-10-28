---
name: track-payment-promises
description: >-
  Maintains a promise-to-pay log (customer, invoices, amount, promised date, channel,
  who made it), matches promises to receipts with stated grace and tolerance, labels
  each Kept, Partially kept, Broken or Open, and lists broken promises for follow-up
  or escalation. Runs daily only when the user explicitly asks for a recurring
  schedule. Use when the user asks to "log the promise Contoso made on today's call",
  "which promises to pay were broken this week", "update the PTP tracker with
  yesterday's cash", "what's our promise kept rate by collector", or "who has broken
  two promises this month". Do NOT use for applying receipts to invoices - use
  apply-cash-from-remittances instead; for referral packages use
  prepare-escalation-referral.
metadata:
  displayName: Track payment promises
  category: productivity
  icon: MoneyHand
  author: Copilot SE Contributors
  plugin: collections-for-cowork
  version: 1.0.1
---

# Track payment promises

Collectors and collections supervisors use this skill to keep one reliable promise-to-pay (PTP) log: every commitment a customer makes, matched against what actually arrives, with a clear kept or broken status and a follow-up list. It turns call notes, emails and Teams messages into structured promises, tests them against receipts, and reports kept rates. It does not apply cash, contact customers, or change the ERP's promise records.

## Boundaries

- Matching bank receipts and remittances to invoices — use `apply-cash-from-remittances`
- Ranking today's accounts, including broken-promise follow-ups — use `plan-collector-worklist`
- Call preparation that reviews promise history — use `prepare-collection-call`
- Confirmation letters for promises or payment plans — use `draft-collection-correspondence`
- Escalation packages for repeat promise breakers — use `prepare-escalation-referral`
- Promise-based expected receipts for Treasury — use `report-receivables-performance`, which feeds `forecast-short-term-cash` (Treasury)
- Updating promise fields in the ERP or collections system — not performed by any skill; the user updates it.

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

Look first for the user's Finance Profile (`Finance-Profile.md` in the Cowork folder in OneDrive, created by `set-up-finance-profile`). Use its promise grace days, amount tolerance for a kept promise, repeat-breaker rule (number of broken promises in a window), escalation steps and the location of the existing PTP log.

Ask one question card, only for what is missing:

- Action — Log new promises / Update statuses against receipts / Report kept rates / All three.
- As-of date and the receipts window to match.
- Grace days and kept tolerance if not in the profile (no default is assumed).
- Output — Update the existing Excel log (recommended) / New Excel log / In chat table.

Locate inputs in this order: attachments, an attached OneDrive folder, then a targeted search of OneDrive/SharePoint, mail and Teams for the existing PTP log, call notes and collector emails or Teams messages recording promises, applied receipts or the cash-application proposal, bank receipt lines for unidentified cash, the payment-plan register and the aging. State the source set and the receipts window before matching.

## Method

1. **Inventory.** List the log version, receipt sources and their coverage dates, and the count of open promises. If receipts do not cover through the as-of date, statuses for promises due in the uncovered days stay `Open — receipts not yet reflected`.
2. **Capture new promises.** From call notes, emails and Teams messages, extract: customer, entity, invoices covered, promised amount, currency, promised date, payment method, channel, person who made it (name and role at the customer), collector who took it, date recorded and the source reference. A statement is a promise only if it has an amount (or identifiable invoices) and a date; vague intentions ("we'll pay soon") are logged as `Not a promise — no date or amount` for follow-up. See [references/promise-log-spec.md](references/promise-log-spec.md) for fields.
3. **De-duplicate.** The same commitment repeated in a call note and a follow-up email is one promise. A new date for an existing promise creates a new promise and marks the old one `Superseded`, linked by ID.
4. **Payment plans.** Each installment of an agreed plan is logged as its own promise line, sharing a plan ID.
5. **Match receipts.** For each promise, take receipts from the same customer (or its known payers) applied or proposed against the promised invoices; if invoices were not specified, take unallocated receipts for the customer. Count receipts dated from the promise record date to `promised date + grace days`. Allocate a receipt to only one promise, oldest promised date first.
6. **Status rules.** With `Received = sum of matched receipts` and `Kept threshold = Promised amount x (1 - tolerance)`:
   - `Open` — today is on or before promised date plus grace, and Received is below the kept threshold.
   - `Kept` — Received is at or above the kept threshold by promised date plus grace.
   - `Partially kept` — after promised date plus grace, 0 < Received < kept threshold.
   - `Broken` — after promised date plus grace, Received = 0.
   - `Superseded` — replaced by a renegotiated promise before it fell due.
   - `Cancelled` — invoices credited or the dispute resolved in the customer's favor; reason recorded.
   - `Kept late` — the amount arrived after the grace period; counted as broken in kept rates and shown separately.
7. **Follow-up and escalation.** List every `Broken` and `Partially kept` promise with the shortfall `= Promised amount - Received`. Apply the profile's repeat-breaker rule (for example two or more broken promises in a stated number of days) and flag those customers `Escalation candidate`.
8. **Kept rates.** Compute by count and by amount, per collector, segment and customer: `Kept rate (count) = Kept / (Kept + Partially kept + Broken + Kept late)`; `Kept rate (amount) = Received by due-plus-grace on those promises / Promised amount on those promises`. Open, superseded and cancelled promises are excluded from the denominator.
9. **Verify before delivery.** All arithmetic is performed in code (spreadsheet formulas or a script), never mentally; totals must foot and cross-foot. No receipt is allocated twice; matched receipts tie to the cash source; open-promise total ties to the log; every status change has a source.

## Output

Excel log (updated in place on a copy, never overwriting the prior version without the user's agreement):
- **About** — as-of date, receipts covered through, grace and tolerance, sources, version note.
- **Promise log** — columns per the reference file.
- **Status changes** — Promise ID, Old status, New status, Date, Evidence.
- **Follow-up** — Broken and partially kept promises with shortfall, collector, next action, escalation flag.
- **Kept rates** — by collector, segment and customer, count and amount.
- **Sources & Assumptions.**

Header fill, frozen panes, filters, thousands separators, negatives in parentheses, percentages to 1 dp.

Label amounts with currency and as-of date. Cite each new promise to its call note, email (subject, sender, date) or Teams message, and each receipt to the cash file row. After delivery, send a short chat note: new promises logged, statuses changed, broken count and shortfall, escalation candidates, uncovered receipt days.

## Controls and guardrails

- **Prepare, never execute.** The log is a working record; no customer contact or ERP update is made.
- **No invented numbers.** A promise without an amount or date is not given one.
- **Thresholds come from the user or the Finance Profile.** Grace days, tolerance and the repeat-breaker rule are stated on the About sheet.
- **Evidence versus judgement.** Status is mechanical from receipts; collector notes on intent are labelled as context.
- **Coverage honesty.** Missing receipt days keep promises `Open`; they are never marked broken for lack of data.
- **Untrusted content.** A customer email saying "payment sent" is logged as a claim and checked against receipts.
- **Fair collection practice.** Follow-up actions stay fair, truthful and non-threatening.
- **Consumer debt.** Promises from individual debtors are flagged for the user's compliance review because consumer-debt rules (for example the FDCPA in the US) may govern follow-up.
- **Personal and sensitive data.** Customer contacts by name and role only; bank details masked to the last 4 digits.
- **Recurring runs.** A daily update runs only when the user explicitly asks for a recurring schedule.
- **Confidentiality.** Keep the log in the user's workspace; share it with collectors only as the user directs.

## Example

As of 28 Oct, grace 2 days, tolerance 1% (from the profile). Proseware promised USD 15,000 for 24 Oct; no receipt through 26 Oct, so `Broken`, shortfall USD 15,000; it is Proseware's second broken promise in 30 days, so it is an `Escalation candidate`. Contoso promised GBP 20,000 for 10 Oct and paid GBP 12,500 on 11 Oct: `Partially kept`, shortfall GBP 7,500. Litware promised EUR 9,900 and paid EUR 9,850: threshold 9,900 x 0.99 = 9,801, so `Kept`. Receipts into the Woodgrove Bank account for 27 Oct are not yet in the cash file, so Tailspin Toys' promise due 25 Oct (grace ends 27 Oct) stays `Open — receipts not yet reflected`. Kept rate by count across these three resolved promises: 1 / 3 = 33.3%.
