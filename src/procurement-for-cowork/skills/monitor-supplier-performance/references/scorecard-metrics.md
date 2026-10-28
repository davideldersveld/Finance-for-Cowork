# Scorecard metric definitions

The contract's definition always governs. Use these definitions where the contract is silent, and record that the default was used.

## Delivery

| Metric | Formula | Unit of measure | Data needed |
|---|---|---|---|
| On-time delivery | Lines delivered within the on-time window / lines due in period | Order line (or order, per contract) | Due date, receipt date, window (for example 0 days early to 0 days late, or contract-defined) |
| In-full delivery | Lines received at ordered quantity (within any contract quantity tolerance) / lines due | Order line | Ordered and received quantity |
| OTIF | Lines both on time and in full / lines due | Order line | Both of the above on the same line |
| Lead time | Median days from order to receipt | Days | Order and receipt dates |
| Fill rate | Units delivered / units ordered | Units | Quantities |

Due in period = lines with a due date in the period, including those not yet delivered (count as failed). Lines cancelled by the buyer before the due date are excluded and listed.

## Quality

| Metric | Formula | Notes |
|---|---|---|
| Defect rate (PPM) | Defective units / units received x 1,000,000 | Defects confirmed by inspection or customer complaint traced to the supplier |
| Return rate | Units returned to supplier / units delivered | Same period basis for numerator and denominator, or state the lag |
| First-pass yield | Lots accepted at first inspection / lots inspected | Lot basis |
| Corrective actions overdue | Count of supplier corrective actions past due date | From quality log |

## Service

| Metric | Formula | Notes |
|---|---|---|
| SLA attainment | Measurements meeting target / total measurements | Per service level, per measurement period |
| Availability | (Scheduled minutes - unplanned downtime minutes) / scheduled minutes | Exclude planned maintenance only if the contract allows |
| Response time | Median and 90th percentile hours to first response | Report both |
| Resolution time | Share resolved within target by priority | Per priority level |
| Backlog | Open tickets older than target at period end | Count |

## Commercial

| Metric | Formula | Data needed |
|---|---|---|
| Invoice accuracy | Invoices with no price, quantity, tax or reference error / invoices received | Match exception report from Accounts Payable |
| Price compliance | Invoice lines at contract price / invoice lines | Contract price list, invoice lines |
| Credit note frequency | Credit notes / invoices | AP data |

## RAG rule (record on the scorecard)

- Green: attainment at or above target (or at or below for "lower is better" metrics such as PPM).
- Amber: worse than target but within the amber band stated by the user or profile.
- Red: worse than the amber band.
- No band supplied: Green or Red only, and say so.

## Trend rule

Latest period versus mean of prior periods. Improving or Deteriorating when the change exceeds the user's stated tolerance; otherwise Stable. State polarity (higher is better or lower is better) for each metric.

## Service credit worksheet columns

Period | Service level | Clause | Measurements | Met | Excluded (evidenced) | Excluded (claimed, no evidence) | Attainment | Tier | Credit % | Applicable charges | Credit before cap | Cap % | Cap amount | Credit after cap | Earn-back applied | Net credit | Claim deadline | Status (Calculated / If exclusion accepted / Insufficient data)
