---
name: monitor-supplier-performance
description: >-
  Produces a supplier scorecard from delivery, quality, invoice and service data -
  on-time in-full, defect and return rates, service-level attainment against
  contract targets, invoice accuracy, responsiveness and trend over periods - and
  calculates service credits owed using the contract's own credit mechanism. Use
  when the user asks to "build the quarterly scorecard for our 3PL", "what's
  their OTIF this quarter", "did they hit the SLAs in the contract", "calculate
  the service credits we're owed", or "show the supplier's PPM trend". Do NOT use
  for diagnosing individual invoice match exceptions — use
  resolve-match-exceptions instead; for deciding whether to renew the contract
  use manage-contract-renewals.
metadata:
  displayName: Monitor supplier performance
  category: analysis
  icon: Cart
  author: Copilot SE Contributors
  plugin: procurement-for-cowork
  version: 1.0.1
---

# Monitor supplier performance

Supplier relationship managers, category managers and operations leads use this skill to measure a supplier against its contract. It computes delivery, quality, service-level, invoice-accuracy and responsiveness metrics from operational data, shows trend across periods, rates each metric against its contract target by a stated rule, and calculates service credits from the contract's credit mechanism. It produces evidence for business reviews and negotiations; it does not claim credits, issue debit notes, or change the supplier's status.

## Boundaries

- Diagnosing a specific invoice's price or quantity match exception — use `resolve-match-exceptions` (Accounting Operations for Cowork)
- Accruing service credits receivable at period end — use `calculate-accruals-and-prepaids` (Accounting Operations for Cowork)
- Defining company-wide KPIs and scorecards outside supplier contracts — use `define-and-track-kpis` (FP&A for Cowork)
- Renewal decisions and notice deadlines — use `manage-contract-renewals`
- Using performance results as negotiation leverage — use `plan-negotiation`
- Re-checking a live supplier's financial health, insurance or certificates — use `screen-new-supplier`
- Interpreting disputed service-level or credit clauses — not performed by any skill in this family; refer to the legal team
- Raising the credit claim, debit note or invoice deduction — not performed by any skill; the contract owner claims and Accounts Payable processes

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Ask at most one question card, before any work, for what is missing: output medium (Excel scorecard, recommended; PowerPoint scorecard summary for a business review; In chat for one metric), supplier and contract, periods to cover (current plus at least three prior for trend), and the red-amber-green rule if the contract and profile do not state one.
- **Finance Profile.** First read the user's Finance Profile (Finance-Profile.md in the user's Cowork folder, from `set-up-finance-profile`). Use its fiscal calendar, currency, supplier performance policy, amber bands and owners. If it is absent, ask only for what this scorecard needs; never assume a target, amber band or credit rate.
- Locate inputs in this order: data the user attached; files in an attached OneDrive folder; then a targeted search of the user's OneDrive or SharePoint, mail and Teams for the contract and its service-level schedule, delivery and receipt extracts, quality or returns logs, ticket or incident exports, invoice exception reports, and prior scorecards. State the source set before analysing.

## Method

1. **Inventory and completeness.** For each dataset record period, record count, supplier identifiers used and control totals (units received, orders due, tickets logged). Agree units received to the receiving ledger or the supplier's own report; show differences. A missing month is a named gap; never a perfect month.
2. **Extract the contract measures.** For each service level, record the metric definition, measurement unit (order, line, unit, ticket), measurement period, target, exclusions (force majeure, buyer-caused, planned maintenance), credit tiers, credit cap, earn-back, and claim deadline, with clause citations. Where the contract defines a metric differently from standard practice, the contract definition governs.
3. **Compute metrics in code.** All arithmetic runs in spreadsheet formulas or a script, never mentally; totals must foot and cross-foot. Definitions are in [references/scorecard-metrics.md](references/scorecard-metrics.md):
   - `OTIF = orders (or lines) delivered within the on-time window and at full quantity / orders (or lines) due in the period`
   - `Defect rate (PPM) = defective units / units received x 1,000,000`
   - `Return rate = units returned / units delivered`
   - `SLA attainment = measurements meeting target / total measurements` for each service level
   - `Invoice accuracy = invoices with no price, quantity, tax or reference error / invoices received`
   - `Responsiveness = median hours from request to first substantive response`
