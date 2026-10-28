# Investment metrics: formulas, conventions and worked schedule

## Conventions to state on every output

- Currency and units; nominal or real; pre-tax or post-tax.
- Discount rate r and its source (user, capital policy in the Finance Profile).
- Timing: end-of-year (t = 1, 2, ... N) or mid-year (t − 0.5 for operating flows; t0 outlay undiscounted).
- Horizon N and terminal value treatment.

## Incremental cash flow per year

CF_t = − Capex_t + (Incremental revenue_t − Incremental cash costs_t) × (1 − Tax rate) + Tax depreciation_t × Tax rate − ΔWorking capital_t + After-tax salvage_N − Cannibalized contribution_t × (1 − Tax rate) − Opportunity cost_t

- After-tax salvage = Salvage value − (Salvage value − Tax book value) × Tax rate
- Working capital released at the end of the horizon unless the user says otherwise
- Exclude: sunk costs, unchanged allocated overhead, interest and principal (when r is a cost of capital)

## Metrics

| Metric | Formula | Notes |
|---|---|---|
| NPV | Σ_(t=0..N) CF_t / (1 + r)^t | Mid-year: exponent t − 0.5 for t ≥ 1 |
| IRR | r* such that Σ CF_t / (1 + r*)^t = 0 | Solve numerically (bisection or Newton) to 0.01% |
| MIRR | (Σ positive CF_t × (1 + r_reinv)^(N − t) / Σ |negative CF_t| / (1 + r_fin)^t)^(1/N) − 1 | Use when CF signs change more than once |
| Simple payback | Y + |Cumulative CF_Y| / CF_(Y+1) | Y = last year with negative cumulative CF; "Not reached" if never positive within N |
| Discounted payback | Same on discounted CF | |
| Profitability index | PV(CF_1..N) / |CF_0| | > 1.0 equivalent to NPV > 0 |
| Terminal value (growing perpetuity) | CF_(N+1) / (r − g), discounted by (1 + r)^N | Only if r > g; show TV share of NPV |
| Equivalent annual amount | NPV × r / (1 − (1 + r)^(−N)) | For alternatives with unequal lives |
| Annuity factor | (1 − (1 + r)^(−N)) / r | Shortcut for level flows |
| Breakeven level annual CF | |CF_0| / Annuity factor | NPV = 0 |

## Worked schedule (USD thousands, r = 10.0%, end-of-year)

| Year | CF | Discount factor | Discounted CF | Cumulative CF | Cumulative discounted |
|---|---|---|---|---|---|
| 0 | (1,000.0) | 1.0000 | (1,000.0) | (1,000.0) | (1,000.0) |
| 1 | 300.0 | 0.9091 | 272.7 | (700.0) | (727.3) |
| 2 | 300.0 | 0.8264 | 247.9 | (400.0) | (479.3) |
| 3 | 300.0 | 0.7513 | 225.4 | (100.0) | (253.9) |
| 4 | 300.0 | 0.6830 | 204.9 | 200.0 | (49.0) |
| 5 | 300.0 | 0.6209 | 186.3 | 500.0 | 137.2 |

NPV = 137.2; IRR = 15.2%; simple payback = 3 + 100.0 / 300.0 = 3.3 years; discounted payback = 4 + 49.0 / 186.3 = 4.3 years; profitability index = 1,137.2 / 1,000.0 = 1.14; equivalent annual amount = 137.2 × 0.10 / (1 − 1.1^(−5)) = 36.2.

## Assumption challenge checklist

| Area | Challenge question |
|---|---|
| Volume ramp | How does the ramp compare with the last comparable launch? Signed orders or letters of intent? |
| Price | Is the price above current realized price? Discounts and rebates included? |
| Cost savings | Which contracts, roles or processes change, and when? |
| Working capital | Inventory, receivables and payables build included and released? |
| Maintenance capex | Included after year 1? |
| Tax | Rate, depreciation basis and timing of tax payments stated? |
| Cannibalization | Effect on existing products quantified? |
| Terminal value | What share of NPV comes from terminal value? Growth rate below r and supported? |
| Alternatives | Is "do nothing" truly flat, or does the base case decline? |
| Timing | Delay of one year — effect on NPV? |

## Sponsor walk

Sponsor NPV + Σ adjustments (each named: sunk cost removed, tax added, working capital added, convention changed, rate corrected) = Recomputed NPV. The sum must be exact.
