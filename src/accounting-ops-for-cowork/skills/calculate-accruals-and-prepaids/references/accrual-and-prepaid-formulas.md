# Accrual and prepaid formulas

All formulas are applied per line in code, in the transaction currency, then translated at the rate the user or `translate-currency` supplies. Rounding is to the currency's minor unit at line level.

## 1. Accrual categories

| Category | Formula | Required inputs | Evidence to cite |
|---|---|---|---|
| GRNI | (Qty received to period end - Qty invoiced) x PO unit price | PO line, receipt date and quantity, invoiced quantity | Receipts report row, PO number and line |
| GRNI - price changed | (Qty received - Qty invoiced) x latest agreed price, if a price change is evidenced | Amended PO or supplier price confirmation | Amendment reference |
| Services - time-based | Monthly fee x unbilled service months in the period (partial months by days in service / days in month) | Contract fee, service dates, last invoiced period | Contract clause, last invoice |
| Services - milestone or completion | Contract value x evidenced completion % - invoiced to date | Completion evidence (status report, acceptance, timesheets) | Document and date |
| Services - hourly | Hours worked unbilled x contracted rate | Timesheets or supplier hours report | Report and date range |
| Utilities - run-rate | Average daily cost x unbilled days; average daily cost = sum of recent bills / days covered by those bills | At least one full billing cycle | Bills used, days covered |
| Utilities - metered | (Closing reading - last billed reading) x tariff + standing charges for unbilled days | Readings, tariff | Reading date, tariff source |
| Bonus and incentive | Eligible cost base x approved payout % x elapsed fraction of the plan year - accrued to date | Plan document, payout % approved, cost base by cost centre | HR or compensation approval |
| Fixed recurring | Contractual amount for unbilled portion | Contract | Clause |

Rules:
- Receipt date, not PO date, determines the period for GRNI.
- Invoices dated on or before period end but not yet entered are listed in a separate "Unentered invoices" block (AP cutoff), not in GRNI.
- Elapsed fraction of the plan year = days elapsed in the plan year to period end / days in the plan year, unless the plan states otherwise.
- Negative GRNI (quantity invoiced exceeds quantity received) is not netted; it is listed as an exception for `resolve-match-exceptions`.

## 2. True-up of prior-period accruals

- True-up = Actual invoice amount for the accrued period - Amount accrued.
- Positive true-up = under-accrual (additional expense in current period); negative = over-accrual.
- Lines still not invoiced after two period ends are listed as aged accruals for the reviewer, with original date and amount.
- Accrual accuracy % = 1 - (sum of absolute true-ups / sum of amounts accrued) for lines invoiced, shown to 1 dp.

## 3. Prepaid amortization

- Daily straight-line - amortization for a period = Total cost x service days in the period / total service days.
- Monthly straight-line - amortization per full month = Total cost / number of service months; the first and last month follow the profile's mid-month rule (for example, service starting on or before the 15th counts as a full month, after the 15th starts next month). If the profile is silent, ask.
- Final period amortization = Total cost - cumulative amortization to the prior period, so the schedule ends at exactly zero.
- Items below the prepaid capitalization threshold are expensed when incurred and listed as `Below threshold - expensed`.
- A prepaid whose service has been cancelled or ended early is flagged for write-off review, not amortized on schedule.

## 4. Prepaid register roll-forward

Opening balance + Additions - Amortization - Write-offs = Closing balance, per item and in total. Closing total is compared with the prepaid ledger account; any difference is reported for `reconcile-balance-sheet-accounts`.

## 5. Proposed entry conventions

| Item | Debit | Credit |
|---|---|---|
| Accrual | Expense (or inventory or asset account, per policy) | Accrued liabilities or GRNI clearing |
| Prepaid addition | Prepaid expenses | AP or cash (normally already posted through AP) |
| Prepaid amortization | Expense | Prepaid expenses |
| Reversal of accrual | Accrued liabilities | Expense, dated first day of next period |

Account numbers come from the user's chart of accounts; the table shows account roles only.
