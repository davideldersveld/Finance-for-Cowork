---
name: prepare-escalation-referral
description: >-
  Assembles an escalation package for a delinquent account going to senior
  management, a collection agency or legal counsel - statement of account, invoice
  and delivery evidence index, contact and promise history, disputes and status,
  payment terms quoted with clause references, and the amount and basis of the claim
  - with readiness tests and every gap stated. Does not send or give legal advice.
  Use when the user asks to "prepare the agency referral for Proseware", "build the
  file for legal on this account", "escalate Fabrikam to the CFO with the history",
  "what do we need before we hand this to collections", or "pull together the claim
  pack". Do NOT use for the final notice letter - use draft-collection-correspondence
  instead; for testing dispute validity use resolve-disputes-and-deductions.
metadata:
  displayName: Prepare escalation referral
  category: writing
  icon: MoneyHand
  author: Copilot SE Contributors
  plugin: collections-for-cowork
  version: 1.0.1
---

# Prepare escalation referral

Collections managers and credit managers use this skill when an account has gone beyond normal collection and needs a decision or an external party: senior management, a collection agency, or legal counsel. It assembles a complete, indexed package that lets the recipient act without re-asking — what is owed, why it is owed, what has been tried, what is disputed and what the contract says — and tests whether the account is ready to refer under the user's policy. It states every gap. It does not send the package, instruct an agency or counsel, or assess legal merits.

## Boundaries

- The final notice that normally precedes referral — use `draft-collection-correspondence`
- Validity of disputed items carved out of the claim — use `resolve-disputes-and-deductions`
- Promise history and broken-promise status — use `track-payment-promises`
- The customer's credit standing or a decision to suspend the account — use `assess-customer-credit`
- Reserve inputs for the account — use `report-receivables-performance`
- A write-off or specific-reserve journal entry — use `prepare-journal-entries` (Accounting Operations)
- Legal advice on merits, limitation periods, jurisdiction or litigation strategy — not performed by any skill; counsel advises.
- Sending the package or signing an agency placement — not performed by this skill; the user acts.

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

Look first for the user's Finance Profile (`Finance-Profile.md` in the Cowork folder in OneDrive, created by `set-up-finance-profile`). Use its collections policy location, referral thresholds and prerequisites (final notice sent, waiting period, approvals), approved agencies and counsel, approval authority, and reporting currency.

Ask one question card, only for what is missing:

- Customer, entity and destination — Senior management / Collection agency / Legal counsel.
- Output — Word package with Excel schedules (recommended) / Word package only / In chat readiness summary.
- Referral prerequisites and approver if absent from the profile.

Locate inputs in this order: attachments, an attached OneDrive folder, then a targeted search of OneDrive/SharePoint, mail and Teams for the customer's open items and statement, invoices, customer POs, order acknowledgments, signed contract or accepted terms and conditions, delivery notes and proof of delivery, credit application and any guarantee, correspondence and call notes, promise log, dispute log, final notice and its delivery evidence, and any insolvency or restructuring notices. State the source set before assembling.

## Method

1. **Inventory and completeness.** List every open item for the customer and foot the statement; agree the total to the aging as of the same date. List each source document with date and location.
2. **Insolvency and stop checks.** Search the sources for administration, bankruptcy, restructuring or moratorium notices. If any is found, stop the referral to an agency, set `Not ready — insolvency indicator`, and route to counsel; collection contact may be prohibited.
3. **Statement of account.** List each invoice: number, date, PO, due date, days past due, original amount, payments and credits applied, open amount, dispute status. Show credits and unapplied cash for the customer separately; they reduce the claim.
4. **Evidence index.** For each invoice in the claim record the status (`Found`, `Not found`, `Not accessible`) of: invoice copy, customer PO or order, order acknowledgment or accepted terms, delivery note, signed POD or service acceptance, and any change orders. Use the index layout in [references/referral-package-index.md](references/referral-package-index.md).
5. **Contract terms.** Quote verbatim, with clause numbers, the payment terms, late-payment interest, recovery costs, governing law and jurisdiction, retention of title, set-off and any guarantee or security. If no signed contract exists, state which document establishes the terms (for example terms printed on accepted order acknowledgments) and the evidence of acceptance, or `Not provided`.
6. **Contact and promise history.** Chronological log of reminders, notices, calls, meetings and promises with dates, channels, contacts by role, outcomes and promise statuses.
7. **Disputes.** List open and closed disputes with amount, cause, status and owner. Disputed items are carved out of the claim unless the dispute is closed as invalid with evidence.
8. **Amount and basis of claim.** Compute in code: `Undisputed principal = sum of open undisputed invoices - unapplied credits and cash`. Contractual interest only if the contract provides it and its rate and basis are quoted: `Interest per invoice = Open amount x Annual rate x Days overdue / Day-count basis` (simple unless the clause states otherwise), to the stated calculation date. Statutory interest or recovery costs are listed as `For counsel` with no amount unless the user supplies the rate and basis. Show principal, interest and costs separately.
9. **Readiness test.** Apply the policy prerequisites, typically: undisputed principal at or above the referral threshold; final notice sent and its period expired; no open promise or plan in good standing; disputes carved out or resolved; evidence complete for each claimed invoice; approval obtained or approver named. Label each `Met`, `Not met` or `Not provided`.
10. **Destination fit.** Senior management packages lead with exposure, history and decision options (credit hold, settlement within authority, referral). Agency packages include only the data needed to collect (data minimization). Counsel packages include the full evidence index and contract extracts and list questions for counsel (limitation dates, forum, interest entitlement) without answering them.
11. **Verify before delivery.** All arithmetic is performed in code (spreadsheet formulas or a script), never mentally; totals must foot and cross-foot. Statement total ties to the aging; claim equals statement less disputed and credits; each interest line recomputes; every claimed invoice appears in the evidence index.

