# Workforce cost formulas, conventions and privacy rules

## Units

- Headcount (heads): people on payroll at period end.
- FTE: Σ contracted weekly hours / standard full-time weekly hours.
- Average FTE for a period = (Opening FTE + Closing FTE) / 2, or the mean of monthly FTE for quarters and years.
- Contractors and agency workers: separate line, cost from invoices or purchase orders, never mixed into employee FTE.

## Fully loaded cost per FTE (band level)

Loaded annual cost = Base pay × (1 + Employer tax % + Benefits % + Bonus target % × Expected payout %) + Other per-FTE costs

- Base pay: band average or band midpoint as the user states (state which).
- Employer tax with a wage cap: Employer tax = Rate × min(Base pay, Cap). At band level apply to the band average and state the approximation.
- Merit: Base pay_m = Base pay × (1 + Merit %) for months on or after the effective month.
- Monthly loaded cost = Loaded annual cost / 12 (use pay-period counts if payroll is not monthly, and state the basis).

## Timing conventions

| Convention | Hire in month m | Leaver in month m |
|---|---|---|
| Full month | Counts fully from month m | Counts fully through month m |
| Start-of-next-month | Counts from month m + 1 | Counts through month m |
| Day-weighted | (Days in m from start date) / (Days in m) | (Days in m to exit date) / (Days in m) |

- Expected fill date = Requisition approval date + Hire lag (months or days as stated).
- Vacancy factor (optional): Cost after vacancy = Planned cost × (1 − Vacancy factor); show the reduction as its own line.

## Headcount roll

Closing_m = Opening_m + Hires_m − Leavers_m + Transfers in_m − Transfers out_m
Opening_(m+1) = Closing_m

Attrition rate (annualized, cohort level) = Leavers over 12 months / Average headcount over 12 months.

## Plan versus actual

For each cost centre × band and period:
- Rate_P = Cost_P / FTE_P; Rate_A = Cost_A / FTE_A
- Volume effect = (FTE_A − FTE_P) × Rate_P
- Rate effect = (Rate_A − Rate_P) × FTE_A
- Check: Volume + Rate = Cost_A − Cost_P
- Optional band-mix effect at cost centre level: Σ_b (FTE_A,b − FTE_A × share_P,b) × Rate_P,b, with the volume effect then measured at the plan average rate; state which version is used.

Typical evidenced explanations for rate effects: merit effective month different from plan; overtime (overtime report); bonus true-up (bonus accrual schedule); band mix; employer tax cap reached mid-year.

## Run-rate

- Exit run-rate = Last month cost × 12
- Cross-check = Exit FTE × Loaded annual cost (current rates)
- Gap to next-year plan = Next-year plan − Exit run-rate; explain by planned hires and leavers, merit, vacancy factor.

## Privacy rules (apply before every delivery)

1. Work from aggregated data; employee-level rows are aggregated at intake and not reproduced.
2. Minimum reporting group size comes from the user's policy; cells below it are merged into the adjacent band or an Other row.
3. If no minimum is stated, ask; until answered, show no cell representing one or two people.
4. Remove names, employee IDs and personal attributes from all outputs.
5. Do not compute or display averages for a group below the minimum size, even inside a larger table.
6. Decline any ranking, scoring or selection of individuals.
