# Spreadsheet model finding catalog

Each finding uses one code from this catalog. Severity is set by the rule shown, then raised one level if the affected cell feeds a reported output (a cell on an output, summary or dashboard sheet, or a cell another document links to).

## Detection definitions

| Code | Finding | Detection rule | Default severity |
|---|---|---|---|
| F01 | Hardcoded number in formula row | A constant in a row or column where most cells (at least 3 neighbours, and the majority) hold formulas | High |
| F02 | Embedded constant in formula | A literal number inside a formula other than 0, 1, -1, 12, 100, 1000, 365 or an explicit unit conversion, e.g. `=B5*1.07`; the number is listed | Medium |
| F03 | Inconsistent formula | Formula in relative (R1C1) form differs from the dominant pattern of its row or column block; first and last cells of each pattern break are listed | High |
| F04 | Broken reference | `#REF!` in a formula, or a defined name pointing to `#REF!` | High |
| F05 | Error value | Cell evaluates to `#DIV/0!`, `#N/A`, `#VALUE!`, `#NAME?`, `#NUM!`, `#NULL!`, `#SPILL!`; error masking with IFERROR around a reference that is actually broken is listed as well | Medium (High if it feeds an output) |
| F06 | External link | Formula or defined name referencing another workbook; source path, whether it is reachable, and last cached value recorded | Medium |
| F07 | Circular reference | Cells in a dependency cycle; note whether iterative calculation is enabled and whether the cycle is intentional and documented (e.g. interest on average cash) | High if undocumented; Low if documented |
| F08 | Total does not foot | A subtotal or total cell differs from the recomputed sum of its components (difference computed in code) | High |
| F09 | Total does not cross-foot | Row totals summed differ from column totals summed for the same block | High |
| F10 | Incomplete range | SUM or similar range omits adjacent rows or columns of the same block (e.g. `=SUM(C5:C19)` with data in C20) | High |
| F11 | Double count | A total includes both components and their subtotal | High |
| F12 | Hidden rows or columns | Hidden rows or columns containing values or formulas; whether they feed outputs | Medium |
| F13 | Hidden or very hidden sheet | Sheet hidden or set to very hidden; content summary and whether outputs depend on it | Medium |
| F14 | Unlabelled units, period or currency | A numeric block without a visible label for units (units, thousands, millions), period (month, quarter, year, as-of date) or currency | Medium |
| F15 | Input, calculation and output mixed | Hardcoded inputs on calculation or output sheets; inputs not visually distinguished; outputs computed on input sheets | Medium |
| F16 | Unit or sign inconsistency | A formula combines cells labelled in different units (thousands with units) or adds a cost shown as negative to a cost shown as positive | High |
| F17 | Volatile or fragile functions | INDIRECT, OFFSET, whole-column references in large models, hard-coded sheet names in text, TODAY/NOW driving period logic | Low |
| F18 | Lookup risk | Approximate-match lookups on unsorted data; lookups returning the first of duplicate keys; lookup ranges not covering the key list | Medium |
| F19 | Defined name issues | Names unused, duplicated across scopes, or pointing to constants that act as hidden inputs | Low |
| F20 | Number stored as text | Numeric-looking text in a calculation range, excluded from sums | Medium |
| F21 | Macros or automation present | Macro code or automation in the file; listed, never run | Info |
| F22 | Protection and structure | Locked sheets or cells that prevent review; noted as a coverage limit | Info |
| F23 | Formatting masks values | Custom formats that hide values (e.g. `;;;`), white font on white fill, or rounding formats that hide significant decimals in check cells | Medium |
| F24 | Check cells failing | The model's own check cells (balance checks, "should be zero" cells) not equal to zero | High |

## Severity definitions

- **High** — can change a reported number or conclusion now.
- **Medium** — creates a material risk of error when the model is updated or reused, or obscures review.
- **Low** — good-practice deviation with low likelihood of error.
- **Info** — context for the reviewer; no error indicated.

## Finding status

- **Confirmed** — the rule is met and the effect is demonstrated (e.g. the foot difference is computed and non-zero).
- **Probable** — the rule is met but intent cannot be determined from the workbook (e.g. a hardcode that may be a deliberate override). Owner confirmation needed.
- **For review** — a judgement area the reviewer should look at (e.g. a documented circularity, a high-risk lookup that currently returns correct values).

## Quantifying impact

Where a finding affects a number, compute the impact in code and report it in the model's own units:

- F01 or F02 — impact = hardcoded value minus the value the row's dominant formula would produce in that cell.
- F03 — impact = current value minus the value the dominant pattern would produce.
- F08, F09, F10, F11 — impact = presented total minus recomputed total.
- F16 — impact = current result minus the result with consistent units or signs.

Impacts are illustrations of the effect of the finding, never corrections to the model.

## Formula map

For each sheet: used range, cells with constants, cells with formulas, distinct formula patterns (R1C1), error cells, external references, hidden rows and columns, and a role label — Input, Calculation, Output, Mixed, or Documentation.
