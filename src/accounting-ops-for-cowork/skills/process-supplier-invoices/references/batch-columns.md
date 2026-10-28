# Batch workbook columns and status definitions

## Batch sheet (one row per invoice)

Batch ID | Source file | Page(s) | Document type | Supplier name (as read) | Vendor ID | Vendor master match (Tax number / Name / None) | Supplier tax number (last 4) | Bill-to entity | Invoice number | Invoice date | Service period from | Service period to | PO number | Currency | Net | Tax | Gross | Gross in functional currency (rate and source stated, or Not provided) | Terms (as stated) | Due date (as stated) | Bank account last 4 on invoice | Bank last 4 in master | Bank match (Yes / No / Not shown) | Arithmetic result | Duplicate risk | Approver required | Status | Exception count | Notes

## Lines sheet (one row per invoice line)

Batch ID | Invoice number | Line no. | Description | Quantity | Unit of measure | Unit price | Line net (as read) | Line net (recomputed) | Difference | Tax rate | Tax (recomputed) | PO line | Proposed GL account | Proposed cost centre | Coding basis (History-matched / Policy-based / Suggested - approver to confirm) | Supporting invoices (count) | Flags (Possible capital item / Possible prepaid or accrual)

## Exceptions sheet

Exception ID | Batch ID | Invoice number | Supplier | Test | Finding | Evidence (file, page, field) | Amount affected | Currency | Owner (AP processor / AP lead / Buyer / Requester / Tax) | Next step | Evidence or Judgement

## Duplicate check sheet

Batch ID | Invoice number | Matched record (source, invoice number, date, gross, status) | Test (D1-D8) | Risk | Comment

## Status definitions

| Status | Applies when |
|---|---|
| Ready for entry | Non-PO invoice within policy, arithmetic agrees, supplier matched, coding History-matched or Policy-based, no duplicate risk above Low |
| Ready for match | PO invoice, PO valid and open, arithmetic agrees, supplier matched; match itself performed in the ERP |
| Ready - coding to confirm | As Ready for entry, but coding is Suggested - approver to confirm |
| Exception - [type] | Arithmetic error, tax, PO required, PO invalid, new supplier, entity, duplicate review |
| Hold - possible duplicate | Any High duplicate test |
| Hold - bank detail mismatch | Bank last 4 on invoice differs from master or master has none |
| Unreadable | A required field cannot be read |
| Excluded | Statement, reminder, quote, pro forma or non-finance document |

Precedence when several apply: Hold - bank detail mismatch, Hold - possible duplicate, Unreadable, Exception, Ready.
