# Procedures by account type

## Bank and cash accounts
- Support - bank statement closing balance at the as-of date (statement or bank portal export with its generation date).
- Match ledger cash entries to statement lines on amount, the date window stated by the user or profile (if none is stated, match on amount and reference and show the date gap for each pair) and reference (check number, payment ID).
- Typical items - deposits in transit (GL, not bank), outstanding payments (GL, not bank), bank-only items (fees, interest, returned items, direct debits), errors on either side.
- Stale-dated outstanding checks are flagged against the user's escheatment or write-back policy; the skill does not decide escheatment.
- Foreign-currency accounts - reconcile in the account currency first; then explain any functional-currency difference as revaluation, using rates the user or `translate-currency` supplies.

## Subledger control accounts (AP, AR, fixed assets, inventory, payroll liabilities)
- Support - subledger report (aged trial balance, register) at the same cutoff, with its run timestamp.
- Compare GL control balance with subledger total; then list manual journals posted directly to the control account in the period (these are the most common cause of breaks), interface batches posted in one ledger but not the other, and cutoff differences.
- A subledger report run after period end is rolled back by removing post-period transactions, listed individually.
- Fixed asset subledger breaks are reported here as items; the full roll-forward belongs to `roll-forward-fixed-assets`.

## Clearing, suspense and transit accounts
- Expected balance zero at period end unless the policy states a standing balance.
- Support - the open-item list for the account, built from GL detail by pairing debits and credits on reference and amount.
- Every unpaired line is a reconciling item with origination date, poster, source and description.
- Any open item is flagged once older than the clearing policy limit; unknown items are `Unidentified`.

## Accrued liabilities
- Support - the accrual schedule by line (from `calculate-accruals-and-prepaids` or the user's schedule).
- Compare schedule total with GL; list lines in the schedule not booked, entries booked without schedule support, and prior-period accruals that did not reverse.
- Aged accruals (lines older than the policy limit without invoice) are flagged.

## Prepaid expenses
- Support - the prepaid register with remaining balance per item.
- Compare register closing balance with GL; list items with amortization not posted, items posted to the prepaid account without register entries, and fully amortized items still carrying a balance.

## Other balance sheet accounts (deposits, employee advances, other receivables and payables)
- Support - a schedule of each open balance with counterparty, origination date, and evidence (agreement, receipt, confirmation).
- Each schedule line is aged; balances without evidence are reported as `Unidentified` until supported.
