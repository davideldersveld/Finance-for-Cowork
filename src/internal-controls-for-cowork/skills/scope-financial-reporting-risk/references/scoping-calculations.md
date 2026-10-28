# Scoping calculations, factors and defaults

All formulas run in the workbook or a script; never compute mentally. Every input cell cites its source.

## 1. Materiality sheet

| Row | Formula | Source |
|---|---|---|
| Benchmark amount | Input | User or Finance Profile |
| Benchmark % | Input | User or Finance Profile |
| Overall materiality | `= Benchmark amount x Benchmark %` (or stated amount) | Calculated |
| Scoping threshold % | Input, if expressed as a % of materiality | User |
| Scoping threshold | `= Overall materiality x Scoping threshold %` (or stated amount) | Calculated |

If the user gives an amount without its basis, record the amount and show the basis as `Not provided`.

## 2. Account scoping columns and tests

- `Balance test = IF(ABS(Closing balance) >= Scoping threshold, "Meets", "Below")`
- `Activity test = IF(MAX(Total debits, Total credits) >= Scoping threshold, "Meets", "Below")` — only when the methodology uses activity.
- `Quantitative result = "Quantitatively significant"` when either applicable test meets.
- Final status combines the quantitative result with the qualitative factors below.

## 3. Qualitative risk factors (AS 2201.29)

Record Present / Not present / Not assessed with a source for each:

1. Size and composition of the account.
2. Susceptibility to misstatement due to errors or fraud.
3. Volume of activity, complexity and homogeneity of the individual transactions.
4. Nature of the account or disclosure.
5. Accounting and reporting complexities.
6. Exposure to losses in the account.
7. Possibility of significant contingent liabilities arising from the activities reflected.
8. Existence of related party transactions.
9. Changes from the prior period in account or disclosure characteristics.

Also consider items the user's risk assessment highlights: significant estimates, new systems, restructurings, acquisitions and prior-year deficiencies. Retrieve authoritative AS 2201 text when exact wording is needed.

## 4. Starter assertion map (adjust per account; user confirms)

| Caption type | Usually relevant | Often relevant |
|---|---|---|
| Revenue | E/O, C, cutoff | V/A (variable consideration), P&D |
| Accounts receivable | E/O, V/A | R&O |
| Inventory | E/O, V/A, C | R&O |
| Property, plant and equipment | E/O, V/A | C, R&O |
| Goodwill and intangibles | V/A | P&D |
| Accounts payable and accruals | C, V/A | cutoff |
| Debt | C, V/A, P&D | R&O |
| Income taxes | V/A, C, P&D | |
| Equity | C, P&D | E/O |
| Cash | E/O, C | R&O |

Codes: E/O existence or occurrence; C completeness; V/A valuation or allocation; R&O rights and obligations; P&D presentation and disclosure.

## 5. Entity scoping procedure

1. For each benchmark the user names, compute `Share = ABS(Entity measure) / ABS(Consolidated measure before eliminations)`. For pretax income with loss-making entities, use the absolute-value total `SUM(ABS(entity pretax income))` as the denominator when the user's methodology says so; state the convention on the About sheet.
2. Rank entities by share for the primary benchmark.
3. Full scope: share at or above the individual threshold on any benchmark the user designates.
4. Specific scope: the entity holds a balance of a significant caption at or above the scoping threshold, or has a specific risk (new acquisition, prior-year deficiency, fraud risk, significant estimate).
5. Aggregate check: `Out-of-scope share = 1 - SUM(shares of Full and Specific scope entities)`. If above the aggregate limit, add the next largest remaining entity and recompute; record each iteration.
6. Remaining entities: Entity-level coverage only; list the entity-level controls relied on.

## 6. Sample size default (user-confirmable; not a standard)

The table below is a commonly used, frequency-based starting point. It is shown only as an option for the user to confirm or replace with the methodology table. Until confirmed, sample size is `Not provided`.

| Control frequency | Typical occurrences per year | Lower risk of failure | Higher risk of failure |
|---|---|---|---|
| Annual | 1 | 1 | 1 |
| Quarterly | 4 | 2 | 2 |
| Monthly | 12 | 2 | 3 |
| Weekly | 52 | 5 | 10 |
| Daily | about 250 | 20 | 30 |
| Multiple times per day | more than 250 | 25 | 40 |
| Automated | n/a | 1 per configuration, with effective ITGCs | 1 per configuration, with effective ITGCs |

Event-driven controls use the band whose occurrences per year are closest to the expected population. If the population is smaller than the size, test all items.

## 7. Testing plan columns

Control ID; Caption(s); Assertions; Entity; Process; Nature; Frequency; Risk of failure (Lower / Higher, with factors); Test of design approach; Operating effectiveness approach (inquiry, observation, inspection, reperformance); Interim period; Roll-forward period; Sample size (lookup); Sample size source (Methodology table / Default table — confirmed by user / Not provided); Tester; Planned start; Planned completion; External auditor reliance (Yes / No / Unknown); Source RCM row.
