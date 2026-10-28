# Canonical schema and validation checks

## Canonical columns (sheet "Data")

| # | Column | Type | Rule |
|---|---|---|---|
| 1 | record_id | text | Stable key `<source_id>-<source_row>`; unique |
| 2 | source_id | text | Short code per source file, e.g. S01; defined on the Sources sheet |
| 3 | source_file | text | File name as received |
| 4 | source_sheet | text | Sheet or tab name; blank for CSV and bank files |
| 5 | source_row | integer | Row number in the source as opened (1-based, header rows counted) |
| 6 | entity | text | Entity code from the Finance Profile Section 1; unmapped codes kept as received and flagged |
| 7 | account | text | Account number as text, leading zeros preserved |
| 8 | account_name | text | As received; trimmed of padding only |
| 9 | period | text | Fiscal period label per Finance Profile Section 3 (e.g. FY27-P03) |
| 10 | posting_date | date | ISO date; blank for balance-only files |
| 11 | currency | text | ISO 4217 code of the amount column |
| 12 | currency_role | text | Transaction / Functional / Reporting |
| 13 | amount | number | Signed in the canonical convention (debit positive, credit negative) at full source precision |
| 14 | amount_type | text | Closing balance / Opening balance / Activity / Budget / Forecast |
| 15 | basis | text | Actual / Budget / Forecast / Prior year / Pro forma |
| 16 | description | text | Line or journal description as received |
| 17 | document_ref | text | Journal, invoice, statement or transaction reference |
| 18 | counterparty | text | Customer, supplier, bank or intercompany entity code; bank account numbers masked to last 4 |
| 19 | dimension_1..n | text | Cost centre, segment, product etc., one column each, named on the About sheet |
| 20 | transform_note | text | Every change applied to this row (sign flipped, scaled from thousands, date reparsed, entity mapped) |
| 21 | ingest_status | text | Clean / Fixed / Flagged / Excluded |

## Row status definitions

- **Clean** — read without any transformation beyond type conversion.
- **Fixed** — a deterministic, documented transformation was applied (sign convention, scale, date format, code mapping from the user's mapping file). The transform_note says exactly what.
- **Flagged** — retained in Data but needs a decision (probable duplicate, unmapped entity or account, ambiguous date, currency missing).
- **Excluded** — not a data row (subtotal, page header, footer total, blank, repeated header). Kept on the Exceptions sheet, never in Data, so totals are not double counted.

## Number parsing rules

| Source form | Interpretation |
|---|---|
| `(1,234.56)` | -1234.56 |
| `1,234.56-` (trailing minus) | -1234.56 |
| `1.234,56` with comma decimal locale | 1234.56 — only when the file's locale or a consistent pattern across the column confirms it; otherwise Flagged |
| `1 234,56` (space grouping) | 1234.56 under the same locale rule |
| Separate Debit and Credit columns | amount = Debit - Credit |
| `DR` / `CR` indicator column | DR keeps sign positive; CR makes it negative |
| Scaled header ("in thousands", "000s") | multiply by 1,000 and note it; never scale without a header or user statement |
| Text such as `-`, `n/a`, blank | null, not zero; counted in the Coverage sheet |

## Date parsing rules

- Determine day-month order per file from values that disambiguate (a day above 12). If every date in a file is ambiguous (day <= 12 throughout) and no locale is stated, Flag the file and ask; do not guess.
- Serial dates from spreadsheets are converted using the workbook's date system (1900 or 1904).
- Period assignment uses the Finance Profile fiscal calendar, not calendar months, when the pattern is week-based.

## File-level checks

| Code | Check | Rule | Result label |
|---|---|---|---|
| C1 | Control total | Sum of data rows (before sign normalization, in source sign) equals the source footer or report total for each amount column; difference computed in code | Agrees / Difference |
| C2 | Record count | Data rows + excluded non-data rows = total rows read; equals source stated count where the footer gives one | Agrees / Difference |
| C3 | Trial balance balances | Sum of closing balances = 0 per entity and period (after sign normalization) | Balances / Out of balance |
| C4 | Roll-forward | Opening + activity = closing per account where all three are present | Agrees / Difference |
| C5 | Period coverage | Every expected period in the requested range is present per entity | Complete / Missing periods |
| C6 | Entity coverage | Every in-scope entity in Finance Profile Section 1 (or the user's list) has rows | Complete / Missing entities |
| C7 | Currency coverage | Each entity's functional currency is present; unexpected currencies listed | Complete / Missing / Unexpected |
| C8 | Exact duplicates | Same entity, account, period, date, amount, currency, document_ref and description | Count, all Flagged |
| C9 | Probable duplicates | Same entity, account, amount, currency and date within 3 days but different reference; or the same file loaded twice (identical control totals and row counts) | Count, all Flagged |
| C10 | Sign convention | Natural-balance test: share of asset and expense accounts with credit balances, and liability, equity and revenue accounts with debit balances, using Finance Profile account ranges. Above 50% of a class reversed suggests an inverted file; confirm with the user before flipping | Consistent / Suspected inversion |
| C11 | Bank file continuity | Opening balance of each statement = closing balance of the prior statement for the same account; statement sequence numbers have no gaps | Continuous / Break |
| C12 | Mapping completeness | Every account maps to a reporting line in the user's mapping file | Complete / Unmapped accounts |

A Difference on C1 or C2 means the file is not complete as read. Report the file as Incomplete and do not present its totals as final until the user resolves it.

## Bank file notes

- Common structures include fixed-width statement formats, tagged SWIFT statement messages, ISO 20022 XML statements and portal CSV exports. Read balances (opening, closing, available) and transaction lines separately; never mix balance rows into activity.
- Keep value date and booking date as separate columns where both exist.
- Mask account identifiers to last 4 in every output column.
