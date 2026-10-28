# Long-range plan model structure and formulas

## Sheet flow

Inputs (Assumptions) -> Baseline -> Initiatives -> Plan P&L -> Capex & WC -> Cash & Funding -> Target Tests

Each calculation sheet uses formulas only; every constant lives on Assumptions with an ID.

## Baseline formulas (per segment, per year t)

- Volume_t = Volume_(t−1) × (1 + market growth_t + share change_t)
- Price_t = Price_(t−1) × (1 + price change_t)
- Revenue_t = Volume_t × Price_t (or Revenue_(t−1) × (1 + g_vol) × (1 + g_price) where volume data is absent)
- Variable cost_t = Volume_t × Unit cost_(t−1) × (1 + cost inflation_t)
- Fixed cost_t = Fixed cost_(t−1) × (1 + inflation_t) + step costs triggered when Volume_t exceeds a stated capacity point
- EBITDA_t = Revenue_t − Variable cost_t − Fixed cost_t

## Initiative block (one per initiative)

| Field | Content |
|---|---|
| ID, name, owner | I-01 ... |
| Status | Approved / Proposed / Idea |
| Included in plan | Yes / No (user decides) |
| Revenue by year | Ramp profile stated (for example 25% / 60% / 100% of run-rate) |
| Gross margin % | Source cited |
| Opex and one-off costs | By year |
| Capex | By year |
| Working capital | Days or direct amounts |
| Overlap check | Customers, capacity or savings also claimed by another initiative |
| Label | Evidenced / Hypothesis |

## Capex and depreciation

- Maintenance capex_t = stated basis (asset plan or % of revenue the user states)
- Straight-line depreciation of each capex vintage = Cost / Useful life, starting in the year stated (full-year or half-year convention stated)
- Depreciation_t = existing asset base depreciation + Σ vintages

## Working capital

- Receivables_t = Revenue_t × DSO_t / 365
- Inventory_t = COGS_t × DIO_t / 365
- Payables_t = COGS_t × DPO_t / 365 (state if purchases are used instead)
- NWC_t = Receivables_t + Inventory_t − Payables_t
- Cash effect_t = −(NWC_t − NWC_(t−1))

## Cash and funding

- Cash taxes_t = Taxable profit proxy_t × tax rate (user-stated; flag as simplified)
- Unlevered FCF_t = EBITDA_t − Cash taxes_t − Capex_t − ΔNWC_t − Other stated items_t
- Cash before funding_t = Opening cash_t + Unlevered FCF_t − Interest_t − Debt repayment_t − Dividends_t
- Funding need_t = max(0, Minimum cash − Cash before funding_t)
- Closing cash_t = Cash before funding_t + Funding need_t (when the user asks to show the plan funded) or Cash before funding_t (unfunded view); state which view is shown
- Peak cumulative funding need = maximum over t of cumulative funding need

## Target tests

| Metric | Formula |
|---|---|
| Revenue CAGR | (Revenue_end / Revenue_base)^(1/n) − 1 |
| EBITDA margin | EBITDA / Revenue |
| Cash conversion | Unlevered FCF / EBITDA |
| Return on capital (simple) | EBIT / (NWC + Net fixed assets), definition stated |
| Net debt / EBITDA (plan test, not covenant) | (Debt − Cash) / EBITDA |
| Required final-year value at target CAGR | Value_base × (1 + target)^n |

Status: Meets (plan value at or better than target by polarity), Gap (worse), Not tested (input missing).

## Verification checklist

1. Base year per line equals source actuals or approved forecast.
2. Baseline + included initiatives = Plan, every line and year.
3. Opening cash_t = Closing cash_(t−1).
4. NWC balances recompute from days; ΔNWC matches the cash flow line.
5. Excluded initiatives contribute zero to Plan and are listed.
