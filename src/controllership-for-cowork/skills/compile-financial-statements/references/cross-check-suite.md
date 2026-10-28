# Cross-check suite

Run every check for every period presented (current and comparative) and, for C1 and C2, for every entity as well as the consolidated total. Checks are executed twice: as live formulas on the Checks sheet, and by an independent script that recomputes each value from the trial balance, mapping and supporting schedules rather than reading the statement cells. Both must agree.

## Sign convention

Trial balance net = debit - credit, so assets and expenses are positive and liabilities, equity and income are negative. The face statements present natural signs. The script works in trial balance signs and converts only for display.

## Tolerance

- Structural checks (C1, C2, C4, C5, C7, C8, C9) compute on unrounded values; tolerance is zero (allow 0.005 of the currency unit for floating-point noise).
- On the presented, rounded statements, a difference no larger than the presentation rounding unit (for example 1 in USD thousands) is `Pass - rounding only` when the unrounded check passes.
- Any other difference is `Fail`. A failing check is traced to cause; no balancing figure is inserted.

## Check definitions

| ID | Check | Value A | Value B |
|---|---|---|---|
| C1 | Balance sheet balances | Total assets | Total liabilities + total equity (including non-controlling interests) |
| C2 | Statements equal the trial balance | Sum of mapped lines by account class | Trial balance total by account class; trial balance nets to zero |
| C3 | Net income agrees across statements | Income statement net income | (a) comprehensive income starting line, (b) retained earnings column in the equity statement plus the NCI share, (c) cash flow starting point bridged to net income |
| C4 | Equity rolls forward | Opening + movements per component | Closing per component; closing equals balance sheet; opening equals prior closing balance sheet |
| C5 | Cash ties | Opening cash + net cash from operating, investing, financing + FX effect | Closing balance sheet cash and cash equivalents (plus restricted cash and restricted cash equivalents under US GAAP); opening equals prior balance sheet |
| C6 | Other comprehensive income ties | OCI for the period by component (after reclassifications and tax) | Movement in accumulated OCI by component on the balance sheet and equity statement |
| C7 | Cash flow proof | Sum of allocated movements per balance sheet line | Balance sheet movement per line; residual = 0 for every line |
| C8 | Eliminations and consolidation | Sum of each elimination entry | Zero; and consolidated line = sum of entity lines + eliminations |
| C9 | Attribution | Net income to parent + net income to NCI | Total net income (and the same for total comprehensive income) |
| C10 | Footing and comparatives | Sum of each column and row | Reported subtotal and totals; comparative column equals prior issued statements unless labelled Restated or Reclassified with reference |

## Script skeleton

Use this shape for the independent script. Inputs are the standardized trial balance (entity, account, period, net), the mapping (account, statement, line, class, cash flow category), and the supporting schedules.

```python
import pandas as pd

TOL = 0.005

def result(a, b, rounding_unit=None):
    diff = round(a - b, 6)
    if abs(diff) <= TOL:
        return diff, "Pass"
    if rounding_unit and abs(diff) <= rounding_unit:
        return diff, "Pass - rounding only"
    return diff, "Fail"

def c1_balance(tb, mapping, period, entity=None):
    df = tb.merge(mapping, on="account", how="left")
    df = df[df.period == period]
    if entity:
        df = df[df.entity == entity]
    unmapped = df[df["class"].isna()]
    assets = df.loc[df["class"] == "Asset", "net"].sum()
    liab_eq = -df.loc[df["class"].isin(["Liability", "Equity"]), "net"].sum()
    # Current-period profit not yet closed to retained earnings belongs in equity
    profit = -df.loc[df["class"].isin(["Income", "Expense"]), "net"].sum()
    return result(assets, liab_eq + profit), unmapped

def c5_cash(opening_cash, cfo, cfi, cff, fx, closing_cash_bs):
    return result(opening_cash + cfo + cfi + cff + fx, closing_cash_bs)

def c7_proof(workings):
    # workings: one row per balance sheet line with movement and allocation columns
    alloc_cols = [c for c in workings.columns if c.startswith("alloc_")]
    workings["residual"] = workings["movement"] - workings[alloc_cols].sum(axis=1)
    return workings[workings["residual"].abs() > TOL]
```

Extend with C2 to C4, C6 and C8 to C10 in the same pattern. Write each result to the Checks sheet with Value A, its source (sheet and range, or schedule and row), Value B, its source, Difference, Tolerance and Result.

## Common failure causes

| Check | Typical cause | Where to look |
|---|---|---|
| C1 | Unmapped or double-mapped account; trial balance not netting to zero; current-year profit not carried into equity | Mapping sheet, TB_Input footer |
| C3 | NCI share omitted in one statement; IFRS starting subtotal not bridged | Equity statement columns, cash flow top section |
| C4 | Dividends declared but not paid recorded only in liabilities; share-based payment credit missing; treasury share purchase omitted | Equity records, payroll share-based payment schedule |
| C5 | FX effect on cash not presented; restricted cash excluded; overdraft classification inconsistent with the cash definition | Translation workings, cash definition in policy |
| C6 | Reclassification adjustments or the tax effect on OCI omitted | OCI workings, tax provision support |
| C7 | Non-cash additions (accrued capex, right-of-use assets, acquisitions) shown as cash; disposal proceeds versus gain confused | Fixed asset and lease roll-forwards |
| C8 | One-sided elimination; elimination posted in a different currency than the entity balance | Eliminations sheet, intercompany reconciliation |
