# Ambiguity log method

A definition is ambiguous when its words reasonably support more than one calculation. The skill records and quantifies each reading; it never chooses between them.

## Common sources of ambiguity

- Cap base: whether a percentage cap is measured on EBITDA before or after the add-backs being capped, or before or after pro forma adjustments.
- "Non-recurring", "unusual" or "extraordinary" items with no further definition.
- Indebtedness scope: earn-outs, deferred purchase price, finance or operating leases under frozen GAAP, letters of credit (drawn versus undrawn), guarantees, hedging liabilities.
- Unrestricted cash: cash in non-guarantor or foreign subsidiaries, cash subject to control agreements, cash netting caps.
- Test-period construction after acquisitions or disposals (pro forma rules and their timing).
- Accounting-change clauses (frozen GAAP) and whether the company elected to freeze.
- Interaction between amendments where a later amendment changes a defined term used elsewhere.

## Log columns

| Column | Content |
|---|---|
| ID | A1, A2, ... |
| Defined term and section | For example "Consolidated EBITDA, section 1.01, clause (b)(vii)" |
| Clause extract | Short quotation (one or two sentences) sufficient to show the issue |
| Issue | One sentence describing what is unclear |
| Reading A / Reading B (and further) | Each reading described neutrally, without characterizing either as correct |
| Component value under each reading | Computed in the workbook |
| Ratio and status under each reading | Computed in the workbook |
| Status changes? | Yes / No |
| Prior practice | How the prior compliance certificate treated it, if known (fact only, not a conclusion) |
| Question for counsel or lenders | Specific question to resolve the item |
| Owner and date raised | Name and role |
| Resolution | Left blank for counsel or the treasurer; record source when resolved |

## Handling rules

- If no reading changes the status, report the status with a note that the ratio range spans the readings.
- If the status changes, set the covenant status to `Definition unclear` and show both results in the summary.
- Do not average readings or pick the "conservative" one as the reported figure.
- Once counsel or the treasurer resolves an item in writing, apply the resolution, cite the written source, and keep the log entry.
