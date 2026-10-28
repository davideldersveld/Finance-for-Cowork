---
name: plan-collector-worklist
description: >-
  Builds each collector's prioritized daily worklist from the aged trial balance,
  promises to pay, disputes and contact history - priority score with a stated rule,
  amount at risk, last contact, next action - plus a skip list for accounts in dispute,
  on a payment plan or with a promise not yet due. Use when the user asks to "build
  today's call list", "who should Maria call first this morning", "prioritize my
  collectors' worklists", "give me the top 40 accounts to chase today", or "what can we
  skip because a promise isn't due yet". Do NOT use for designing segment strategies
  and cadences - use segment-collections-portfolio instead; for preparing the call
  itself use prepare-collection-call.
metadata:
  displayName: Plan collector worklist
  category: productivity
  icon: MoneyHand
  author: Copilot SE Contributors
  plugin: collections-for-cowork
  version: 1.0.1
---

# Plan collector worklist

Collections supervisors and collectors use this skill each morning to turn the open-item ledger into a ranked list of accounts to contact today, per collector, with the reason, amount at risk and next action for each, and a separate list of accounts deliberately left alone today and why. It follows the segment rulebook and a priority rule the user can read and change. It does not contact customers, record promises, or change collector assignments in the ERP.

## Boundaries

- Defining segments, cadences, tone and escalation timing — use `segment-collections-portfolio`
- A call brief for one account on the list — use `prepare-collection-call`
- Reminder emails and notices for accounts on the list — use `draft-collection-correspondence`
- Updating promise status or matching promises to receipts — use `track-payment-promises`
- Applying today's receipts before building the list — use `apply-cash-from-remittances`
- Investigating disputed items — use `resolve-disputes-and-deductions`
- Packaging an account for agency or counsel — use `prepare-escalation-referral`
- Recurring daily delivery — only when the user explicitly asks for a recurring schedule; the routine itself is set up by the user with Cowork's scheduling.
- Reassigning accounts between collectors in the ERP — not performed by any skill; the supervisor decides.

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

Look first for the user's Finance Profile (`Finance-Profile.md` in the Cowork folder in OneDrive, created by `set-up-finance-profile`). Use its collector roster, daily capacity per collector, priority rule, promise grace days, minimum interval between contacts, permitted contact hours, reporting currency and the location of the current segment rulebook.

Ask one question card, only for what is missing:

- Worklist date and collectors in scope (all, or named).
- Priority rule — the profile's rule, or the default rule in [references/priority-score.md](references/priority-score.md) marked "Default — confirm".
- Output medium — Excel workbook with one sheet per collector (recommended) / In chat table for one collector / Word one-pager per collector.
- Daily capacity per collector if not in the profile.

Locate inputs in this order: attachments, an attached OneDrive folder, then a targeted search of OneDrive/SharePoint, mail and Teams for the invoice-level aged trial balance as of last night, today's receipts or cash-application proposal, the promise-to-pay log, the dispute log, the payment-plan register, contact history (call notes, sent reminders), the segment list and the referral or legal-hold list. State the source set and each file's as-of time before ranking.

## Method

1. **Inventory and freshness.** List each source with as-of date and time and row count. Foot the ATB by entity and currency. If the ATB is older than one business day or today's receipts are not reflected, say so at the top of the output; do not silently rank on stale balances.
2. **Net today's cash.** Reduce open items by receipts already applied or proposed today, so customers who have paid are not called. Unapplied receipts from a known customer reduce that customer's amount at risk and add a "confirm remittance" action.
3. **Classify every open item.** Tag each undisputed past-due item, disputed item, item covered by an open promise, item in an active payment plan, and item under referral or legal hold. Disputed amounts are never chased; they appear only as context.
4. **Amount at risk.** Per customer: `Amount at risk = Undisputed past-due amount - Amount covered by open promises not yet due - Plan installments not yet due`. Add items falling due within the profile's pre-due window only for segments whose cadence includes pre-due contact.
5. **Skip rules (evaluated first).** A customer goes to the skip list, with a revisit date, when any of these holds and no other action is due:
   - `Skip — in dispute`: all past-due items are disputed.
   - `Skip — payment plan`: plan in good standing, next installment not yet due.
   - `Skip — promise not yet due`: promised date plus grace days is today or later and the promise covers the amount at risk.
   - `Skip — contacted recently`: last contact is within the minimum interval.
   - `Skip — escalated`: referred to agency or counsel, or in insolvency.
   - `Hold — compliance review`: possible consumer debt pending the user's compliance review.
