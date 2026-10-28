# Inventory fields, fee analysis and change-request template

## Account inventory fields

| Field | Notes |
|---|---|
| Account ID | Internal key |
| Bank and branch | Legal bank name; bank group (ultimate parent) |
| Country | Account domicile |
| Entity | Legal entity owning the account |
| Currency | ISO code |
| Account number | Last four digits only |
| Account type | Operating, collections, disbursement, payroll, zero-balance sub-account, pool header, escrow, collateral, investment, merchant, petty cash |
| Purpose | Documented business purpose and owner |
| Pool membership | Pool name and role (header or participant) |
| Opened date / closed date | From bank letters |
| Restriction | Restricted or not; reason (links to cash classification) |
| Statement delivery | Format and channel (MT940, camt.053, BAI2, portal) |
| GL account | Ledger account mapped |
| Mandate reference | Board resolution or mandate letter and date |
| KYC refresh date | Next due date if known |
| Status | Active / Dormant / Closure candidate / Pending closure / Closed |
| Source reconciliation | In all sources / Not in inventory / Not in bank data / Not in ledger |

## Signatory labels

| Label | Rule |
|---|---|
| Current | Employed, role consistent with matrix, bank-confirmed |
| Leaver — remove | HR shows a leaving date on or before the as-of date |
| Role changed — review | HR shows a role change since the mandate date |
| Exceeds authority matrix | Bank limit or authority type exceeds the internal matrix |
| Sole authority | One person can both initiate and approve, or sign alone where the matrix requires joint |
| Unverified | Mandate appears only in internal records |

## Fee analysis

- Use the account analysis statement's service codes (AFP codes in the US; ISO camt.086 Bank Services Billing where provided) to map services.
- `Expected charge = Volume × Agreed unit price` (or tiered price for the volume band).
- `Variance = Billed charge − Expected charge`; status `Overbilled` if variance > tolerance, `Underbilled` if variance < −tolerance, otherwise `Agrees`.
- `Unpriced service` when no agreed price exists; list for negotiation review.
- Earnings credit (where offered): `Earnings credit = Average collected balance × (1 − Reserve requirement, if stated) × Earnings credit rate × Days in period ÷ Day basis` — use the statement's stated formula; reconcile to the statement's credit.
- Net fees = Total charges − Earnings credit (not below zero unless the bank pays excess credit).
- Trend: compare volumes and charges with the prior three periods where data exists.

## Wallet share

| Product line | Revenue measure (as supplied) |
|---|---|
| Cash management | Fees net of earnings credit |
| Credit | Interest margin, commitment and utilization fees, upfront fees amortized for the period |
| FX and derivatives | Spread or revenue estimate supplied by the user or bank |
| Capital markets and advisory | Fees on transactions in the period |
| Trade finance | Letter of credit and guarantee fees |
| Investments and deposits | Fund or deposit revenue where supplied |

`Wallet share = Bank revenue ÷ Total revenue across banks`; `Credit commitment share = Bank's commitments ÷ Total committed facilities`; `Give-get gap = Wallet share − Credit commitment share` (percentage points). Present without recommending reallocations.

## Change-request template

| Field | Content |
|---|---|
| Request ID | CR-<date>-<sequence> |
| Request type | Remove signatory / Amend limit / Add joint authority / Close account / Update purpose / Remove banking user |
| Bank, entity, account (last 4) | |
| Person (if applicable) | Name and role |
| Reason | Label and evidence (HR record, dormancy data, matrix clause) |
| Effective date requested | |
| Internal approvals required | Per the authority matrix and bank policy (for example two authorized officers, board resolution) |
| Bank documents likely required | Mandate amendment form, closure letter, resolution extract — as listed by the bank, if known |
| Status | Draft — for review |
