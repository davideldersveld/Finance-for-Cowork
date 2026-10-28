# Renewal types and date rules

## Renewal types

| Type | Meaning | Dates to compute |
|---|---|---|
| Fixed term, no renewal | Ends on the term end date; continuing requires a new contract | Term end; recommended decision date = term end - sourcing lead time |
| Auto-renewal, fixed renewal term | Renews for a stated period unless notice is given | Notice deadline each cycle; next term end if missed |
| Evergreen or rolling | Continues indefinitely until terminated on notice | Earliest termination date = as-of date + notice period; flag as no natural decision point |
| Buyer option to extend | Buyer may extend by exercising an option by a date | Option exercise deadline; options remaining |
| Mutual renewal by agreement | Renews only if both parties sign | Term end; decision date ahead of term end |
| Termination for convenience | Either or one party may terminate on notice at any time | Earliest effective termination date; note any termination fee |

Record "Renewals remaining" where the contract limits the number of renewals or options.

## Date arithmetic rules

| Situation | Rule |
|---|---|
| Notice in calendar days | Deadline = term end - N days |
| Notice in months | Deadline = same day-of-month N months before term end; if that day does not exist, use the last day of that month and label the adjustment |
| Notice in business days | Count back N business days using the user's business-day calendar from the profile |
| "At least N days before" | Deadline is the last date on which notice still leaves N full days; the computed deadline above is the latest acceptable date |
| Notice must be received | Subtract delivery time for the method (for example courier days) from the deadline; state the assumption |
| Deadline on weekend or holiday | If the contract is silent, move to the previous business day and label it |
| Term end not stated but term length stated | Term end = start date + term length - 1 day; label computed |
| Amendment changes term | Use the latest amendment's date; if an amendment is referenced but missing, mark the date unverified |

All date arithmetic is performed in code. Show the formula inputs in the calendar so a reviewer can recompute.

## Decision lead time table (from the user's profile)

Columns: Value band or sourcing route | Lead time (days) | Source (profile section or user statement). Populate rows only from the profile or the user; a longer lead time normally applies where the route is a formal tender, because the tender itself must finish before the notice deadline.

If the profile has no lead-time table, ask the user once; do not substitute a default.

## Status precedence

Apply the first status that matches, in this order: Notice served, Renewed, Expired, Data incomplete, Notice deadline missed - locked in, Decision overdue, Decision due, Upcoming, Not in window.

## Alert draft content

Subject: Renewal decision needed — [Supplier] [Contract title] — notice by [deadline]

Body: contract reference; current term end; renewal type; notice deadline and method; recommended decision date; annual value with basis; open register mismatches or gaps; decision options to consider (renew, renegotiate, retender, terminate) with the skill that supports each; request to confirm the decision and owner.