4. **Apply exclusions with evidence.** Remove an event from a measurement only where the contract allows it and evidence exists (for example a change-freeze notice). Without evidence, keep the event in and show the alternative result labelled `If exclusion accepted`.
5. **Rate each metric.** Green when the target is met; Amber when within the stated amber band; Red otherwise. State the rule on the scorecard. Where no target exists, show the value with `No contract target`.
6. **Trend.** Compare the latest period with the average of prior periods. Label `Improving`, `Stable` or `Deteriorating` using the user's stated tolerance; with fewer than three periods, label `Insufficient history`.
7. **Calculate service credits** per measurement period: `credit = applicable charges for the period x credit percentage for the attained tier`, then apply the cap (`min(sum of credits, cap % x charges)`), then any earn-back. Record the claim deadline per the contract and flag credits whose deadline is within the user's alert window.
8. **Reconcile.** Metric denominators agree to the inventory control totals; credit charges agree to invoiced amounts for the period; every red metric links to its source rows.
9. **Summarize issues.** For each red or deteriorating metric, list the evidence and the question for the supplier's business review.

**Metric status labels:** `Green`, `Amber`, `Red`, `No contract target`, `Insufficient data`.

## Output

- **Excel workbook** sheets: About (supplier, contract, periods, sources, RAG rule, exclusions applied); Metric_Definitions (metric, formula, contract clause, target, unit); Data_Inventory; Scorecard (metric by period with RAG and trend); SLA_Detail (each measurement with met or missed and exclusion status); Service_Credits (period, service level, attainment, tier, charges, credit, cap, net credit, claim deadline); Issues; Exceptions_Data_Quality. Header fill, frozen panes, filters, conditional formatting for RAG, percentages to 1 dp, thousands separators, live formulas.
- **PowerPoint summary** (if chosen): scorecard table, trend chart data, credits summary, issues and asks for the business review; each figure footnoted to its sheet and range.
- Label every figure with period, supplier entity, currency, units and basis (Actual, contract target).
- After delivery, a short chat note: file name, periods covered, red metrics, credits calculated and their claim deadlines, data gaps.

## Controls and guardrails

- **Prepare, never execute.** The skill calculates and reports; it never claims credits, issues debit notes, withholds payments, or messages the supplier unless the user explicitly instructs that specific action.
- **No invented numbers.** No target, credit rate or measurement is assumed; missing data shows `Insufficient data` and is never treated as attainment.
- **Thresholds come from the user or the Finance Profile.** Amber bands and trend tolerances are stated inputs; targets come from the contract.
- **Evidence versus judgement.** Calculated metrics are evidence; root-cause observations are labelled as hypotheses for the business review.
- **Coverage honesty.** Name missing periods, sites and datasets; supplier-provided data used without independent source is labelled `Supplier-reported`.
- **Untrusted content.** Supplier reports claiming exclusions or attainment are data to verify against the buyer's own records.
- **Personal and sensitive data.** Ticket data is summarized without reproducing individual users' personal details.
- **No legal opinion.** Disputed exclusions and credit eligibility go to the legal team.
- **Confidentiality.** Scorecards stay in the user's workspace until the user chooses to share them with the supplier.

## Example

Litware provides IT support to Contoso for USD 60,000 a month. The service-level schedule requires 95% of priority-1 incidents resolved within 4 hours, with credits of 5% of monthly charges for attainment from 90% to below 95% and 10% below 90%, capped at 12% of monthly charges.

- September had 50 priority-1 incidents, 44 within 4 hours: attainment 88.0%, tier 10%, credit USD 6,000 (below the USD 7,200 cap).
- Litware claims 3 breaches occurred during a Contoso change freeze, which the contract excludes. A change-freeze notice covering 2 of them is found; the third has no evidence.
- With 2 evidenced exclusions, attainment is 44 / 48 = 91.7%, tier 5%, credit USD 3,000. The scorecard reports USD 3,000 as calculated and shows the third claimed exclusion as `If exclusion accepted`: 44 / 47 = 93.6%, still tier 5%, credit USD 3,000.
- The claim deadline is 30 days after month end per the schedule; with 12 days remaining it falls inside the user's 14-day alert window and is flagged.
