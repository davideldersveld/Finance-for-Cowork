# Referral package index and readiness checklist

## Evidence index (one row per claimed invoice)

| Column | Content |
|---|---|
| Invoice | Number |
| Invoice date | Date |
| Open amount | Transaction currency |
| Dispute status | None / Open / Closed — valid / Closed — invalid |
| Invoice copy | Found / Not found / Not accessible, with file name |
| Customer PO or order | Status and document reference |
| Terms evidence | Signed contract clause, accepted order acknowledgment, or Not provided |
| Delivery note | Status and reference |
| Signed POD or service acceptance | Status, signatory role and date |
| Change orders | Status and reference, or Not applicable |
| Reminders and notices covering this invoice | Dates |
| In claim | Yes / No (with reason) |

An invoice with no POD or acceptance evidence stays in the claim only if the user decides so; it is marked as a gap in the cover memo.

## Contract terms extract (quote verbatim with clause numbers)

- Payment terms and due-date basis.
- Late-payment interest (rate, simple or compound, day-count basis, start date).
- Recovery costs or collection fees.
- Retention of title.
- Set-off and withholding rights.
- Dispute notification window.
- Governing law and jurisdiction or arbitration.
- Guarantees, security or credit insurance conditions (including notification deadlines to the insurer).
- Notice clause (addresses and methods for formal notices).

## Claim calculation layout

| Invoice | Open amount | Due date | Calculation date | Days overdue | Annual rate | Day-count basis | Interest | Source clause |
|---|---|---|---|---|---|---|---|---|

- `Days overdue = Calculation date - Due date` (calendar days).
- `Interest = Open amount x Annual rate x Days overdue / Day-count basis` unless the clause specifies another method; reproduce that method exactly.
- Totals: principal, contractual interest, `For counsel` items (statutory interest, recovery costs), less unapplied credits and cash, equals claim total.

## Readiness checklist

| Prerequisite | Status | Evidence |
|---|---|---|
| Undisputed principal at or above referral threshold | Met / Not met / Not provided | Claim calculation |
| Final notice sent and period expired | | Notice copy and delivery evidence |
| No open promise or payment plan in good standing | | Promise log |
| Disputes carved out or resolved | | Dispute log |
| Evidence complete for every claimed invoice | | Evidence index |
| No insolvency or moratorium indicator | | Searches performed and dates |
| Debtor is a business (not an individual) or compliance review completed | | Customer master |
| Approval obtained or approver named | | Authority matrix |
| Account manager informed (strategic accounts) | | Email or Teams reference |

## Questions for counsel (list, never answer)

- Limitation period applicable to each invoice and the earliest invoice date.
- Entitlement to statutory interest or compensation in the governing jurisdiction.
- Forum and service requirements under the contract.
- Effect of any open dispute, set-off claim or retention of title on the claim.
- Steps required for any guarantee or credit insurance claim.
