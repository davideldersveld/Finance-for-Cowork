# Savings classification, baselines and validation rules

The user's savings policy governs. Use these rules where the policy is silent, and say so on the Savings_Policy sheet.

## Classification tests

| Type | Test | Typical examples | Not this type when |
|---|---|---|---|
| Hard savings | Unit price or total cost on recurring spend is lower than an evidenced baseline, and the spend occurs in the measurement window | Renegotiated price, consolidation discount, specification change lowering unit cost, demand reduction measured against baseline volume | No prior price exists; the reduction offsets an increase the company never paid |
| Cost avoidance | A cost increase is prevented or reduced, or a price is obtained below a quote or market reference without a prior baseline | Increase request held below asked; new category bought below the highest compliant bid; extended price hold | The saving reduces the run-rate against a prior price paid (then it is hard savings) |
| Pipeline - Identified | Opportunity sized but not contracted | Wave plan initiatives | A contract is signed |
| Pipeline - Contracted | Contract signed; no or partial invoicing in the window | New contract effective next quarter | Invoices exist in the window (realized portion moves to hard savings) |

Rebates and retrospective discounts count as hard savings only when received or contractually earned; otherwise Pipeline - Contracted.

One-time savings (for example a one-off waiver) are hard savings in the period realized only; they do not annualize.

## Baseline methods

| Method | Formula | Acceptance test |
|---|---|---|
| Last price paid | Unit price on the last invoice before the contract effective date | Invoice cited; same item, unit of measure and terms |
| Trailing volume-weighted average | Sum of (price x quantity) / sum of quantity over the trailing window | Window per policy; invoice extract cited |
| Prior contract price | Price in the expiring contract | Contract and clause cited; check prices actually paid matched |
| Budget price | Unit price in the approved budget | Accepted only if the policy allows; label clearly |
| Lowest compliant bid or market quote | Reference price at award | Supports cost avoidance only, not hard savings |

Inflation-adjusted baselines are accepted only if the policy permits; the inflation-adjusted portion is cost avoidance, not hard savings.

## Measurement window

Default to the policy's window (often 12 months from contract effective date). Savings after the window are not reported as new value unless the policy says so. Record the window per initiative.

## Validation formulas

| Measure | Formula |
|---|---|
| Claimed annual | (Baseline price - contract price) x forecast annual volume |
| Claimed to date | (Baseline price - contract price) x forecast volume for elapsed periods |
| Realized | Sum over invoice lines of (baseline price - invoiced unit price) x invoiced quantity |
| Gap | Claimed to date - realized |
| Price leakage | (Volume-weighted actual invoiced price - contract price) x actual volume |
| Volume effect | (Forecast volume - actual volume) x (baseline price - contract price) |
| Residual | Gap - price leakage - volume effect (must be zero for a single item; show it if mix or multiple items create one) |
| Realization rate | Realized / claimed to date |

With multiple items, compute per item and sum; a mix effect appears as residual when items are aggregated, and is labelled mix.

## Validation status rule

| Status | Rule |
|---|---|
| Validated | Realization rate within the user's tolerance of 100 percent |
| Partially validated | Realized greater than zero but outside tolerance |
| Not validated | Realized zero or negative, or baseline not evidenced |
| Insufficient data | Invoice lines or volumes missing for the window |
| Reclassified | Claimed type failed its classification test; new type recorded with reason |

## Double-count checks

- Same supplier, item and period appearing in two initiatives.
- A category-wide discount and an item-level renegotiation on the same lines.
- Savings counted both at contract signature (pipeline) and at invoicing (hard) in the same total.
