# Expected-receipts schedule (hand-off to Treasury)

This schedule is the collections input to `forecast-short-term-cash` in Treasury for Cowork. Keep the sheet name and columns exactly as below so Treasury can consume it without remapping.

## Scope

- Covers only invoices open and undisputed at the as-of date, per entity and transaction currency.
- Collections on sales not yet invoiced are outside scope; Treasury forecasts them from its own sales or receipts drivers.
- Reporting-currency columns are added only if the user or profile supplies the rate, rate type and rate date.

## Week structure

- 13 weekly buckets starting on the first week start on or after the as-of date, using the week convention from the profile or Treasury's forecast (for example Monday to Sunday). If unknown, ask on the question card.
- Column headers show the week-start date, for example `Wk 1 (2026-11-02)`.

## Expected-date basis hierarchy (first applicable wins)

| Order | Basis label | Expected date | Default confidence |
|---|---|---|---|
| 1 | `Promise` | Promised date of an open promise covering the invoice | High if the customer's promise kept rate (12 months) is at or above the profile level; Medium otherwise |
| 2 | `Payment plan` | Installment due date | High if the plan is in good standing; Low if an installment is missed |
| 3 | `Terms plus history` | Due date + customer's amount-weighted average days beyond terms, using at least the profile's minimum number of paid invoices | Medium |
| 4 | `Segment history` | Due date (or as-of date if already past due) + segment's average days beyond terms | Low |
| 5 | `Past due, no basis` | Placed in `Beyond week 13` unless the user supplies a rule | Low |

- Customer lag: `Average days beyond terms = sum(Paid amount x max(0, Paid date - Due date)) / sum(Paid amount)` over 12 months.
- An expected date falling before the first week start (an already-past due date plus lag) is moved to week 1 and labelled `Catch-up`.
- Expected receipt amount = invoice open amount less any discount the customer habitually takes (only if history shows it consistently; label it).

## Exclusions (separate columns, never in weekly buckets)

- `Disputed — excluded`: open disputed amounts.
- `At risk — excluded`: accounts referred to agency or counsel, in insolvency, or beyond the profile's at-risk days-past-due threshold.
- `Unapplied cash`: shown as a memo; already received, not a future receipt.

## Summary sheet layout ("Expected receipts")

| Column | Content |
|---|---|
| Entity | Selling entity |
| Currency | Transaction currency |
| Customer or group | Top N customers by open AR named; remainder aggregated as "Other — <segment>" |
| Wk 1 ... Wk 13 | Expected receipts by week |
| Beyond week 13 | Expected after the horizon |
| Disputed — excluded | Amount |
| At risk — excluded | Amount |
| Total open AR | Open AR for the row |
| Check | `Sum of Wk 1..Wk 13 + Beyond + Disputed + At risk - Total open AR`; must be zero |
| Confidence mix | Share of the row's scheduled amount that is High / Medium / Low |

Header block above the table: as-of date, AR cut-off time, entities, week convention, basis hierarchy version, "Basis: Forecast", prepared by and date.

## Detail sheet ("Expected receipts detail")

Invoice, Customer ID, Customer, Entity, Currency, Invoice date, Due date, Open amount, Disputed amount, Expected amount, Expected date, Week, Basis label, Confidence, Promise ID or plan ID, Customer lag (days), Source row.

## Back-test (when prior schedules exist)

`Accuracy for week w = Actual receipts on scheduled invoices in week w / Scheduled amount for week w`. Report the last four weeks to help Treasury weight the schedule; do not adjust the current schedule for it unless the user asks.
