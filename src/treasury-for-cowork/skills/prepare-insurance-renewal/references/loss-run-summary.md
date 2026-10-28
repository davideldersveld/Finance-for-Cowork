# Loss run summary rules

## Inputs

Carrier-issued loss runs (or third-party administrator reports for self-insured retentions), each with carrier, line, policy number, policy period and valuation date. Use the number of years the broker or underwriters request (commonly five for casualty lines). Include all policy years in that window, including years with no claims, which need a "no known losses" confirmation from the carrier or the insured.

## Fields per claim (internal workpaper)

Claim number, line, policy year, date of loss, date reported, status (open, closed, reopened), cause or coverage part, location, paid indemnity, paid expense (ALAE), case reserve indemnity, case reserve expense, recoveries (salvage, subrogation, deductible reimbursement), total incurred, net incurred, amount within retention and amount above retention. Exclude claimant names, injury descriptions, medical information and driver identities from all outputs.

## Formulas

- `Total incurred = Paid indemnity + Paid expense + Case reserves (indemnity and expense)`.
- `Net incurred = Total incurred − Recoveries`.
- `Within retention = min(Net incurred per occurrence, Retention per occurrence)`; `Above retention = Net incurred − Within retention` (respect aggregate retentions and whether expense erodes the retention, per the policy).
- `Frequency = Claim count ÷ Exposure units` (for example per 100 vehicles or per 1 million of payroll), using the same exposure base as the rating.
- `Severity = Net incurred ÷ Claim count` (state whether closed-without-payment claims are included).
- `Loss ratio = Net incurred ÷ Earned premium` for the same policy year (insured layer only when premium relates only to the insured layer).

## Summary table (by line and policy year)

Policy year, valuation date, claim count (open, closed), paid, reserves, total incurred, recoveries, net incurred, within retention, above retention, exposure, frequency, severity, earned premium, loss ratio, maturity note.

## Large losses

List every claim with net incurred at or above the profile's large-loss threshold, by claim number: date of loss, line, status, cause, paid, reserves, net incurred, and a factual one-line description without personal data. Note reserve changes between valuations if multiple runs exist.

## Quality labels

| Label | Rule |
|---|---|
| Current | Valuation date within the age the broker or underwriters require (often 90 days before submission) |
| Stale valuation | Valuation older than required |
| Missing year | Policy year in the window with no run and no "no known losses" confirmation |
| Inconsistent | Run totals do not foot, or differ from the prior run for closed claims without explanation |

## Development and maturity

- Recent policy years are immature: reserves can develop and late-reported claims can emerge. Label the latest years as immature.
- Where several valuations exist, show incurred development between valuations as an observation (`Change = Incurred at later valuation − Incurred at earlier valuation`).
- Do not apply loss development factors, trend factors or IBNR unless an actuary or the broker supplies them, with their source.

## Claims-made lines

Summarize claims-made lines (D&O, cyber, professional liability, EPL) by report year rather than accident year, and record the retroactive and continuity dates.
