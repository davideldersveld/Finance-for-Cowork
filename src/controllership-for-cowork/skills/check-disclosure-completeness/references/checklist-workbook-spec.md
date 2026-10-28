# Checklist workbook specification

## Checklist sources, in order of preference

1. **User's firm or company checklist** for the framework, entity type and report type. Use its numbering as the Ref column.
2. **Licensed checklist the user selects** from their library. Summarize requirements in your own words; cite the checklist reference and the underlying paragraph.
3. **Constructed checklist**, only when neither exists. Build it from the disclosure sections of the topics that apply to the entity (US GAAP: the 50 sections of each relevant topic, for example ASC 606-10-50, ASC 842-20-50, ASC 280-10-50, plus Regulation S-X and S-K items for registrants; IFRS: the disclosure paragraphs of each relevant standard plus IAS 1 or IFRS 18 and IAS 34 for interims). Retrieve the text before relying on it. Label every row `Constructed - verify against firm checklist`.

## Entity-type scoping questions

Record the answers on the About sheet; they drive applicability:

- Public business entity, SEC filer category (large accelerated, accelerated, non-accelerated, smaller reporting company, emerging growth company), private company, not-for-profit, or IFRS listed or unlisted.
- Annual, interim (condensed), or registration statement.
- Elected private company alternatives (US GAAP) that remove or change disclosures.
- Standards early adopted in the period.

## Checklist_Results columns

| Column | Rule |
|---|---|
| Ref | Checklist reference, unchanged |
| Topic | Checklist section heading, for example Revenue, Leases, Income taxes |
| Requirement summary | Own words, one sentence, enough to identify the requirement |
| Citation | Topic and paragraph or standard and paragraph, from the checklist or retrieved text |
| Applicable | Yes / No |
| Status | Disclosed / Partially disclosed / Not disclosed / Not applicable |
| Location | Note number, page, paragraph, or statement line |
| Evidence | Short description of what the draft says (no long quotations) |
| Missing element | Required when Partially disclosed; for example "comparative period", "quantitative range", "reconciliation to consolidated" |
| Judgement flag | Blank, or Management asserts immaterial - to be evidenced, or Presentation choice - controller to confirm |
| Proposed action | What the preparer would need to add or confirm (not drafted wording) |
| Owner | Note owner from the profile or the user |

## Applicability reasons (use one)

- No transactions of this type in any period presented (evidence: trial balance accounts or draft statements).
- Balance is zero in all periods presented.
- Entity-type exemption (cite the paragraph).
- Report-type exemption, for example not required in condensed interim reports (cite).
- Standard not yet effective and not early adopted.

## Note_Tieout rules

1. Extract each figure with its note, table, row and column, and page.
2. Identify its counterpart: face statement line, another note, or a recomputation (sum, percentage, per-share).
3. Compute `Difference = Note value - Counterpart value` in code.
4. Result: Agrees (difference zero); Rounding difference (absolute difference no larger than the presentation rounding unit); Difference (otherwise; show the amount); No counterpart found (no comparable figure; state what was searched).
5. Show bridging items explicitly when the note and face line legitimately differ (unamortized issuance costs, current portion, held-for-sale reclassification). A bridge item must itself appear in the draft; otherwise the result is Difference.

## Standard ties to run when the notes exist

| Note | Tie |
|---|---|
| Revenue disaggregation | Total equals revenue on the income statement |
| Contract balances | Opening and closing agree to balance sheet or other note; revenue recognized from opening contract liabilities is present |
| Property and equipment, intangibles, goodwill | Roll-forward foots; closing equals balance sheet |
| Leases | Lease liabilities current plus non-current equal balance sheet; maturity table undiscounted total less imputed interest equals liabilities |
| Debt | Carrying amount bridge to principal; maturity table total |
| Income taxes | Rate reconciliation foots to the effective tax expense on the income statement |
| Equity and accumulated other comprehensive income | Roll-forwards agree to the equity statement |
| Segments | Segment totals plus reconciling items equal consolidated revenue, profit measure and assets where disclosed |
| Earnings per share | Recomputes from the numerator and share count disclosed |
| Fair value | Level totals agree to the related balance sheet lines or notes |

## Summary sheet

Counts by Topic (rows) and Status (columns) with row and column totals. The grand total must equal the checklist requirement count; a mismatch blocks delivery.