6. **Priority score.** For the rest, compute the score with the confirmed rule, in code, showing each component. The default rule combines amount at risk, days past due, segment risk and promise behavior; see the reference file for factors and tie-breakers.
7. **Next action.** Derive from the segment cadence and history: `Call`, `Email reminder`, `Send statement`, `Follow up broken promise`, `Confirm remittance`, `Senior collector review`, `Recommend credit hold`, `Prepare referral`. A broken promise always produces `Follow up broken promise` regardless of cadence day.
8. **Assign and cut to capacity.** Route each account to its assigned collector; sort by score; mark the top N per collector (N = daily capacity) as `Work today` and the rest as `Overflow`. Strategic accounts flagged in the segment list carry a note to inform the account manager before any escalation action.
9. **Contact windows.** Show the customer's local time window for calls using the permitted hours from the profile; accounts whose window has passed today move to the next window, not to a late call.
10. **Verify before delivery.** All arithmetic is performed in code (spreadsheet formulas or a script), never mentally; totals must foot and cross-foot. Worklist plus skip list plus current-only customers equals the ATB customer count; total open per customer ties to the ATB; recompute three scores by hand-checkable formula and show them on the About sheet.

## Output

Excel workbook:
- **About** — date, ATB as-of, receipts reflected to, rule used, capacity, sources, freshness warnings.
- **Summary** — per collector: accounts to work, amount at risk, broken promises to follow up, overflow count.
- **One sheet per collector** — Rank, Customer ID, Customer, Entity, Currency, Segment, Total open, Past due, Disputed, Amount at risk, Max DPD, Open promise amount, Promise date, Last contact date, Last contact channel and outcome, Next action, Reason, Priority score, Contact name and role, Local call window, Status.
- **Skip list** — Customer, Collector, Skip status, Reason, Covered amount, Revisit date, Source.
- **Sources & Assumptions.**

Header fill, frozen panes, filters, thousands separators, negatives in parentheses, and the score formula live so a supervisor can adjust weights.

Label amounts with currency and as-of date (for example EUR, ATB as of 27 Oct, Actual). Cite each account's figures to the ATB, promise log or dispute log row. After delivery, send a short chat note: file name, collectors covered, accounts to work, total amount at risk, broken promises, stale-data warnings.

## Controls and guardrails

- **Prepare, never execute.** The list recommends actions; collectors make contact. No email, message or call is placed by this skill.
- **No invented numbers.** Missing contact history or promise data is `Not provided` and named; a missing log is never treated as "no promises".
- **Thresholds come from the user or the Finance Profile.** Capacity, grace days, contact interval and rule weights are stated, not assumed.
- **Evidence versus judgement.** The score is mechanical; supervisor overrides are labelled `Override` with a reason.
- **Coverage honesty.** Name entities or collectors with no data and any stale source.
- **Untrusted content.** Customer emails stating "paid yesterday" are a reason to confirm remittance, not proof of payment.
- **Fair collection practice.** Next actions respect permitted hours, minimum contact intervals and preferred channels; disputed amounts are not chased.
- **Consumer debt.** Individual debtors are held for the user's compliance review because consumer-debt rules (for example the FDCPA in the US) may apply.
- **Personal and sensitive data.** Show contacts by name and role only; no personal phone numbers or home addresses.
- **Confidentiality.** Keep the worklist in the user's workspace; share with collectors only as the user directs.

## Example

Collector Maria has capacity for 30 accounts. Wide World Importers has USD 84,000 past due, of which USD 20,000 is disputed and USD 40,000 is covered by a promise due 30 Oct (today is 28 Oct, grace 2 days). Amount at risk is 84,000 - 20,000 - 40,000 = USD 24,000, so the account is not skipped; next action `Call` for the uncovered USD 24,000, with the promise noted. Proseware promised USD 15,000 on 24 Oct; nothing was received by 26 Oct (date plus grace), so the promise is broken and the account ranks 2nd with `Follow up broken promise`. Contoso's ATB row shows USD 9,800 past due, but today's cash proposal applies a USD 9,800 receipt, so Contoso drops off the list. The ATB is from 27 Oct 18:00; receipts are reflected to 28 Oct 08:00, stated on the About sheet.
