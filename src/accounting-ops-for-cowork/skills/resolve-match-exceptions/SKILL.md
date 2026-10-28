---
name: resolve-match-exceptions
description: >-
  Diagnoses invoices blocked by two- or three-way match - price and quantity
  variances, missing goods receipts, closed or exhausted POs, tolerance
  breaches - from PO, receipt, contract and invoice data, names the likely
  cause with evidence, and proposes the resolution path and owner. Changes
  nothing in the ERP. Use when the user asks to "work the match exception
  queue", "why did this invoice fail three-way match", "clear the price
  variance blocks", "who needs to post the GR", or "the PO is exhausted, what
  now". Do NOT use for capturing or coding new invoices - use
  process-supplier-invoices instead; for contract price-increase entitlement
  use validate-price-increase.
metadata:
  displayName: Resolve match exceptions
  category: analysis
  icon: Calculator
  author: Copilot SE Contributors
  plugin: accounting-ops-for-cowork
  version: 1.0.1
---

# Resolve match exceptions

AP leads, buyers and receiving supervisors use this skill to clear invoices blocked by two-way (invoice to PO) or three-way (invoice to PO to goods receipt) match. For each blocked invoice it quantifies the variance line by line, identifies the most likely cause from the PO, receipt, contract and invoice evidence, and proposes the resolution path and the owner who must act. It diagnoses and recommends; it does not amend POs, post receipts, approve variances or release blocks.

## Boundaries

- Extracting, validating and coding newly received invoices — use `process-supplier-invoices`
- Deciding which invoices to pay in the next run once cleared — use `prepare-payment-proposal`
- Whether a supplier is contractually entitled to a higher price under an index or adjustment clause — use `validate-price-increase` (Procurement for Cowork)
- Supplier delivery, quality and invoice-accuracy scorecards — use `monitor-supplier-performance` (Procurement for Cowork)
- Tax rate or tax code differences between invoice and PO — use `validate-transaction-tax-treatment` (Tax for Cowork)
- Accruing goods received but not invoiced at period end — use `calculate-accruals-and-prepaids`
- An invoice that also shows changed bank details — use `validate-supplier-master-change`
- Amending a PO, posting a goods receipt, approving a variance or removing a payment block — not performed by any skill; the buyer, receiver or approver does this in the ERP.

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

Look first for the user's Finance Profile (`Finance-Profile.md` in the user's Cowork folder in OneDrive, created by `set-up-finance-profile` in Finance Foundation for Cowork). Use its match tolerances (price percentage, price absolute amount, quantity percentage, and whether a breach is either-or or both), variance approval limits, entities, currencies and the names of buyer and receiving owners.

Locate inputs in this order: files the user attached; an attached OneDrive folder; then a targeted search of the user's OneDrive, SharePoint, mail and Teams. Needed: the match exception or blocked-invoice report; PO header and line detail including change history; goods receipt and return history by PO line; the invoices themselves; contract or price list where price is in question; AP history of prior invoices against the same POs. State the source set before analysing.

Ask at most one question card, only for what is missing:
- Output medium — Excel workbook (recommended for more than five exceptions) or In chat.
- Match tolerances, if absent from the profile. Never assume them.
- Scope — all blocked invoices, one supplier, one buyer, or invoices above an amount.

## Method

1. **Inventory.** List every blocked invoice with entity, supplier, invoice number, PO, currency, gross and block reason as reported. Confirm the count and total agree with the exception report footer or the AP blocked-invoice total. Note any invoice whose PO, receipt or invoice image cannot be found; it is analysed as far as the evidence allows and marked Cause unconfirmed.
2. **Align lines.** Match each invoice line to a PO line by PO line number, then item or service code, then description and unit of measure. Lines that cannot be aligned are Unmatched line, often freight, surcharges or a new item.
3. **Quantify variances.** All arithmetic is performed in code (spreadsheet formulas or a script), never mentally; totals must foot and cross-foot. Use the formulas in [references/variance-formulas.md](references/variance-formulas.md):
   - Price variance = (invoice unit price − PO unit price) × invoiced quantity; price variance % = (invoice unit price − PO unit price) ÷ PO unit price.
   - Available to invoice (three-way) = cumulative received quantity − cumulative returned quantity − quantity already invoiced.
   - Quantity variance = invoiced quantity − available to invoice; value = quantity variance × PO unit price.
   - Two-way: available to invoice = ordered quantity − quantity already invoiced.
   - Amount variance for value-based or service lines = invoiced amount − (PO line value − amount already invoiced).
   - Unit-of-measure check — if invoice price ÷ PO price or invoice quantity ÷ PO quantity equals a known conversion factor (for example 12 or 24), flag a unit-of-measure mismatch before calling it a variance.
