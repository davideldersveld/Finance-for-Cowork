# Test catalogue

Each test applies only where its precondition holds; otherwise the line shows `N/A` for that test. Every rule value used (rate, format pattern, required field, certificate validity) carries a Rule ID that resolves to a cited user document or an authoritative source with retrieval date.

| Test | Precondition | Pass condition | Fail examples | Exposure formula |
|---|---|---|---|---|
| T1 Tax code | Matrix row exists for the line's keys | Line tax code = matrix expected code | Standard-rated code on a zero-rated export; exempt code on a taxable product | Via T2 |
| T2 Rate | Cited rate exists for code and jurisdiction | `abs(Tax − Net x Rate) <= line tolerance` | Superseded rate still in the system; rate for wrong jurisdiction | `Expected tax − Tax charged` (sales); `Tax claimed − Recoverable tax` (purchases) |
| T3 Registration number | Treatment requires a counterparty or own registration number (for example B2B reverse charge or zero-rated cross-border supply, as the cited rule states) | Number present and matches the cited format pattern for its country or jurisdiction | Missing customer number on a zero-rated supply; pattern mismatch | If the relief fails, `Net x Cited rate` shown as potential exposure, labelled Hypothesis until reviewed |
| T4 Reverse charge | Matrix treatment is reverse charge or self-assessment | Supplier tax = 0 and recipient output and input entries both present; input limited to recovery position | Supplier charged tax; only input side recorded; neither side recorded | Missing output side: `Net x Cited rate`; tax wrongly charged by supplier: amount charged (recovery at risk) |
| T5 Exemption certificate | Line relies on a customer exemption | Certificate on file, legal name matches, jurisdiction and product category covered, signed, `Issue date <= Transaction date <= Expiry date` | Expired; wrong state; blanket certificate not covering the category; unsigned | `Net x Cited rate` |
| T6 Invoice content | Cited checklist exists for the jurisdiction and invoice type | Every mandatory field present | Missing sequential number; tax amount not shown in required currency; missing reverse-charge wording | None quantified; status Exception with field list |
| T7 Jurisdiction sourcing | Ship-to or place-of-supply evidence available | Coded jurisdiction = evidenced jurisdiction | City tax coded where address is outside city limits; country of supply wrong for services | `Net x (Correct cited rate − Applied rate)` |
| T8 Consistency and duplicates | Population has repeated counterparty-product pairs or document numbers | Same keys receive the same treatment; document numbers unique | Same SKU taxed for one customer and exempt for another without certificate; duplicate invoice numbers | Exposure from the failing line's other tests |

## Line status precedence

1. `Rule not provided` if any applicable test lacks a cited rule.
2. `Exception` if any test fails on available evidence.
3. `Needs information` if a test cannot run for missing evidence (no certificate copy, no address, no invoice image).
4. `Pass` otherwise.

A line can carry several failed tests; exposure is counted once per line using the largest applicable formula to avoid double counting, and the Exceptions sheet lists every failed test.

## Registration number format checks

- Strip spaces, dots and hyphens before testing; keep the original in the evidence column.
- Test length, character classes, country prefix and any check-digit rule only as the cited source defines them.
- Record the result as `Format valid`, `Format invalid` or `Format rule not provided`. Never record `Registered` from a format test alone.

## Root-cause grouping

Group exceptions by (Test, Tax code, Matrix key, Counterparty) and sort groups by exposure, then line count. Groups that share one matrix key across several counterparties point to a potential systemic cause for the matrix owner; single-line groups are listed as one-off errors. Apply any cut-off for "systemic" only when the user or the Finance Profile supplies it.
