# Calendar columns, date logic and status vocabulary

## Calendar sheet columns

| Column | Content | Rule |
|---|---|---|
| Obligation ID | `<Entity>-<Jurisdiction>-<TaxType>-<Form>-<PeriodEnd>` | Unique key used to compare versions |
| Entity | Legal entity name from the Finance Profile | Must exist in the profile entity list |
| Jurisdiction | Country, state, province or local authority | Spell as the authority does |
| Tax type | Income / Estimated or installment / VAT / GST / Sales and use / Payroll / Withholding / Information return / Other (state) | One per row |
| Return or payment | Return name or payment description as the authority labels it | Filing and payment are separate rows when their dates differ |
| Period start, Period end | Dates of the reporting period | From the registration frequency and fiscal calendar |
| Frequency | Monthly / Quarterly / Semiannual / Annual / Other (as assigned) | Cite the registration letter or matrix |
| Rule ID | Key into Rule Sources | Mandatory for any dated row |
| Statutory due date | Computed from the cited rule | `Not provided` if no rule |
| Extension evidenced | Yes (evidence ref) / No / Not applicable | Yes only with a filed copy or acknowledgement |
| Extended due date | Computed from the cited extension rule | Blank unless Extension evidenced = Yes |
| Payment due date | Computed from the cited payment rule | Never moved by a filing extension unless the rule says so |
| Internal due date | Applicable due date minus lead days | Lead days from profile or user |
| Preparer, Reviewer, Signatory | Name and role | Flag blanks and Preparer = Reviewer |
| Status | See vocabulary below | Set from evidence |
| Evidence reference | Acknowledgement number, filed-copy location, payment confirmation | Required for Filed, Paid, Filed and paid |
| Days to due | Applicable due date minus as-of date | Negative values shown in parentheses |
| Notes | Free text | Assumptions labelled as such |

Applicable due date = Extended due date when present, otherwise Statutory due date (for filing rows); Payment due date for payment rows.

## Date computation patterns

- Offset from period end: `due = EOMONTH(period end, months) + days` or `period end + days`, exactly as the cited rule words it.
- Fixed day of following period: `due = DATE(year, month of period end + n, fixed day)`.
- Date stated by the authority (for example on an annual filing notice): use the stated date, cite the notice.
- Weekend or holiday roll-forward: apply `WORKDAY(due − 1, 1, holidays)` only when the cited rule provides roll-forward; holidays from the profile calendar or the cited source.
- If a rule is ambiguous (for example "the last working day" without a holiday list), compute the plain reading, label the row `Assumption — review`, and list the question.

## Status vocabulary

| Status | Applies when |
|---|---|
| Rule needed | No cited rule exists for the row; due date is `Not provided` |
| Not started | Rule cited; no preparation evidence; internal due date not passed |
| In preparation | Preparer has started (draft workpaper or tracker update) |
| In review | Draft sent to the reviewer |
| Ready to file | Reviewer sign-off evidenced |
| Filed — evidence pending | User states it is filed; no acknowledgement yet |
| Filed | Acknowledgement, confirmation number or filed copy referenced |
| Paid | Payment confirmation referenced (payment rows) |
| Filed and paid | Both evidenced where filing and payment share one row |
| Extended | Extension evidenced; extended due date not passed |
| At risk | Internal due date passed and status earlier than In review |
| Overdue | As-of date after applicable due date with no filing or payment evidence |
| Not required | Evidence that the period needs no return (for example a deregistration letter or authority confirmation) |

## Verification checklist

1. Row count equals registrations x periods in horizon, differences explained.
2. Every dated row has a Rule ID that resolves to Rule Sources with citation and retrieval date or document reference.
3. No Filed, Paid or Filed and paid status without an evidence reference.
4. Every row has preparer and reviewer, or is flagged.
5. Change Log explains every removed obligation with evidence.
