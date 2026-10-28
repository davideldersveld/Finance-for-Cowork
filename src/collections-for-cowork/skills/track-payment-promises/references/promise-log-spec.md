# Promise-to-pay log specification

## Columns (Promise log sheet)

| Column | Content |
|---|---|
| Promise ID | Stable ID, for example `PTP-2026-00451`. Never reused. |
| Plan ID | Payment plan reference if the promise is an installment; blank otherwise. |
| Supersedes ID | ID of the promise this one replaces, if renegotiated. |
| Customer ID | From the customer master. |
| Customer name | Legal name. |
| Entity | Selling entity owed the money. |
| Currency | Transaction currency of the promised amount. |
| Invoices covered | Invoice numbers, or "Unspecified". |
| Promised amount | Amount as stated by the customer. |
| Promised date | Date the customer said funds would be sent or received; record which ("send" or "value") if stated. |
| Payment method | Wire, ACH, check, card, portal, or Not stated. |
| Channel | Call, email, Teams, portal, meeting. |
| Made by | Customer contact name and role. |
| Taken by | Collector name. |
| Date recorded | Date the promise was made. |
| Source | Call note reference, email subject + sender + date, or Teams message date. |
| Grace days | Value applied (from profile). |
| Due-plus-grace date | Promised date + grace days (calendar days unless the profile says business days). |
| Received | Sum of matched receipts within the window. |
| Receipt references | Bank line or cash-application IDs. |
| Shortfall | Promised amount - Received, floor zero. |
| Status | One of the statuses below. |
| Status date | Date the current status was set. |
| Next action | Follow up broken promise, confirm remittance, escalate, none. |
| Notes | Context, labelled as collector context. |

## Statuses

| Status | Rule |
|---|---|
| `Open` | Today is on or before due-plus-grace date; Received below kept threshold. |
| `Open — receipts not yet reflected` | Due-plus-grace date passed but receipts are not available through that date. |
| `Kept` | Received at or above `Promised amount x (1 - tolerance)` by due-plus-grace date. |
| `Kept late` | Kept threshold reached only after due-plus-grace date. |
| `Partially kept` | After due-plus-grace date, Received greater than zero but below kept threshold. |
| `Broken` | After due-plus-grace date, Received equals zero. |
| `Superseded` | Replaced by a renegotiated promise before due-plus-grace date. |
| `Cancelled` | Underlying invoices credited or dispute resolved for the customer; reason recorded. |
| `Not a promise — no date or amount` | Statement of intent without a date or amount; follow-up needed to obtain one. |

## Receipt allocation rules

1. Use receipts from the customer and its known payer accounts only.
2. If the promise names invoices, allocate receipts applied to those invoices first.
3. Remaining unallocated customer receipts are allocated to promises in order of promised date, oldest first.
4. A receipt amount is allocated once; split a receipt across promises only when the remittance shows it covers several.
5. Receipts dated before the promise was recorded do not count toward it.

## Kept-rate formulas

- `Resolved promises = Kept + Kept late + Partially kept + Broken`.
- `Kept rate (count) = Kept / Resolved promises`.
- `Kept rate (amount) = Received by due-plus-grace on resolved promises / Promised amount on resolved promises`.
- Report by collector, segment, customer and period; show the count behind every rate.
