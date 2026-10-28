# Budget submission validation rules and status transitions

## Template integrity tests (run before any guideline test)

| ID | Test | Rule | Fail outcome |
|---|---|---|---|
| T-01 | Structure | Sheet names, row order, account codes and period columns match the issued template version | Resubmission requested |
| T-02 | Periods | Every period in the cycle has an entry (zero is allowed only if typed as zero) | Resubmission requested |
| T-03 | Footing | Each subtotal equals the sum of its lines; each annual total equals the sum of its periods | Resubmission requested |
| T-04 | Control total | Control-total cell equals the sum of all input lines | Resubmission requested |
| T-05 | Accounts | Every account code exists in the chart-of-accounts mapping and is open for budgeting | Resubmission requested |
| T-06 | Signs | Revenue and cost signs follow the convention in the guideline pack | Resubmission requested |
| T-07 | Unit identity | Unit code inside the file matches the tracker row | Unmatched file, ask the user |

## Guideline tests (examples of the shape; actual rules come from the issued guidelines)

| ID | Rule type | Formula | Data needed |
|---|---|---|---|
| G-01 | Growth cap on a line or total | Growth % = (Submitted − Base) / Base; Excess = Submitted − Base × (1 + Cap %) | Base by line, cap % |
| G-02 | Absolute ceiling | Excess = Submitted − Ceiling | Ceiling |
| H-01 | Net new FTE | Net new FTE = Closing FTE − Opening FTE; compare with approved additions | Opening FTE, approved additions |
| H-02 | Role band | Every planned role sits in an approved band | Band list |
| H-03 | Backfill | Each backfill links to a leaver row in the same cost centre | Leaver rows |
| A-01 | Key completeness | Every allocation key set sums to 100.0% (tolerance only if stated) | Key table |
| A-02 | Pool integrity | Allocated total = source pool | Pool amount |
| P-01 | Assumption usage | Recomputed driven line = submitted line, using issued inflation, merit and FX rates | Issued assumptions |

Each test records: Expected or limit, Submitted, Difference, Result (Pass / Fail / Not testable), and the source cell range.

## Status transitions

```
Not started -> In progress -> Submitted -> Validated -> Accepted (set by a person only)
                          \-> Submitted -> Off-guideline -> (resubmitted) Submitted
                          \-> Submitted -> Resubmission requested -> (resubmitted) Submitted
Not started / In progress -> Missing (deadline passed, nothing received)
Missing -> Late (file received after deadline) -> validated as for Submitted
```

- `Days late = Received date − Due date` in calendar days, never negative.
- A justified exception (owner explanation accepted by the user) is recorded in Open issues; the test result stays Fail, the status may move to Validated only on the user's instruction.

## Consolidation checks

1. Consolidated total = sum of included submission control totals (difference must be zero).
2. Excluded block lists every unit not included and why.
3. Intercompany lines listed by counterparty pair with both sides' amounts; unmatched pairs flagged.
4. Translation uses only the issued budget rates; the rate table is shown on the About sheet.