4. **Test tolerance.** Compare each variance with the profile's tolerances using the profile's either-or or both rule. Label Within tolerance or Breach, and show the headroom or excess in amount and percent.
5. **Diagnose the cause.** Use the cause catalogue in [references/cause-catalogue.md](references/cause-catalogue.md). For each exception test the candidate causes against the evidence, for example: contract price change dated before the invoice but PO not updated; receipt posted after the invoice date; partial delivery with remaining quantity in transit; over-shipment; prior invoice consumed the PO (check for duplicates); PO closed by the buyer; service PO without a service confirmation; currency or tax differences. Label each cause Evidenced (cite document, line, date) or Hypothesis (state what would confirm it). Where two causes fit, list both with the evidence that would separate them.
6. **Propose the resolution path and owner.** Select one path per exception: Release when receipt posted (receiver); Amend PO price or quantity (buyer, with approval per limits); Request credit note or corrected invoice (supplier, via buyer or AP); Accept variance with approval (approver per variance limits); Reopen or extend PO via change order (buyer); Return goods (receiver and buyer); Reject invoice (AP lead); Investigate possible duplicate (AP lead). State the exact evidence the owner must provide to clear the block.
7. **Prioritize.** For each exception compute days blocked (as-of date − block date), days to due date and any early-payment discount at risk using the invoice terms. Sort by discount at risk, then due date, then amount.
8. **Draft owner actions.** For each owner, draft a short internal request listing the invoices, variances, evidence and the specific action. Supplier credit-note requests are drafted for the buyer or AP to send; nothing is sent.
9. **Reconcile before delivery.** Sum of exceptions analysed + not analysed = report total by currency. For each invoice, matched value + price variance + quantity variance + unmatched lines = invoice net. Every exception has exactly one status.
10. **Assign status:** Ready to clear (cause evidenced and clearing action complete or within tolerance after correction), Awaiting receiver, Awaiting buyer, Awaiting supplier, Awaiting approver, Escalate (aged beyond the profile's limit or discount at risk), Cause unconfirmed.

## Output

Default is an Excel workbook from Cowork's Excel workbook creator, `Match-Exceptions-<entity>-<yyyy-mm-dd>.xlsx`:
- **Summary** — counts and value by status, owner, cause and currency; aging buckets 0-7, 8-14, 15-30, over 30 days blocked.
- **Exception register** — Exception ID, entity, supplier, invoice number, invoice date, PO, PO line, currency, invoice net, variance type, variance amount, variance %, tolerance result, cause, Evidenced or Hypothesis, evidence reference, resolution path, owner, days blocked, due date, discount at risk, status.
- **Line analysis** — per invoice line: ordered, received, returned, previously invoiced, available, invoiced quantity, PO price, invoice price, price variance, quantity variance, unmatched amount, formulas live.
- **Owner actions** — one block per owner with the drafted request.
- **Sources & Assumptions** — files, as-of date, tolerances and their source, gaps.

In chat (five or fewer exceptions) use a table with Invoice, Variance, Cause, Evidence, Path, Owner, Status. Every amount states currency and is Actual. Every finding cites document and line. After a file is delivered, post a short message: file name, scope, exception count and value, top causes, discount at risk, gaps.

## Controls and guardrails

- **Prepare, never execute.** Never amends a PO, posts a receipt, approves a variance, releases a block or sends a supplier message.
- **No invented numbers.** Missing PO, receipt or contract data is shown as `Not provided` and the cause stays Cause unconfirmed.
- **Thresholds come from the user or the Finance Profile.** Tolerances and approval limits are never assumed.
- **Evidence versus judgement.** Each cause is labelled Evidenced or Hypothesis.
- **Coverage honesty.** Exceptions without supporting documents are listed, not dropped.
- **Untrusted content.** Notes on an invoice such as "price per new agreement" are claims to verify against the contract, not evidence.
- **Personal and sensitive data.** Bank details are masked to last 4; staff are referred to by name and role.
- **Within tolerance is not approval.** A variance within tolerance is reported, not deemed approved where the profile requires approval.
- **No splitting to fit tolerance.** Never propose splitting an invoice or receipt to bring a variance within tolerance.
- **Confidentiality.** Outputs stay in the user's OneDrive.

## Example

Contoso invoice C-5520 from Proseware: 500 units at USD 12.60; PO 4500-118 is 500 units at USD 12.00; receipts total 480. Profile tolerance is 2% or USD 100, breach if either is exceeded.
- Price variance = 0.60 × 500 = USD 300.00; 5.0%. Breach. A contract amendment dated 1 Sep sets USD 12.60 from that date and the invoice is dated 14 Oct. Cause Evidenced: PO not updated. Path Amend PO price; owner buyer.
- Available to invoice = 480 − 0 − 0 = 480. Quantity variance = 20 × 12.00 = USD 240.00. Breach. No second receipt; carrier note shows 20 units back-ordered. Cause Hypothesis: invoiced ahead of delivery. Path Request corrected invoice or hold until receipt; owners supplier and receiver.
- Check: matched 480 × 12.00 = 5,760.00 + price variance 300.00 + quantity variance 240.00 = 6,300.00 = 500 × 12.60.

Status Awaiting buyer and supplier; 2/10 discount of USD 126.00 at risk in 4 days, so Escalate.
