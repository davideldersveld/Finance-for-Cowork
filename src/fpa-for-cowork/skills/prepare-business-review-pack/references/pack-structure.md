# Business review pack structure, slide rules and figure register

## Default section templates

| # | Section | Content | Typical source analysis |
|---|---|---|---|
| 1 | Cover | Review name, period, entity scope, version, Draft status, as-of date, preparer | User |
| 2 | Headline results | 3-5 figures: revenue, gross margin %, EBITDA, operating cash flow, one KPI; each vs plan and prior year | Variance workbook, scorecard |
| 3 | Performance vs plan | Summary variance table (Actual, Plan, Variance, %), one bridge chart, flagged variances with drivers | Variance workbook, bridge |
| 4 | KPI scorecard | KPI, Actual, Target, RAG, Trend, Owner | KPI scorecard |
| 5 | Outlook | Full-year forecast vs budget, change since last forecast, scenario range if supplied | Forecast, scenarios |
| 6 | Findings | Finding, figure IDs, label (Evidenced / Hypothesis), owner | All analyses |
| 7 | Risks and opportunities | Item, quantification (Verified only) or "Not quantified", owner, label, next step | Analyses, user |
| 8 | Decisions requested | Decision, options, recommendation only if the user supplied one, owner, date needed | User |
| 9 | Appendix | Detail tables, Sources and assumptions, figure register, glossary of KPI definitions | All |

QBR variant: add a quarter-to-date and year-to-date view in section 3 and a strategic initiative status table in section 5 if supplied.

## Slide rules (PowerPoint)

- One message per slide; the title is a full-sentence takeaway that uses register figures (for example "Q3 revenue 2.6% below budget as volume shortfall outweighed price").
- Body: one chart or table plus up to four bullets.
- Footer on every content slide: period, entity, currency and units, basis, source file names.
- Evidence labels appear next to each finding: [Evidenced] or [Hypothesis].
- Slide limit as the user states; overflow goes to the appendix, never to smaller fonts.

## Document rules (Word)

- Headings match the section list; numbered tables and figures with captions stating period, units and source.
- One-paragraph section summaries, then tables.
- Appendix holds the figure register.

## Figure register columns

| Column | Content |
|---|---|
| ID | F-001 ... |
| Figure | Plain description |
| Value | As shown in the pack (with rounding rule) |
| Unrounded value | From source |
| Unit | For example USD millions, % |
| Period | For example Q3 FY2026 |
| Entity | Scope |
| Basis | Actual / Budget / Forecast / Pro forma |
| Source | File, sheet, cell or range |
| Formula | For Derived figures only, referencing other IDs |
| Status | Verified / Derived / Conflict / Unverified |
| Used on | Slide or section numbers |

## Consistency checklist

1. Same ID, same value on every slide or section.
2. Rounding rule stated (for example one decimal in millions); tables that do not foot after rounding carry a note.
3. Every percentage recomputes from its register components.
4. Period labels, units and basis agree with the source.
5. No figure in the pack lacks a register ID.
6. Conflicts and Unverified items appear in the chat summary and on the affected page.
