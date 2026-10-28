# Workday convention, status definitions and critical path rules

## 1. Workday convention

- A **business day** is a weekday that is not a holiday in the entity's holiday calendar (Finance Profile or the user's close checklist). Entity-specific calendars apply per entity; a group milestone uses the group calendar stated by the user.
- **WD-1** is the last business day on or before the period-end date. WD-2 is the business day before WD-1, and so on.
- **WD+1** is the first business day after the period-end date. WD+2 is the next business day, and so on.
- There is **no WD0**. If a checklist uses WD0, ask the user once whether it means WD-1 or WD+1 and record the answer in Sources & Assumptions.
- A due time, if the checklist gives one (for example "WD+2 12:00"), is in the entity's local time zone. Without a time, a task is due by the end of the due business day.
- Calendar-day items (for example "bank statements received by the 3rd") are kept as calendar dates, not converted.

## 2. Status definitions

Apply the first label in this precedence list whose condition is met.

| Precedence | Status | Condition |
|---|---|---|
| 1 | Not applicable this period | Task frequency does not apply to this period (quarterly task in a non-quarter month, year-end task before year end), or the user excludes it. |
| 2 | Complete | Tracker shows complete (or reviewer sign-off recorded) with a completion date on or before the due date. |
| 3 | Complete - late | Tracker shows complete with a completion date after the due date. Days late is shown. |
| 4 | Blocked | Not complete, and either a predecessor is not complete, or the owner has reported a blocker (missing input, system outage, awaiting approval) in the tracker, Teams or mail. |
| 5 | Reported complete, not confirmed | Tracker does not show complete, but the owner or reviewer stated completion in Teams or mail. |
| 6 | Overdue | Not complete and the due date (and time, if given) has passed. |
| 7 | At risk | Not yet due, and forecast finish is later than the due date, or slack is zero or negative, or the owner flagged a risk. |
| 8 | In progress | Not yet due, with evidence of activity (tracker status, partial upload, message). |
| 9 | Not started | Not yet due and no evidence of activity. |

Notes:
- A blocked task that is also past due keeps `Blocked` and shows days late, so the blocker is visible.
- Percentage complete = (Complete + Complete - late) / (all tasks minus Not applicable this period), shown to 1 dp.
- Days late = business days from the due date (exclusive) to the completion date or today (inclusive).

## 3. Critical path

Inputs per task: duration D in business days (default 1 if the checklist gives none, labelled as an assumption), predecessors, due date, and actual completion date if complete.

1. **Forward pass.** For each task in dependency order:
   - Earliest start = the business day after the latest forecast finish among predecessors, or the task's planned start if later.
   - Forecast finish = actual completion date if complete; otherwise earliest start plus D minus 1 business days, but never earlier than today if the task is open and overdue.
2. **Backward pass.** From the final milestone (its due date is its latest permissible finish), for each predecessor: latest permissible finish = the minimum over its successors of (successor latest permissible finish minus successor D business days). A task's own due date also caps its latest permissible finish.
3. **Slack** = latest permissible finish minus forecast finish, counted in business days.
4. **Critical path** = the chain of tasks with slack of zero or less leading into the final milestone. Negative slack on the milestone means the close date is forecast to be missed by that many business days.
5. **Cycles.** If dependencies form a loop, stop, list the tasks in the loop, and ask the tracker owner to correct them; do not compute slack for those tasks.

## 4. Daily status note structure

1. Headline - workday, date, percentage complete, milestone on track or at risk (with days).
2. Critical path - tasks with slack of zero or less, owner, forecast finish.
3. Overdue and blocked - task, entity, owner, days late, blocker, evidence.
4. Help or decisions needed - who needs to act and by when.
5. Completed since last note.
6. Due next business day.
7. Data gaps - unread sources, unowned tasks, conflicts between tracker and messages.
