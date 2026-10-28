# Driver library, calibration checks and register layout

## Common driver formulas

| P&L line | Formula | Typical evidence for Evidenced label |
|---|---|---|
| Product revenue | Units × Net price per unit | Signed orders, price list, contract volumes |
| Pipeline-led revenue | Σ(Opportunity value × Stage win rate) by expected close period | CRM extract with stage history; win rates from closed history |
| Subscription revenue | Average customers × ARPU; Closing = Opening + New − Churned | Billing system counts; churn from trailing cohorts |
| Usage revenue | Active users × Usage per user × Rate | Usage logs, rate card |
| Services revenue | Billable FTE × Available hours × Utilization × Realized rate | Timesheets, rate cards, staffing plan |
| Discounts and rebates | Gross revenue × Discount % by customer tier | Contract terms, trailing realized discount |
| Materials cost | Units × Bill-of-materials cost × (1 + Scrap %) | Standard cost file, supplier contracts |
| Freight | Units or shipments × Cost per unit or shipment | Carrier rate cards, trailing actuals |
| People cost | Average FTE × Loaded cost per FTE (band level) | Workforce plan output |
| Commissions | Eligible revenue × Plan rate | Commission plan document |
| Rent and fixed contracts | Contracted amount by period | Lease or contract schedule |
| Other opex | Run-rate × (1 + inflation) + known one-offs, or Revenue × stable ratio | Trailing actuals; ratio stability shown |

Average customers or FTE in a period = (Opening + Closing) / 2 unless the data supports a daily or monthly average.

## Calibration checks

1. Implied driver from actuals for each trailing period (for example Implied price = Revenue / Units).
2. Trailing average, minimum and maximum over the periods the user states.
3. Forecast value inside the trailing range: no flag. Outside the range: record the reason and evidence in the register.
4. Ratio stability test before using "% of revenue": coefficient of variation of the ratio = standard deviation / mean over trailing periods; report it, and let the user decide whether it is stable enough.

## Back-test metrics

- Bias = Σ(Forecast − Actual) / Σ Actual. Positive means over-forecasting.
- MAPE = mean over periods of |Actual − Forecast| / |Actual|; skip periods where Actual = 0 and say so.
- Report by line and in total; never tune a driver to make the back-test look better without recording the change.

## Assumptions register columns

| Column | Content |
|---|---|
| ID | D-001, D-002 ... stable across versions |
| Driver | Plain name, for example "Beverages net price per case" |
| Value | By period or period block |
| Unit | Currency per unit, %, FTE, hours |
| Applies to | Lines, entities, periods |
| Source | File + sheet + cell, system extract with date, or meeting note with date and attendees |
| Owner | Name and role accountable for the value |
| Captured | Date |
| Label | Evidenced or Hypothesis |
| Prior value | Value in the prior forecast |
| Change reason | Short reason with source |

## Attribution of change versus prior forecast

For a line Y = f(d1, d2, ...):
- Effect of driver k = f(prior values with dk set to new value) − f(all prior values).
- Interaction = (New Y − Prior Y) − Σ effects.
- For Y = Q × P: Volume = (Qn − Qp) × Pp; Price = (Pn − Pp) × Qp; Interaction = (Qn − Qp) × (Pn − Pp).
