# Sensitivity techniques and layouts

## Base-case reproduction

| Output | Supplied model value | Replica or copy value | Difference | Within tolerance |
|---|---|---|---|---|

All chosen outputs must be within the user's tolerance before any flexing. Record the model file, version and output cell references.

## Scenario definition table

| Scenario | Narrative (one line) | Input ID | Base | Scenario value | Linked to | Label |
|---|---|---|---|---|---|---|

- Linked to: the input whose movement implies this one (for example price weakness linked to volume decline), with the stated relationship.
- Unlisted inputs stay at base.

## One-way sensitivity

For each input k with low L_k and high H_k:
- Output_low = f(base with x_k = L_k); Output_high = f(base with x_k = H_k)
- Swing_k = |Output_high − Output_low|
- Tornado: sort descending by Swing_k; bars drawn from Output_low to Output_high around the base line.
- Elasticity (optional) = (% change in output) / (% change in input), computed from the high case.

## Two-way grid

Rows = values of input A, columns = values of input B, cell = f(base with A = a, B = b). Include the base values as a row and a column; mark the base cell. Use full recalculation per cell, never linear interpolation from one-way results (interaction would be lost).

## Breakeven formulas

| Target | Closed form (single product, linear) |
|---|---|
| EBITDA = 0, solve units | Fixed cost / (Price − Variable cost per unit) |
| EBITDA = 0, solve price | Variable cost per unit + Fixed cost / Units |
| EBITDA = target T, solve units | (Fixed cost + T) / (Price − Variable cost per unit) |
| Margin of safety | (Base units − Breakeven units) / Base units |

Non-linear models: bisection between two input values that bracket the target; stop when |Output − Target| ≤ stated tolerance; report the iterations and the bracket. If no bracket exists in the plausible range, report "No breakeven in tested range".

## Reverse stress test

Find the smallest combined move of named inputs (moving together along the scenario narrative) at which an output breaches a stated threshold (for example closing cash below the minimum). Report the multiplier on the downside moves at which the breach occurs.

## Carrying scenarios to cash

- Receivables = Revenue × DSO / days in period; Inventory = COGS × DIO / days; Payables = COGS × DPO / days
- Operating cash flow = EBITDA − ΔNWC − cash taxes (stated rate) ± other stated items
- Closing cash = Opening cash + Operating cash flow − Capex − Debt service − Dividends
- Breach if Closing cash < Minimum cash (threshold from the user or the Finance Profile)

## Assumption labels

| Label | Meaning | Treated in review packs as |
|---|---|---|
| Sourced | From a cited document, data set or system extract | Evidenced |
| User-stated | Given by the user or a named owner, dated | Hypothesis |
| Inferred | Derived by the skill; derivation shown | Hypothesis |

## Verification checklist

1. Base column = supplied model outputs.
2. Each one-way at base value = base output.
3. Grid base cell = base output.
4. Breakeven input re-run returns the target within tolerance.
5. Scenario outputs foot across periods to annual totals.
