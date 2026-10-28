# Threshold test specification

## Rule Sources register fields

| Field | Example of how to record (values must come from the cited source) |
|---|---|
| Rule ID | NX-<jurisdiction>-<tax type>-<version> |
| Jurisdiction, Tax type | As named by the authority |
| Threshold amount, currency | Exactly as the source states |
| Measure | Gross sales / Retail sales / Taxable sales / Transactions / Other (quote the source term) |
| Conjunction | And / Or / Single test |
| Comparison wording | Exceeds / Meets or exceeds / Other (quote) |
| Measurement period | Prior calendar year / Current calendar year / Rolling 12 months / Preceding four quarters / Other (quote) |
| Inclusions and exclusions | Marketplace-facilitated sales, exempt sales, resale sales, services, digital supplies |
| Non-established business rule | Whether the source applies a different or nil threshold to businesses not established there |
| Registration lag | Time allowed after crossing, or `Not provided` |
| Effective from, Effective to | Dates the rule applies |
| Source type | User-supplied / Retrieved authoritative |
| Citation | Title, section, URL or document reference |
| Retrieval date | Date the source was read |

## Measure computation

- `Measure value (sales) = SUM(net amount of qualifying rows in period)` after applying cited inclusions and exclusions.
- `Measure value (transactions) = COUNT(distinct qualifying invoices in period)`; count credit notes only if the cited source says so, otherwise exclude and note the assumption.
- Rolling 12 months is evaluated at each month end in scope; report the highest ratio and its month.
- When the rule allows either the prior or current year, evaluate both and report the earlier crossing.
- FX: `Amount in threshold currency = Amount x Rate`, rate type, source and date recorded in About.

## Status rules

| Status | Condition |
|---|---|
| Exceeds | Comparison satisfied for the conjunction (Or: any test; And: all tests) in any tested period |
| Approaching | Not Exceeds, and highest ratio >= user watch level |
| Below | Not Exceeds and highest ratio < watch level |
| Rule not provided | No cited rule for the jurisdiction and tax type |
| Data insufficient | Rule cited, but required fields (location, date, channel) missing for rows whose value could change the status |

Data insufficient test: if `Measure value + value of unassigned rows that could belong to the jurisdiction` would change the status, label `Data insufficient` and show both figures.

## Crossing date

1. Filter qualifying rows for the jurisdiction and period; sort by date, then document number.
2. Compute running sales and running count.
3. Crossing date = first date where the running measure satisfies the comparison wording (strictly greater than threshold for "exceeds"; greater than or equal for "meets or exceeds").
4. With an Or conjunction, crossing date = earliest date across tests.

## Physical presence indicators checklist

Employees working in the jurisdiction (count, role); contractors or agents acting for the business; owned or leased property; inventory, including at third-party or marketplace warehouses; installation, repair or training services performed on site; trade shows or events with sales; delivery in own vehicles. Each indicator: evidence document, period, label Indicator present / Not present / Unknown. The adviser concludes.
