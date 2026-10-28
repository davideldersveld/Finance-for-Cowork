# PBC tracker specification

## PBC_Tracker columns

| Column | Rule |
|---|---|
| Request ID | Auditor's ID, unchanged; never renumber |
| Area | Statement caption or process (Cash, Revenue, Inventory, Payroll, Tax, IT general controls, Legal and commitments) |
| Description | Auditor's wording, shortened only if over 200 characters |
| Phase | Planning, Interim, Year-end, Completion |
| Requested | Date the auditor issued the request |
| Due | Agreed due date; blank becomes "Due date needed" |
| Owner | From the profile's area map or the user; otherwise "Owner needed" |
| Reviewer | Internal reviewer before release, where required |
| Status | Not started, In progress, Ready for review, Provided, Accepted, Returned - follow-up, Not applicable - agreed |
| Status evidence | Citation: email date and sender role, portal record, file in evidence folder |
| Business days to due | Formula from as-of date using the profile's business-day calendar; negative when overdue |
| Flag | Late, At risk, On track (formula) |
| Date provided | Date of release evidence |
| Auditor query date | For Returned - follow-up |
| Query age | Business days since query date while unresolved |
| Evidence IDs | Links to Evidence_Index |
| Notes | Conflicts, dependencies, owner estimates (labelled) |

## Flag formula logic

```
IF status in (Provided, Accepted, Not applicable - agreed) -> On track (closed)
ELSE IF due < as_of -> Late
ELSE IF business_days_to_due <= warning_window AND (status = Not started OR dependency incomplete) -> At risk
ELSE -> On track
```

The warning window (in business days) comes from the Finance Profile or the user.

## Evidence release checklist

Before an item moves to Provided:

1. Correct entity and period in the file and file name.
2. Preparer and reviewer recorded; review evidenced (sign-off, comment, or approval record).
3. For reports from systems (information produced by the entity): report name, run date, parameters and record count captured; completeness check against the ledger total where possible.
4. Amounts that represent ledger balances agree to the trial balance in code; difference recorded.
5. Personal data limited to what the request requires; bank accounts masked to last four digits unless the auditor requires full details through the secure channel.
6. File naming: `<RequestID>_<Area>_<ShortDescription>_<Period>_v<n>` or the user's convention.
7. Released only through the agreed channel and only on the user's instruction.

## Adjustments_Log and SUM

| Column | Rule |
|---|---|
| ID | Auditor's reference |
| Description | Nature of the misstatement |
| Account / Debit / Credit | Each line; the entry must balance |
| Pre-tax income effect | Positive = increases income |
| Assets, Liabilities, Equity effect | Signed |
| Classification | Factual, Judgemental, Projected (per the auditor) |
| Management response | Agree - to book, Disagree - support provided, Under review |
| Status | Open, Booked (journal reference), Waived - uncorrected |

**Summary of uncorrected misstatements (SUM).**

- Rollover view: sum of current-period income statement effects of uncorrected items, including the reversal effect of prior-period uncorrected items that turned around in the current period (as supplied by the user or auditor).
- Iron curtain view: cumulative misstatement in balance sheet captions at period end, including prior-period uncorrected items not yet reversed.
- Present each view by caption: pre-tax income, total assets, total liabilities, equity, and key subtotals the user designates.
- `Percentage of materiality = absolute effect / materiality figure recorded by the user`. Present the percentage only; the evaluation belongs to management and the auditor.
- Tax effect is shown only if the user supplies the rate to apply.

## Status note structure

1. Headline: percent complete (Accepted plus Provided over total) and days to next milestone.
2. Late items: ID, area, owner, days late.
3. At-risk items: ID, area, owner, due date, blocker.
4. Auditor queries older than the warning window.
5. Adjustments: count and totals by management response; SUM totals.
6. Decisions needed from the controller.
7. Next milestones from the audit timetable.
