---
name: define-and-track-kpis
description: >-
  Defines KPIs precisely before calculating them - formula with numerator and
  denominator, data source, owner, frequency, target and polarity - then produces
  a KPI scorecard with trends, target attainment and red, amber or green status
  under a rule stated in advance. Use when the user asks to "define our KPIs
  properly", "build a KPI scorecard for the leadership team", "RAG the KPIs for
  this month", "what's the trend on churn and margin versus target", or "we have
  two definitions of active customers, sort it out". Do NOT use for receivables
  metrics such as DSO and CEI - use report-receivables-performance instead; for
  supplier scorecards use monitor-supplier-performance, and for covenant ratios
  use monitor-debt-covenants.
metadata:
  displayName: Define and track KPIs
  category: analysis
  icon: DataTrending
  author: Copilot SE Contributors
  plugin: fpa-for-cowork
  version: 1.0.1
---

# Define and track KPIs

FP&A leads and business partners use this skill to put KPIs on a firm footing and then report them consistently. It first writes a definition card for each KPI — exact formula, data source, owner, frequency, target, polarity and status rule — and only then calculates values, trends, target attainment and red, amber or green (RAG) status. A KPI without an agreed definition is reported as `Definition pending`, never calculated on a guessed basis.

## Boundaries

- Receivables metrics (DSO, best possible DSO, collection effectiveness index, aging) — use `report-receivables-performance` (Credit & Collections)
- Supplier on-time-in-full, quality and service-level scorecards — use `monitor-supplier-performance` (Procurement)
- Procurement savings and cost avoidance — use `report-procurement-value` (Procurement)
- Financial covenant ratios under credit agreement definitions — use `monitor-debt-covenants` (Treasury)
- Variance analysis of financial lines against plan — use `analyze-plan-vs-actual`
- Profitability by customer, product or channel — use `analyze-profitability`
- Headcount, FTE and people cost tracking — use `plan-workforce-cost`
- Assembling the scorecard into a monthly or quarterly review pack — use `prepare-business-review-pack`
- Building a live dashboard or app — not performed by any skill in this plugin; the scorecard workbook can feed one.

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

