# Flux thresholds, driver categories and labels

## 1. Movement and threshold test

- Movement = Current balance - Comparative balance (trial balance sign convention, stated in Sources & Assumptions).
- Movement % = Movement / absolute value of Comparative, to 1 dp; `n/a` when the comparative is zero.
- Flag test, per the profile rule:
  - *Either* - flagged if absolute Movement >= absolute threshold, or absolute Movement % >= percentage threshold.
  - *Both* - flagged only if both are met. When Movement % is `n/a`, the absolute test alone decides.
- Balance sheet and income statement thresholds are applied separately when the profile gives separate values.
- Comparison bases and when to use them:

| Basis | Typical use |
|---|---|
| Current month vs prior month | Monthly close review of income statement and balance sheet |
| Current month vs same month prior year | Seasonal income statement accounts |
| Quarter vs prior quarter, or vs same quarter prior year | Quarterly review |
| Period end vs prior year end | Balance sheet for annual or interim reporting |
| Actual vs analytical expectation | Accounts with a predictable relationship (depreciation, interest, payroll, rent, amortization) |

## 2. Driver categories

| Category | How to quantify from ledger detail |
|---|---|
| Specific transaction | Sum of journal lines for the identified document (invoice, contract, settlement) |
| Accrual reversal and true-up | Current-period actual for the item - prior-period accrual reversed |
| New accrual or provision | Amount booked this period with no comparable prior-period entry |
| Reclassification | Amount moved in or out by reclass journal; both accounts noted |
| Recurring change | Change in a recurring entry's amount (new rate, new contract, contract ended) |
| Volume or rate | (Current volume - prior volume) x prior rate, and (current rate - prior rate) x current volume, only with supplied operational data |
| FX translation | Current foreign-currency balance x (current rate - comparative rate), rates from the user or `translate-currency` |
| Subledger activity | Net subledger postings by source (AP, AR, payroll, inventory, fixed assets) compared with the prior period |
| Correction or error candidate | Misposting identified; amount and suggested correction listed for `prepare-journal-entries` |
| Seasonality | Only when quantified from the same period in prior years |

## 3. Driver evidence labels

| Label | Counts toward explained amount | Condition |
|---|---|---|
| Documented | Yes | Traced to journal lines and a source document (invoice, contract, calculation) |
| Ledger-evident | Yes | Traced to specific journal lines; business reason not yet documented |
| Owner-stated | Yes | A quantified amount given by the account owner in mail or Teams, cited by sender and date |
| Hypothesis | No | Plausible but not quantified from evidence |

## 4. Account labels (first match in this order)

| Label | Condition |
|---|---|
| Below threshold - not required | Movement not flagged |
| Not analysed - data missing | Flagged, but ledger detail unavailable |
| Explained | Residual (Movement - counted drivers) would not be flagged under the same threshold rule against the same comparative |
| Partially explained | At least one counted driver, but the residual would still be flagged |
| Unexplained | No counted driver |

## 5. Explanation writing standard

Each explanation states: amount and direction, the drivers with amounts and sources, the evidence label of each, the residual, and any follow-up. Avoid unquantified words such as "timing", "higher activity" or "various" unless followed by the amount and the journals behind it.

Example of an acceptable explanation: "Up 86,500 (47.5%). Proseware legal invoice INV-2209 60,000 (Documented); August accrual true-up 14,000 (Ledger-evident, JE-0911). Residual 12,500 below threshold."
