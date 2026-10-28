# Tracker fields, status rules and defaults

## 1. Tracker columns

Finding ID; Source (deficiency evaluation, internal audit report, external auditor letter, regulator, self-identified) with reference and date; Finding summary; Classification as recorded by management (Deficiency / Significant deficiency / Material weakness / Audit finding rating as issued) or `Not provided`; Control ID; Accounts and assertions; Process; Root cause; Action plan summary; Owner (name, role); Executive sponsor; Original due date; Current due date; Revision count; Revision approvals (approver, date); Lifecycle status; Timeline flag; Evidence label; Days overdue; Slippage days; Implementation date; Occurrences since implementation; Minimum occurrences; Earliest retest date; Projected retest completion; Retest workpaper reference and result; Closure approver and date; Last update (date, source); Notes.

## 2. Milestones sheet

Finding ID; Milestone (Design change / Implementation / Operating period / Retest / Closure); Planned date; Actual date; Evidence reference; Status (Not started / Complete — evidence verified / Complete — evidence not provided / Overdue).

## 3. Lifecycle status rules (first rule that applies, top to bottom)

| Status | Rule |
|---|---|
| Closed | Closure approver and date recorded from evidence |
| Retest failed — reopened | Latest retest workpaper shows exceptions or a reviewer conclusion of not effective |
| Retest passed — awaiting closure approval | Retest workpaper shows no exceptions and the reviewer has concluded; no closure approval yet |
| Ready for retest | Implementation evidence verified and occurrences since implementation at or above the minimum |
| Implemented — operating period running | Implementation evidence verified and occurrences below the minimum |
| In progress | At least one milestone complete or a dated update shows work under way |
| Not started | None of the above |

## 4. Timeline flag rules (first rule that applies)

| Flag | Rule |
|---|---|
| Not demonstrable by assessment date | Classification is Material weakness or Significant deficiency (or the user extends the rule to all) and projected retest completion is after the assessment date, or no projection is possible because the operating period cannot complete in time |
| Overdue | As-of date after current due date and the item is not yet Implemented or later |
| At risk | Current due date within the at-risk window with milestones outstanding; or a milestone is overdue; or projected retest completion is later than assessment date minus the at-risk window |
| On track | None of the above |

Formulas: `Days overdue = MAX(0, as-of date - current due date)`; `Slippage days = current due date - original due date`; `Buffer days = assessment date - projected retest completion`.

## 5. Evidence labels

Evidence verified; Evidence not sufficient — reason; Owner reports complete — evidence not provided; Conflict — confirm with owner.

## 6. Minimum operating occurrences before retest (commonly used default; user must confirm)

Offered only when the methodology is silent. Label "Default — confirm" until accepted; until then the readiness columns show `Not provided`.

| Control frequency | Minimum occurrences before retest |
|---|---|
| Annual | 1 (must occur before the assessment date) |
| Quarterly | 2 |
| Monthly | 2 |
| Weekly | 5 |
| Daily | 20 |
| Multiple times per day | 25 |
| Automated | 1, after change management evidence for the change |

Occurrences are counted from evidence of actual performance where available; otherwise they are projected from frequency and the fiscal calendar and labeled Projected.

## 7. Leadership summary layout

1. Headline — one sentence with closing open count and the number not demonstrable by the assessment date.
2. Status by classification — table of lifecycle status by classification (counts).
3. Material weakness and significant deficiency path — per item: implementation date, earliest retest, projected completion, buffer days.
4. Overdue and at risk — item, owner role, days overdue or reason at risk, next milestone.
5. Decisions and support needed — items revised twice or more, resourcing or scope decisions.
6. Sources — tracker version, as-of date, evidence folders read.