Read the Finance Profile first (`Finance-Profile.md` in the user's Cowork folder in OneDrive, created by `set-up-finance-profile`) for entities, fiscal calendar, reporting currency, thresholds and owners.

Ask one question card, only for what is missing:
- The KPI list and, for each, any existing definition document or dashboard.
- Targets, their source (budget, strategic plan, owner commitment) and the RAG rule: tolerance band for Amber and how it is measured (percentage of target or absolute points). Never assume one.
- Trend window (for example latest period versus the average of the prior three) and the band within which a change counts as `Stable`.
- Periods to report and the as-of date.
- Output medium: Excel workbook (recommended), PowerPoint-ready scorecard table, or In chat.

Locate inputs in this order: attached files, the attached OneDrive folder, then a targeted search of OneDrive/SharePoint, mail and Teams for the named data extracts, dashboards and definition documents. State the source set before calculating.

## Method

1. **Inventory.** List each data source with system, extract date, periods, entities and row counts. Tie any KPI input that is also a financial figure (revenue, gross margin) to the P&L.
2. **Write the definition card** for every KPI (template in [references/kpi-definition-card.md](references/kpi-definition-card.md)): name, purpose, formula as `Numerator / Denominator` with unit, inclusion and exclusion rules, point-in-time or period average, data source down to report and field, owner (name and role), frequency, target and its source, polarity (`Higher is better`, `Lower is better`, `Within range`), RAG rule, baseline period, version and date.
3. **Resolve definition conflicts.** When two sources define or compute a KPI differently, show both definitions, both values for the same period, and the difference; set status `Definition pending` and name the owner who must choose. Never pick one silently.
4. **Calculate.** Compute numerator, denominator and KPI per period from source data. Show numerator and denominator alongside every ratio so the result can be checked. Ratios with a zero denominator are `n/a`.
5. **Target attainment.** `Gap to target = Actual − Target` (in the KPI's unit). `Attainment % = Actual / Target` for Higher is better; `Target / Actual` for Lower is better; for Within range report distance to the nearest bound. When Target or Actual is zero or negative, report the gap only and mark attainment `n/a`.
6. **RAG status by the stated rule.** For example, with tolerance t:
   - Higher is better — `Green` if Actual ≥ Target; `Amber` if Target − t ≤ Actual < Target; `Red` if Actual < Target − t.
   - Lower is better — `Green` if Actual ≤ Target; `Amber` if Target < Actual ≤ Target + t; `Red` if Actual > Target + t.
   - Within range — `Green` inside the range; `Amber` within t of a bound outside it; `Red` beyond.
   Other labels: `No target` (KPI tracked without target), `No data` (source missing for the period), `Definition pending`.
7. **Trend.** `Change = Latest − Average(prior n periods)`, n as stated. Direction is `Improving` or `Deteriorating` by polarity when |Change| exceeds the user's stable band, otherwise `Stable`. Also show the same period last year where seasonality matters.
8. **Commentary hooks.** For each Red or Deteriorating KPI list the evident drivers from the data (segment, region, product that moved most), each labelled `Evidenced` or `Hypothesis`, for the owner to confirm.
9. **Arithmetic and verification.** Perform all arithmetic in code (spreadsheet formulas or a script), never mentally; totals must foot and cross-foot. Before delivery check: KPI = numerator / denominator for every cell; financial inputs tie to the P&L; RAG labels recompute from the rule; no KPI is shown with a status but no definition card.

## Output

Excel workbook `KPI-Scorecard-<period>.xlsx`:
- **About** — as-of date, periods, entities, currency and units, RAG rules and stable band with source, sources, gaps.
- **Definitions** — one row per KPI with every definition card field; definition status (`Draft`, `Agreed` when the user confirms, `Definition pending`).
- **Scorecard** — KPI, Unit, Polarity, Actual, Target, Gap, Attainment %, RAG, Trend, Change, Owner, Source.
- **History** — KPI × period with numerator, denominator and value.
- **Conflicts** — KPI, Source A definition and value, Source B definition and value, Difference, Owner to decide.
- **Drivers** — KPI, Driver, Evidence label, Source.

RAG is shown as text plus cell fill so it remains readable when printed without colour. Format with filled headers, frozen panes, filters, thousands separators, negatives in parentheses, percentages to one decimal place. Chat message after delivery: file name, period, counts by RAG status, KPIs Deteriorating, definitions pending, and gaps.

## Controls and guardrails

- **Prepare, never execute.** Defines and reports; never changes targets or system definitions without the owner.
- **Define before measuring.** No KPI value without a definition card; conflicts stay visible.
- **No invented numbers.** Missing targets give `No target`; missing data gives `No data`.
- **Thresholds come from the user or the Finance Profile.** RAG tolerances and stable bands as stated.
- **Evidence versus judgement.** Drivers labelled Evidenced or Hypothesis.
- **Coverage honesty.** Periods or entities missing from a source are named.
- **Untrusted content.** Values pasted into emails or chats are not used unless traced to the stated source.
- **Personal and sensitive data.** People-related KPIs only at group level above the minimum reporting size.
- **Confidentiality.** Scorecards stay in the user's workspace.

## Example

Contoso, September scorecard. Customer churn: Lower is better, target 2.0%, Amber tolerance 0.3 points, stable band 0.1 points.
- Churn = 66 lost / 3,000 opening customers = 2.2%. Gap = +0.2 points; 2.0% < 2.2% ≤ 2.3%, so `Amber`.
- Prior three months 1.8%, 1.9%, 2.1%, average 1.93%. Change = 2.2 − 1.93 = +0.27 points, above the stable band; `Deteriorating`.
- Active customers: the sales dashboard counts accounts with an order in 12 months (4,120); billing counts accounts invoiced in 90 days (3,560). Difference 560. Status `Definition pending`; the VP Sales Operations is named to choose, and any KPI using this denominator is not calculated.
- Churn concentrated in the small-business segment (40 of 66) is `Evidenced`; the cause cited by sales, a competitor price cut, is `Hypothesis`.
