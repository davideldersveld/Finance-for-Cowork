# Expense test catalogue

Each test cites the rule ID from the rule register and the policy clause. Limits, factors, windows and rates come from the policy or the user; never assume them.

| ID | Test | Rule | Amount at issue | Status if failed |
|---|---|---|---|---|
| T1 | Receipt present | Receipt attached when amount ≥ receipt threshold | Full line | Needs documentation |
| T2 | Receipt agrees | Amount, date, merchant and currency on receipt agree with line | Difference, or full line if unreadable | Needs documentation |
| T3 | Itemized receipt | Itemized receipt where policy requires (hotel folio, meals) | Full line | Needs documentation |
| T4 | Category limit | Per-person amount = amount ÷ attendees ≤ limit | max(0, amount − limit × attendees) | Policy exception |
| T5 | Hotel nightly limit | Nightly rate ≤ city-tier limit | max(0, nightly rate − limit) × nights | Policy exception |
| T6 | Per diem | Claimed ≤ allowable; no actual meals and per diem on the same day unless allowed | max(0, claimed − allowable) | Policy exception |
| T7 | Mileage | Claimed ≤ (distance − commute deduction) × rate on trip date | max(0, claimed − allowable) | Policy exception; Distance not verified noted separately |
| T8 | Approver independence | Approver ≠ claimant and not a direct report of the claimant | Full report | Policy exception |
| T9 | Approval level | Approver level ≥ level required for the report total | Full report | Policy exception |
| T10 | Approval timing | Submission ≤ approval < reimbursement | None (process exception) | Policy exception |
| T11 | Duplicate within employee | Same employee + amount + date + merchant in two lines or reports | Duplicate line(s) | Policy exception |
| T12 | Duplicate across employees | Same receipt image, folio or bill reference claimed by two employees | Second and later claims | Policy exception |
| T13 | Card and cash duplicate | Card transaction also claimed out-of-pocket | Out-of-pocket line | Policy exception |
| T14 | Split claim | Same merchant + date (or same bill) across lines, claims or employees; each under a limit or approval band, combined above | Combined excess over the limit | Policy exception |
| T15 | Weekend or holiday | Spend on weekend or public holiday with no trip covering the date | None | Review - out of pattern |
| T16 | Outside itinerary | Date or city outside the trip itinerary | None | Review - out of pattern |
| T17 | During leave | Spend on a recorded leave day (roster supplied) | None | Review - out of pattern |
| T18 | Round amount cash | Out-of-pocket amount ending in .00 above the receipt threshold without receipt | None | Review - out of pattern |
| T19 | Outlier | Amount > user or profile multiple of the employee or peer median for the category | None | Review - out of pattern |
| T20 | Prohibited item | Category or merchant type on the prohibited list | Full line | Policy exception |
| T21 | Late submission | Submission date − line date > policy window | None | Policy exception |
| T22 | Currency conversion | Converted amount differs from policy rate method by more than allowed | Difference | Policy exception |

## Per diem formula

Allowable = Σ over travel days of (location daily rate × day factor) − Σ provided-meal deductions.
Day factor: first and last day per policy (for example 0.75 if the policy says so); full days 1.00. Provided-meal deduction per policy (fixed amount or percentage of the daily rate per meal).

## Mileage formula

Allowable = (round-trip distance − commute deduction, if required) × rate in force on the trip date. When the rate changes mid-period, apply by date.

## Roll-up and no double counting

- Line status = most severe failed test: Policy exception > Needs documentation > Review - out of pattern > Policy unclear > Compliant.
- Line amount at issue = largest single test amount on the line, capped at the line amount.
- Claim amount at issue = sum of line amounts at issue, plus report-level amounts (T8, T9) only where no line amount already covers them.