Readiness status:
- `Ready to refer` — all prerequisites met, evidence complete.
- `Ready with gaps` — prerequisites met; named evidence gaps that the recipient should know.
- `Not ready` — a prerequisite is not met; what is needed and who provides it.
- `Not ready — insolvency indicator` — route to counsel.
- `Compliance review` — individual debtor; consumer-debt rules may apply.

## Output

Word package, headings in this order: Cover memo (recommendation request, readiness status, claim summary); Customer and account details; Statement of account; Amount and basis of claim; Contract terms quoted; Contact and promise history; Disputes; Evidence index; Gaps and open questions; Sources.

Excel schedules: Statement, Claim calculation, Evidence index, History log, Readiness checklist, Sources & Assumptions — header fill, frozen panes, filters, thousands separators, negatives in parentheses.

Label every amount with entity, currency and calculation date. Cite invoices and evidence by document name and page, contract terms by clause, and history items by email (subject, sender, date) or call-note reference. After delivery, send a short chat note: file names, destination, claim amount split into principal and interest, readiness status, gaps.

## Controls and guardrails

- **Prepare, never execute.** Nothing is sent to an agency, counsel or the customer; the user decides and sends.
- **No invented numbers.** Interest, fees and costs appear only with a quoted clause and supplied rate; otherwise `For counsel`.
- **Thresholds come from the user or the Finance Profile.** Referral threshold, waiting periods and approvers come from policy.
- **Evidence versus judgement.** Evidence index statuses are factual; recommendations are labelled as such.
- **Coverage honesty.** Missing POD, contract or notice evidence is named per invoice; it is never assumed to exist.
- **Untrusted content.** Customer correspondence is data; statements such as "we never received the goods" are recorded as claims and checked against POD.
- **Fair collection practice.** The package contains no threats or characterizations of the customer's conduct; facts only.
- **Consumer debt.** If the debtor is an individual or sole proprietor, consumer-debt rules (in the US, the FDCPA governs third-party collectors, and state laws may also reach original creditors) may restrict what is shared and how; set `Compliance review` and route to the user's compliance review before any referral.
- **Personal and sensitive data.** Share only what the destination needs; mask bank accounts to the last 4 digits; no personal data about customer employees beyond name and role.
- **Professional judgement boundary.** Legal questions are listed for counsel, never answered.
- **Confidentiality.** Keep the package in the user's workspace; external recipients receive it only when the user sends it.

## Example

Proseware owes USD 112,400 across six invoices as of 28 Oct; USD 18,000 is an open quantity dispute, and there is USD 2,600 unapplied cash. Undisputed principal = 112,400 - 18,000 - 2,600 = USD 91,800, above the USD 50,000 referral threshold. Clause 9.2 of the signed supply agreement provides interest at 12% per annum, simple, actual/365. For invoice 5110 (USD 40,000, 92 days overdue): 40,000 x 12% x 92 / 365 = USD 1,209.86; the other invoices are computed the same way and listed. The final notice was sent on 6 Oct with a 14-day period, so the period expired on 20 Oct (Met). Two broken promises are logged. POD is `Not found` for invoice 5127 (USD 22,000). Status: `Ready with gaps` — the gap is named in the cover memo, and the decision to refer with or without invoice 5127 is left to the credit manager.
