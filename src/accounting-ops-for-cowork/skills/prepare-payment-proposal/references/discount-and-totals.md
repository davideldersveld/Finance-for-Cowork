# Discount mathematics, hold reasons and workbook columns

## Discount formulas

Notation: d = discount rate (2% = 0.02); D = discount days; N = net days; V = payment value date.

| Measure | Formula |
|---|---|
| Discount date | baseline date + D |
| Net due date | baseline date + N |
| Eligible | discount date ≥ V |
| Discount amount | discount base × d (base as stated in the terms, gross or excluding tax) |
| Amount paid | discount base × (1 − d) + any amount outside the base |
| Days accelerated | net due date − V (use N − D when paying exactly on the discount date) |
| Annualized return, simple | d ÷ (1 − d) × 365 ÷ days accelerated |
| Effective annual return, compound | (1 + d ÷ (1 − d)) ^ (365 ÷ days accelerated) − 1 |
| Take discount | simple annualized return > hurdle rate from profile |

Reference values (paid exactly on the discount date):

| Terms | Simple | Compound |
|---|---|---|
| 1/10 net 30 | 18.4% | 20.1% |
| 2/10 net 30 | 37.2% | 44.6% |
| 2/10 net 45 | 21.3% | 23.5% |
| 1/15 net 45 | 12.3% | 13.0% |

Recompute these in code for every item; the table is a sanity check only. The simple formula divides by (1 − d) because the buyer gives up only the discounted amount for the acceleration period.

## Hold reasons (codes)

| Code | Reason | Evidence |
|---|---|---|
| H1 | Disputed | Dispute list entry or open dispute email |
| H2 | ERP payment block | Block code on the item |
| H3 | Open match exception | Exception report or resolve-match-exceptions output |
| H4 | Bank details new or changed, not Verified | Change date within lookback window and master change outcome other than Verified |
| H5 | Supplier blocked or inactive | Vendor master status |
| H6 | Possible duplicate | Matching rule and the matched item |
| H7 | Missing approval | No approval record per limits |
| H8 | Net credit | Supplier net ≤ 0 after credit notes |
| H9 | Data missing | Terms, due date or bank account not provided |
| H10 | One-time or new supplier | Created within lookback window |

## Workbook columns

- Proposal — Entity | Paying bank account (last 4) | Payment method | Supplier ID | Supplier | Invoice number | Invoice date | Baseline date | Terms | Net due date | Days past due | Currency | Gross | Credit notes applied | Discount taken | Amount to pay | Status | Source reference
- Discounts — Supplier | Invoice | Terms | Discount date | Net due date | Value date | Days accelerated | Discount base | Discount amount | Simple annualized return | Compound return | Hurdle rate | Decision | Discount at risk
- Holds — Supplier | Invoice | Currency | Amount | Hold codes | Evidence | Owner | Action to clear
- Deferred — Supplier | Invoice | Currency | Amount | Net due date | Planned run
- Totals — Currency × Entity × Paying bank: count of payments, count of invoices, amount; high-value payments; top 10 payees
- Treasury handoff — Funding by bank account and value date; changed-bank payees with outcome; high-value list; new destination countries; preparer
- Sources & Assumptions — files, as-of date, control total agreement, profile values used, gaps

Reconciliation by currency: Proposed + Held + Deferred + Not eligible = open balance; difference must be zero.
