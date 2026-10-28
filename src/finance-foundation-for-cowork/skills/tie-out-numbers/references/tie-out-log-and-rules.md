# Tie-out log specification and comparison rules

## Figure inventory — what counts as a figure

Capture every numeric expression a reader could rely on:

- amounts, percentages, ratios, multiples, basis points, per-share figures, headcount, units, days (DSO, DPO), counts;
- figures in body text, tables, charts (data labels and axis-implied values where labelled), footnotes, headers, call-outs and speaker notes;
- dates and periods only when they assert a fact that can be checked (e.g. "repaid on 2026-06-30");
- words that express numbers ("doubled", "a third", "flat", "record high") — logged as Qualitative claims and tested against the source arithmetic.

Excluded from the inventory: page numbers, section numbers, clause numbers, years used only as labels, and phone numbers. Record exclusions by category in the About sheet, not line by line.

## Figure classes

| Class | Meaning | How tested |
|---|---|---|
| Source | Should equal a value in a source (cell, ledger balance, schedule line) | Compare to source value after unit and rounding conversion |
| Derived | Calculated from other figures (total, change, growth %, margin, ratio, mix share) | Recompute in code from the source values (not from the rounded presented values) and compare |
| Repeated | Same figure appearing more than once in the document | Each occurrence must agree with the first traced occurrence and with source |
| Qualitative | Numeric words or directional claims | Test direction and magnitude against the computed values |
| Non-financial | Operational data (headcount, stores, units) | Traced like Source if a source is supplied; otherwise Unsupported |

## Comparison rules

1. Convert the source value to the presentation basis: same currency, same units (divide by 1,000 or 1,000,000), same sign presentation (parentheses or minus), same period and basis (Actual, Budget, Forecast, Pro forma).
2. Round the converted source value to the number of decimals shown in the document using round-half-away-from-zero, unless the document states another rounding convention.
3. `difference = presented value - rounded source value` (in presentation units). For percentages, the difference is in percentage points.
4. Status:
   - **Agrees** — difference = 0 after rounding.
   - **Within threshold** — difference is non-zero but |difference| <= the tie-out tolerance (Finance Profile Section 6, TIE-01, or the user's stated tolerance). Typical cause is rounding of components that do not add to a rounded total. The cause is stated.
   - **Difference** — |difference| > tolerance, or the sign, period, entity, basis or unit is wrong even if the digits match (e.g. a Budget number presented as Actual).
   - **Unsupported** — no source was supplied or found, the source cell is blank or unreadable, or the figure is a forward-looking statement without a supplied forecast source.
   - **Not in scope** — figures the user explicitly excluded (for example, market data). Listed so coverage is visible.
5. If no tolerance is given or recorded, any non-zero difference is a Difference; the skill never assumes a tolerance.
6. Derived figures: recompute from unrounded source values. If the recomputed derived figure agrees but the presented components do not add to the presented total because of rounding, mark Within threshold only if inside tolerance, and note "rounding — components presented do not foot".

## Tie-out log columns (sheet "Tie-out Log")

| Column | Content |
|---|---|
| Ref | T-001, T-002 ... in document order |
| Location | Page or slide number, section heading, table and row/column, or paragraph |
| Presented text | Exact text as it appears, e.g. "$12.4m" |
| Presented value | Numeric value in presentation units |
| Units and currency | e.g. USD millions |
| Period / as-of | e.g. FY27 Q2, as of 2026-06-30 |
| Entity / scope | e.g. Contoso Group consolidated |
| Basis | Actual / Budget / Forecast / Prior year / Pro forma |
| Class | Source / Derived / Repeated / Qualitative / Non-financial |
| Source reference | File + sheet + cell or range; or ledger account + entity + period; or schedule + line; or document + page/section |
| Source value | Unrounded source value in source units |
| Converted source value | In presentation units, before rounding |
| Recomputed value | For Derived figures, the code-computed result and its formula in plain notation |
| Difference | Presented minus rounded source or recomputed, in presentation units |
| Tolerance applied | Value and source (TIE-01 or user-stated) |
| Status | Agrees / Within threshold / Difference / Unsupported / Not in scope |
| Tickmark | See legend |
| Comment | Cause of any difference, what is needed to support an Unsupported figure |

## Tickmark legend

| Tickmark | Meaning |
|---|---|
| A | Agreed to source without exception |
| R | Recomputed (derived figure) and agrees |
| W | Within threshold — rounding or tolerance difference explained |
| X | Difference — see Comment |
| U | Unsupported — no source evidence |
| C | Agrees to another occurrence in the same document (cross-reference) |
| N | Not in scope |

Each mark in the ticked-and-referenced view is printed as `[T-014 A]` next to the figure, so a reviewer can find the log row from the document and vice versa.

## Summary metrics (sheet "Summary")

- Figures inventoried; count and percent by status (percent to 1 dp; percentages sum to 100.0%).
- Differences ranked by absolute amount in presentation units.
- Unsupported figures grouped by missing source.
- Coverage — pages or slides reviewed versus total; sources used versus sources referenced in the document.
