# Hedge designation memo template

Each memo covers one relationship. Use the framework's own terms (see the terminology map in effectiveness-and-terminology.md). Mark the document "Draft — for review by the hedge accounting owner and auditor".

## Headings

1. **Relationship identification** — relationship ID, entity, framework (ASC 815 or IFRS 9), hedge type, designation date, documentation date (as evidenced), preparer and reviewer roles.
2. **Risk management objective and strategy** — the strategy-level objective from the risk policy (section cited) and the specific objective for this relationship. Under IFRS 9 these are distinct concepts; changes to the relationship-level objective drive discontinuation.
3. **Hedged risk** — for example, the risk of changes in USD cash flows from forecast EUR-denominated sales due to EUR/USD spot rate movements; or changes in fair value of fixed-rate debt attributable to the benchmark interest rate.
4. **Hedged item** — for a recognized item, the asset or liability with reference; for a forecast transaction, nature, expected timing (a period narrow enough to identify the transaction when it occurs), currency and amount, and the evidence supporting probability (ASC 815 probable; IFRS 9 highly probable): history of similar transactions, forecast and budget approval, ability to carry out the transaction.
5. **Hedging instrument** — trade IDs, counterparty, trade date, maturity, notional, rate, direction, and the designated proportion if less than 100 percent.
6. **Excluded components / costs of hedging** — for example forward points, option time value, cross-currency basis; ASC 815 recognition approach elected (amortization or fair value through earnings) or IFRS 9 costs-of-hedging treatment.
7. **Hedge ratio** — quantity of instrument to quantity of hedged item and how it reflects risk management practice.
8. **Effectiveness assessment method** — prospective (and, under ASC 815, retrospective) method; quantitative technique (dollar offset cumulative, regression, hypothetical derivative) or qualitative (critical terms match, shortcut where eligible under ASC 815); frequency (at least at each reporting date and on significant change); range or criteria from the policy.
9. **Sources of ineffectiveness** — for example timing differences between forecast and settlement, counterparty or own credit risk, basis differences between the instrument's index and the hedged item's, notional mismatch.
10. **Accounting for the relationship** — where gains and losses go and when they are reclassified or used for basis adjustment; income statement line for presentation.
11. **Discontinuation and rebalancing** — triggers and how amounts already deferred will be treated.
12. **Attachments** — confirmation, policy extract, forecast extract, prior test.

## Completeness check

| Element | Required under ASC 815 | Required under IFRS 9 |
|---|---|---|
| Risk management objective and strategy | Yes | Yes |
| Hedging instrument identified | Yes | Yes |
| Hedged item or transaction identified | Yes | Yes |
| Nature of risk hedged | Yes | Yes |
| Method of assessing effectiveness | Yes, prospective and retrospective | Yes, prospective |
| Hedge ratio determination | Implicit in designated amounts | Yes, explicitly |
| Analysis of sources of ineffectiveness | Not a separate requirement | Yes |
| Excluded components and their recognition | Yes, if any | Costs of hedging election where applied |
| Forecast transaction timing and amount | Yes | Yes |

Status `Documentation incomplete` lists every missing element by heading number.

## Inventory reconciliation statuses

| Status | Rule |
|---|---|
| Agrees | All key fields match and fair value difference within tolerance |
| Difference | Any key field differs, or fair value difference above tolerance |
| Missing confirmation | Inventory trade with no bank confirmation located |
| Not in inventory | Bank confirmation with no inventory trade |
| Matured / Terminated | Listed separately with settlement evidence |
