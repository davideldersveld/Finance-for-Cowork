# Price adjustment mechanisms — formulas and checks

Always apply the contract's own wording first. These forms help recognize and compute common mechanisms. Notation: P0 current price, P1 adjusted price, I_base index at the base reference period, I_review index at the review reference period.

## Mechanism forms

| Mechanism | Formula | Notes |
|---|---|---|
| Fixed percentage | P1 = P0 x (1 + k) | k stated in contract; no index needed |
| Full index-linked | P1 = P0 x (I_review / I_base) | Base resets at each review unless cumulative-from-base |
| Partial (fixed portion a, indexed portion b, a + b = 1) | P1 = P0 x (a + b x I_review / I_base) | Often used where only labour or materials are indexed |
| Multi-index basket | P1 = P0 x (a + b1 x L1/L0 + b2 x M1/M0 + ...) | Each index weight from contract; weights must sum to 1 with a |
| Index minus efficiency | P1 = P0 x (1 + max(0, index change - e)) | e stated in contract; check whether the floor at zero applies |
| Cost pass-through | P1 = P0 + documented cost change x pass-through share | Requires the evidence the clause names (invoices, audited cost data) |
| Open-book | Price rebuilt from agreed cost base plus agreed margin | Check each cost line against evidence; margin fixed by contract |

## Caps, floors and collars

- Apply after computing the formula result: allowable % = min(max(computed %, floor), cap).
- Collar: no adjustment while the computed change is inside a band (for example +/- 2%); outside it, the contract states whether the whole change or only the excess applies.
- Cumulative cap: total adjustments since contract start may not exceed a stated percentage; track cumulative = product of (1 + each prior adjustment) - 1.

## Reference periods and lag

- Identify which month, quarter or annual average the contract names. "Latest published at the review date" means the release available on that date, not the reference period ending on that date.
- Publication lag: if the index for month M is released in month M+1 or later, the review uses the value released by the review date.
- Annual average: mean of the 12 monthly values for the named period, computed in code from cited values.

## Revisions and rebasing

- If the publisher revises values, use the vintage the contract names; if silent, compute with first-published and latest values and flag any difference.
- If the publisher rebases the series (new reference year = 100), use the publisher's linking factor or compute both values on the same base; never mix bases in one ratio.

## Compounding versus cumulative-from-base

| Basis | Calculation |
|---|---|
| Year-on-year (compounding) | Each review uses the prior review's index as the new base |
| Cumulative-from-base | Each review compares to the original base index and applies to the original base price; prior adjustments are not added on top |

Check the supplier has not applied a year-on-year change to an already-indexed price under a cumulative-from-base clause (double counting).

## Condition checks

| Condition | Test | Status if failed |
|---|---|---|
| Notice period | Effective date requested - date notice received >= required days, using calendar or business days as the contract states | Condition not met |
| Notice method | Delivered by the method and to the address the contract requires | Condition not met |
| Frequency | Months since last adjustment >= minimum interval | Condition not met |
| Evidence | Supplier supplied the evidence the clause names | Condition not met |
| Price-hold period | No increase within any fixed-price period | Not supported |

## Recalculation sheet columns

Line | Item or service | Unit | Current price (P0) | Clause | Index series | I_base (period, value, source) | I_review (period, value, source) | Computed % | Cap | Floor | Allowable % | Allowable price | Requested price | Requested % | Annual volume (source) | Requested amount | Allowable amount | Excess | Status
