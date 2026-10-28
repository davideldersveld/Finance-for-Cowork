# Covenant formulas and headroom

These are generic shapes only. The credit agreement's own definitions always govern; rebuild each component from the cited section, in the agreement's order and with its capitalized terms.

## Typical ratio shapes

| Covenant | Typical shape (confirm against the agreement) | Test type |
|---|---|---|
| Total (or Senior, or Secured) Leverage | Consolidated Total Debt ÷ Consolidated EBITDA for the trailing four quarters | Maximum |
| Net Leverage | (Consolidated Total Debt − Unrestricted Cash, subject to any netting cap) ÷ Consolidated EBITDA | Maximum |
| Interest Coverage | Consolidated EBITDA ÷ Consolidated Interest Expense (cash or total, as defined) | Minimum |
| Fixed Charge Coverage | (Consolidated EBITDA − Unfinanced Capital Expenditures − Cash Taxes − Restricted Payments, as defined) ÷ (Scheduled Principal Payments + Cash Interest Expense, as defined) | Minimum |
| Minimum Liquidity | Unrestricted cash + Availability under the revolver, as defined, at the test date or on each day | Minimum amount |
| Capital Expenditure limit | Capital Expenditures in the fiscal year ≤ Cap, plus any permitted carry-forward of unused amounts from the prior year | Maximum amount |
| Minimum Net Worth / Tangible Net Worth | As defined, often with step-ups from retained earnings | Minimum amount |

## Common EBITDA build items to look for in the definition

Starting point (usually Consolidated Net Income), plus: interest expense, income tax expense, depreciation and amortization, non-cash charges (with any exclusion for items that become cash later), extraordinary, unusual or non-recurring charges (often capped), restructuring and integration costs (often capped and time-limited), transaction costs, stock-based compensation, run-rate cost synergies (often capped, with a realization window and officer certification), pro forma EBITDA of acquired businesses; less: non-cash gains, interest income, unusual gains. Record each item's cap, base, time limit and certification requirement.

## Cap application

`Permitted add-back = min(Actual amount supported, Cap % × Cap base)`, where the cap base is exactly as defined. When the definition applies one aggregate cap across several categories, apply it once across their sum. When the base is unclear, log an ambiguity.

## Headroom measures

| Measure | Maximum test (for example leverage) | Minimum test (for example interest cover) |
|---|---|---|
| Ratio headroom % | (Maximum − Actual) ÷ Maximum | (Actual − Minimum) ÷ Minimum |
| EBITDA cushion | EBITDA − Debt ÷ Maximum | EBITDA − Minimum × Denominator |
| EBITDA cushion % | EBITDA cushion ÷ EBITDA | EBITDA cushion ÷ EBITDA |
| Debt capacity | Maximum × EBITDA − Debt | Not applicable |
| Denominator capacity | Not applicable | EBITDA ÷ Minimum − Denominator |

Amount tests (liquidity, capex): `Headroom = Actual − Minimum` or `Cap − Actual`, and as a percentage of the minimum or cap.

The EBITDA cushion % is the decline in EBITDA, with debt held constant, that would bring the ratio exactly to the level. State that assumption next to the figure.

## Status rules

| Status | Rule |
|---|---|
| Compliant | Passes; headroom measure the profile names is at or above the alert threshold |
| Near breach | Passes; headroom below the alert threshold |
| Breach indicated | Fails on the calculation as prepared; not a legal determination |
| Definition unclear | Status differs between reasonable readings |
| Not testable | A required component or level is missing |

## Projection rules

- Roll LTM: `LTM(q) = Sum of the four quarters ending q`, mixing actual and forecast quarters with each labelled.
- Use the level applicable at each future test date per the step-down schedule.
- Debt at future dates from the register schedule (amortization, maturities) and cash from the forecast; do not assume refinancing or new draws unless the forecast includes them.
- Map forecast lines to definition components explicitly; list unmapped components as `Not testable`.
- Do not apply equity cures or pro forma adjustments to projections unless the user supplies them with support.
