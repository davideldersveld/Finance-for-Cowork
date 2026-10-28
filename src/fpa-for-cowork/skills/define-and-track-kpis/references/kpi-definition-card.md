# KPI definition card and status rules

## Definition card (one per KPI)

| Field | Content | Example |
|---|---|---|
| KPI name | Short, unique | Monthly customer churn |
| Purpose | Decision it informs | Retention investment |
| Formula | Numerator / Denominator, unit | Customers lost in month / Customers at start of month, % |
| Inclusions and exclusions | Precise rules | Excludes customers migrated to a group account; includes involuntary churn |
| Measurement basis | Point in time, period total or period average | Period total over opening count |
| Data source | System, report, field, extract timing | Billing system, subscription report, status field, extracted business day 2 |
| Owner | Name and role | Head of Customer Success |
| Frequency | Monthly, quarterly | Monthly |
| Target and source | Value and where it comes from | 2.0% per month, FY2027 budget |
| Polarity | Higher is better / Lower is better / Within range | Lower is better |
| RAG rule | Tolerance and how measured | Amber if above target by up to 0.3 points |
| Trend rule | Window and stable band | Latest vs average of prior 3 months; stable within 0.1 points |
| Baseline | First period of consistent data | January 2025 |
| Version and date | Change log | v1.1, 2 October 2026 |
| Definition status | Draft / Agreed / Definition pending | Agreed (confirmed by owner) |

## Common FP&A KPI formulas (adapt to the user's definitions)

| KPI | Formula |
|---|---|
| Revenue growth % | (Revenue_t − Revenue_(t−1 comparable)) / Revenue_(t−1 comparable) |
| Gross margin % | Gross margin / Net revenue |
| EBITDA margin % | EBITDA / Net revenue |
| Opex ratio | Operating expenses / Net revenue |
| Revenue per FTE | Net revenue / Average FTE |
| Customer churn % | Customers lost in period / Customers at start of period |
| Net revenue retention % | Recurring revenue from the start-of-period cohort at end / Recurring revenue of that cohort at start |
| Average revenue per customer | Revenue / Average customers |
| Forecast accuracy | 1 − |Actual − Forecast| / |Actual| |
| Cash conversion % | Operating cash flow / EBITDA |
| Capex to sales % | Capex / Net revenue |
| Inventory days (DIO) | Inventory / COGS × days in period |

Receivables, supplier, savings and covenant metrics belong to their own skills (see Boundaries in the skill).

## Attainment and RAG rules

Let A = actual, T = target, t = tolerance (in the KPI's unit, or t = T × p% when stated as a percentage of target).

| Polarity | Attainment % | Green | Amber | Red |
|---|---|---|---|---|
| Higher is better | A / T | A ≥ T | T − t ≤ A < T | A < T − t |
| Lower is better | T / A | A ≤ T | T < A ≤ T + t | A > T + t |
| Within range [L, U] | Distance to nearest bound | L ≤ A ≤ U | L − t ≤ A < L or U < A ≤ U + t | A < L − t or A > U + t |

- Attainment is `n/a` when A or T is zero or negative; report the gap only.
- Other statuses: No target, No data, Definition pending.

## Trend rule

Change = Latest − Average(prior n periods)
- Higher is better: Improving if Change > stable band; Deteriorating if Change < −stable band; else Stable.
- Lower is better: Improving if Change < −stable band; Deteriorating if Change > stable band; else Stable.
- Within range: Improving if distance to the range shrinks by more than the stable band; Deteriorating if it grows by more; else Stable.

## Definition conflict log

| KPI | Source A | Definition A | Value A | Source B | Definition B | Value B | Difference | Owner to decide | Status |
|---|---|---|---|---|---|---|---|---|---|
