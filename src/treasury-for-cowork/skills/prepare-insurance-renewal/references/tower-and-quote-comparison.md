# Coverage tower and quote comparison

## Tower notation and terms

- Layer notation: `Limit xs Attachment`, for example USD 25m xs USD 25m. A participation is written `Share p/o Layer`, for example USD 10m p/o USD 25m xs USD 25m (a 40 percent share).
- Primary: the first insured layer above the retention.
- Umbrella: excess layer that sits over scheduled underlying policies and may drop down over exhausted aggregates or cover gaps in underlying coverage, subject to its own retention.
- Excess / follow form: layer following the terms of a lead or underlying policy, subject to its own exclusions.
- Buffer layer: a layer between primary and a lead umbrella or excess.
- Quota share: several insurers share one layer by percentage.
- Deductible: the insurer handles the claim and is reimbursed by the insured; the limit may be inclusive of or in addition to the deductible, per the policy.
- Self-insured retention (SIR): the insured pays and handles losses up to the SIR before the policy responds; often with collateral or claims-handling requirements.
- Aggregate: the maximum the layer pays in the policy period; erosion of underlying aggregates can cause drop-down if the excess policy provides it.
- Reinstatement: restoring an exhausted aggregate, sometimes for additional premium.

## Continuity test (state the convention)

Present attachment points on one convention for the whole tower: either above the primary limits (common for casualty) or from ground up including the retention (common for property and SIR programs). Then in code:

- `Attachment(1) = Primary limit` (or `Retention + Primary limit` on the ground-up convention).
- `Attachment(n) = Attachment(n−1) + Limit(n−1)`.
- `Continuous` if equal; `Gap` if Attachment(n) > Attachment(n−1) + Limit(n−1) (gap amount = difference); `Overlap` if lower.
- Quota-share participations in each layer sum to 100 percent; otherwise `Participation not 100 percent` with the unplaced share.
- Program limit = sum of layer limits; check against the limit the risk manager targets.

## Layer pricing measures

| Measure | Formula |
|---|---|
| Rate on line (ROL) | Layer premium ÷ Layer limit |
| Price per million | Layer premium ÷ (Layer limit ÷ 1,000,000) |
| ROL change | Renewal ROL ÷ Expiring ROL − 1 |
| Layer share of program premium | Layer premium ÷ Program premium |

Higher layers normally carry a lower ROL than layers beneath them; a higher ROL in a higher layer is reported as an observation, not an error.

## Rate and premium change

| Line | Typical exposure base |
|---|---|
| Property | Per 100 of TIV |
| General liability | Per 1,000 of revenue (or as rated) |
| Workers' compensation | Per 100 of payroll by class |
| Auto | Per vehicle or per power unit |
| D&O, cyber, crime | Often flat; report premium change and ROL instead of a rate per exposure |

- `Rate = Premium ÷ Exposure base`
- `Rate change = Renewal rate ÷ Expiring rate − 1`
- `Exposure change = Renewal exposure ÷ Expiring exposure − 1`
- `Premium change = Renewal premium ÷ Expiring premium − 1`
- Identity: `(1 + Premium change) = (1 + Exposure change) × (1 + Rate change)`.
- Compare premiums on a consistent basis: base premium, terrorism premium, taxes (for example surplus lines tax and stamping fees, insurance premium tax), fees (broker fee, fronting fee) and commission shown separately; totals before and after taxes and fees.
- Pure rate change ignores term changes. A coverage-adjusted (risk-adjusted) rate change requires a valuation of term changes by the broker or an actuary; show it only when supplied, with its source.

## Term-by-term comparison rows

| Category | Terms to compare |
|---|---|
| Limits | Per occurrence, aggregate, products-completed operations aggregate, program limit, reinstatements |
| Attachment and retention | Attachment point, deductible or SIR per occurrence and aggregate, percentage deductibles for catastrophe perils (percent of values, minimum and maximum), waiting periods in hours for business interruption and cyber |
| Sublimits | Flood, earthquake, named windstorm, contingent business interruption, ordinance or law, debris removal, transit, spoilage, cyber extortion, social engineering; whether within or in addition to the limit |
| Conditions | Coinsurance or margin clause, valuation basis, period of indemnity and extended period, territory, cancellation terms, claims-control or consent provisions |
| Claims-made terms | Retroactive date, continuity date, prior and pending litigation date, extended reporting period |
| Exclusions and endorsements | Additions and removals, for example communicable disease, cyber exclusion on non-cyber lines, war, PFAS, sanctions clause, wildfire, abuse; quote the endorsement name and number |
| Security | Insurer, financial strength rating as supplied by the broker, share |
| Commercial | Premium, taxes, fees, commission, payment terms, subjectivities and their deadlines |

## Term status

| Status | Rule |
|---|---|
| Broader | More favorable to the insured (higher limit, lower retention, removed exclusion, wider territory) |
| Narrower | Less favorable (lower limit or sublimit, higher retention, added exclusion, longer waiting period) |
| Equivalent | Same wording or same values |
| Not comparable | Form or structure differs so the term cannot be set side by side without coverage interpretation; refer to the broker |
| Not quoted | The insurer did not quote the term or layer |

Each status cites the quote page, form or endorsement. Interpretation of wording differences is for the broker, risk manager and counsel.
