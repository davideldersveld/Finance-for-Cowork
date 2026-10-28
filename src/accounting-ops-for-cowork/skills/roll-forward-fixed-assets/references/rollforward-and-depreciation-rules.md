# Roll-forward columns, depreciation conventions and test rules

## 1. Roll-forward columns (per entity and asset class)

| Column | Definition | Source |
|---|---|---|
| Opening cost | Gross cost at the start of the period | Prior closing roll-forward and opening register |
| Additions | Assets capitalized in the period, including direct costs to bring to working condition | Additions listing, invoices |
| Disposals | Gross cost of assets sold, scrapped or retired in the period (entered as a negative) | Disposal records |
| Transfers | Reclassification between classes or entities, and transfers in from CIP | Register transfer log, CIP schedule |
| Impairments (cost) | Where policy writes impairment against cost (common under US GAAP ASC 360, where the written-down amount becomes the new cost basis) | Approved impairment memo |
| FX translation | Difference from translating foreign-entity balances at closing versus opening rates; rates from the user or `translate-currency` | Rate table |
| Closing cost | Sum of the above | Must equal closing register cost |
| Opening accumulated depreciation | Start of period | Prior roll-forward |
| Depreciation | Charge for the period | Register depreciation run |
| Disposals (AD) | Accumulated depreciation removed on disposal | Disposal records |
| Transfers (AD) | Moves with the asset | Transfer log |
| Impairments (AD) | Where policy records impairment in accumulated depreciation and impairment (common under IFRS, IAS 36) | Approved impairment memo |
| FX translation (AD) | As for cost | Rate table |
| Closing accumulated depreciation | Sum of the above | Must equal closing register |
| Net book value | Closing cost - Closing accumulated depreciation | |

If the entity applies the IAS 16 revaluation model to a class, add Revaluation columns for cost (or fair value) and accumulated depreciation and state the policy.

Sign convention - cost and accumulated depreciation shown as positive balances; reductions shown in parentheses.

## 2. Tie-out rows

| Check | Rule |
|---|---|
| R1 | Opening cost and AD = prior period closing roll-forward |
| R2 | Closing cost and AD per roll-forward = closing register, by class |
| R3 | Closing register = ledger cost and AD accounts, by class mapping |
| R4 | Depreciation column = ledger depreciation expense for the period (excluding non-asset items the user names) |
| R5 | CIP transfers out = transfers into classes |
| R6 | Intercompany or inter-entity asset transfers net to zero at group level |

Each check shows the difference and `Ties` or `Does not tie`.

## 3. Depreciation conventions (use the policy's convention)

| Convention | First-period charge | Last-period charge |
|---|---|---|
| Full-month, start following month | Starts the month after the in-service month | Full charge in the disposal month or none, as policy states |
| Full-month, start same month | Full charge in the in-service month | None in the disposal month |
| Half-month | Full month if in service on or before the 15th, otherwise starts next month | Mirror rule on disposal |
| Mid-year (annual) | Half of the annual charge in the year placed in service | Half in the disposal year |
| Actual days | Daily rate x days in service in the period | Daily rate x days to disposal |

Formulas:
- Straight-line monthly = (Cost - Salvage value) / Useful life in months.
- Declining balance monthly = Opening NBV for the year x (rate / 12), with switch to straight-line if the policy requires it; the rate comes from policy.
- Units of production = (Cost - Salvage value) x units in period / total estimated units.
- Accumulated depreciation is capped at Cost - Salvage value; any charge beyond the cap is an exception.

## 4. Capitalization test labels (one per addition)

| Label | Condition |
|---|---|
| Capitalization supported | At or above threshold, nature is a new asset or betterment, invoice and receipt support present, class and life consistent with policy, in-service date present |
| Below threshold - expense candidate | Cost below the capitalization threshold (unless the policy allows pooled or bulk purchases above a group threshold, which is stated) |
| Repair or maintenance - expense candidate | Description or invoice indicates repair, maintenance or replacement of a minor part that does not extend life or capacity |
| Insufficient support | No invoice, no receipt or approval evidence |
| In-service date missing | Asset capitalized (or transferred from CIP) without an in-service date |
| Possible capital item in expense | Item in a repairs or small-equipment expense account at or above threshold with a capital-type description |

## 5. Sampling

- When the user asks for a sample, record the population (count and value), the selection method (for example all items above a value plus a random selection with a recorded seed), and the sample size.
- Report differences found in the sample as facts; any extrapolation is labelled as an estimate for the reviewer, not a conclusion.

## 6. Exceptions list columns

Exception ID, Asset ID, Class, Type (Tie-out break, Capitalization, Depreciation, Disposal, Transfer, Impairment support, Over-depreciated, Aged CIP), Amount, Description, Evidence, Proposed action, Owner.
