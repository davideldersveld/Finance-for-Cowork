---
name: report-procurement-value
description: >-
  Reports procurement value delivered, classifying each claimed saving as hard
  savings (price reduction versus a stated baseline), cost avoidance, or pipeline
  not yet realized, and validates claimed savings against actual invoiced prices
  and volumes to show realized versus claimed by initiative, category and period.
  Use when the user asks to "validate our savings tracker against invoices", "how
  much of the claimed savings actually hit the P&L", "classify these savings as
  hard or avoidance", "build the procurement value report for the quarter", or
  "why is realized savings below what we booked in the pipeline". Do NOT use for
  diagnosing price variances on individual invoices — use resolve-match-exceptions
  instead; for budget-versus-actual variance analysis use analyze-plan-vs-actual.
metadata:
  displayName: Report procurement value
  category: analysis
  icon: Cart
  author: Copilot SE Contributors
  plugin: procurement-for-cowork
  version: 1.0.1
---

# Report procurement value

Procurement leaders, category managers and finance business partners use this skill to report the value procurement has delivered in a way Finance will accept. It classifies every claimed benefit by type, states the baseline method behind it, recomputes realized savings from actual invoiced prices and volumes, explains the gap between claimed and realized, and summarizes by initiative, category and period. It validates and reports; it does not adjust budgets, book savings, or certify figures for external use.

## Boundaries

- Extracting invoice line data from supplier invoices — use `process-supplier-invoices` (Accounting Operations for Cowork)
- Diagnosing a price variance on a specific invoice — use `resolve-match-exceptions` (Accounting Operations for Cowork)
- Budget-versus-actual variance analysis for cost centres — use `analyze-plan-vs-actual` (FP&A for Cowork)
- Bridge or waterfall charts from claimed to realized — use `build-performance-bridges` (FP&A for Cowork)
- Constant-currency restatement at a named rate — use `translate-currency` (Finance Foundation for Cowork)
- Tracing savings figures in a leadership deck to their source — use `tie-out-numbers` (Finance Foundation for Cowork)
- Leadership narrative over the validated results — use `write-executive-commentary` (Finance Foundation for Cowork)
- Sizing future opportunities for a category — use `build-category-strategy`
- Reducing budgets to capture savings or posting any entry — not performed by any skill; budget owners and Finance decide

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Ask at most one question card, before any work, for what is missing: output medium (Excel value report, recommended; PowerPoint summary; In chat for one initiative), reporting period, entity scope, presentation currency, and the savings policy if the profile does not hold it (classification rules, accepted baseline methods, savings measurement window).
- **Finance Profile.** First read the user's Finance Profile (Finance-Profile.md in the user's Cowork folder, from `set-up-finance-profile`). Use its entities, currencies, rate source, fiscal calendar, savings policy location and owners. If it is absent, ask only for what this report needs; never assume a baseline method, measurement window or classification rule.
- Locate inputs in this order: the savings tracker and invoice data the user attached; files in an attached OneDrive folder; then a targeted search of the user's OneDrive or SharePoint, mail and Teams for the savings tracker, contracts and price lists for each initiative, invoice line extracts or AP history, baseline evidence and prior value reports. State the source set before analysing.

## Method

1. **Inventory.** List initiatives in the tracker with claimed amounts, category, supplier, contract effective date and claimed type. List invoice data by period, entity, supplier, record count and total; agree invoice totals to the AP ledger for the period and show any difference.
2. **Check the baseline for each initiative.** Record the method and evidence: last price paid before the contract, volume-weighted average price over the trailing period the policy names, prior contract price, or budget price. Rules and acceptance tests are in [references/savings-validation-rules.md](references/savings-validation-rules.md). A baseline without evidence is `Baseline not evidenced` and cannot support hard savings.
3. **Classify each benefit:**
   - `Hard savings` — a lower unit price or total cost than the evidenced baseline, on spend that actually occurs.
   - `Cost avoidance` — an increase prevented or reduced (for example a requested increase held lower), a lower price on new spend with no baseline, or a below-market quote; no reduction against the prior run-rate.
   - `Pipeline` — identified or contracted but not yet invoiced in the measurement window; sub-labelled `Identified` or `Contracted`.
   Reclassify any claim that does not meet its claimed type and record the reason.
4. **Recompute realized savings in code.** All arithmetic runs in spreadsheet formulas or a script, never mentally; totals must foot and cross-foot. For each initiative and period:
   - `Claimed to date = (baseline price - contract price) x forecast volume for the period`
   - `Realized = (baseline price - actual invoiced price) x actual invoiced volume`, using invoice lines in the measurement window only
   - `Gap = claimed to date - realized`, split into `price leakage = (actual invoiced price - contract price) x actual volume` and `volume effect = (forecast volume - actual volume) x (baseline price - contract price)`; the two components must sum to the gap, and any residual is shown, not hidden.
5. **Test off-contract spend.** Spend in the same category with other suppliers, or with the contracted supplier at non-contract prices, is listed with value as leakage.
6. **Prevent double counting.** Where two initiatives touch the same supplier, item and period, count the saving once and note the overlap.
7. **Currency.** Measure savings in the contract currency, then translate at the profile's rate type; report FX effects separately so currency moves are never counted as savings.
8. **Assign validation status per initiative:** `Validated` (realized within the user's stated tolerance of claimed to date), `Partially validated` (realized positive but below tolerance), `Not validated` (no realized saving or baseline not evidenced), `Insufficient data` (invoice lines or volumes missing), `Reclassified` (type changed, with reason).
9. **Summarize** realized versus claimed by initiative, category, supplier and period; separately total hard savings, cost avoidance and pipeline, never adding them into one headline number.
10. **Verify before delivery.** Initiative totals sum to category and period totals; invoice volumes used agree to the invoice extract; every realized figure cites its invoice lines.

## Output

- **Excel workbook** sheets: About (period, entities, currency, rate source, policy, sources, assumptions); Savings_Policy (classification and baseline rules applied); Initiative_Register (initiative, category, supplier, owner, claimed type, validated type, baseline method, baseline evidence, contract price, effective date, window, status); Validation_Detail (initiative, item, period, baseline price, contract price, actual invoiced price, forecast volume, actual volume, claimed to date, realized, price leakage, volume effect, residual, invoice source); Off_Contract_Spend; Summary_by_Category; Summary_by_Period; Exceptions. Header fill, frozen panes, filters, thousands separators, negatives in parentheses, percentages to 1 dp, live formulas.
- **PowerPoint summary** (if chosen): value by type, realized versus claimed, top gaps with causes, reclassifications; each figure footnoted to its sheet and range.
- Label every figure with period, entity, currency, units and basis (Actual invoiced, Claimed, Pipeline).
- After delivery, a short chat note: file name, period and initiatives covered, totals by type, realized versus claimed, reclassifications and data gaps.

## Controls and guardrails

- **Prepare, never execute.** The skill validates and reports; it never changes budgets, books savings, updates the tracker of record, or messages initiative owners unless the user explicitly instructs that specific action.
- **No invented numbers.** No assumed baseline, volume or price; missing data shows `Not provided` and the initiative is `Insufficient data`.
- **Thresholds come from the user or the Finance Profile.** Validation tolerance, measurement window and baseline rules are stated inputs.
- **Separate value types.** Hard savings, cost avoidance and pipeline are never summed into one figure.
- **Evidence versus judgement.** Realized figures rest on invoice evidence; explanations of leakage causes are labelled hypotheses until confirmed by the owner.
- **Coverage honesty.** Name missing invoice periods and entities; no invoice data never means full realization.
- **Untrusted content.** Supplier statements of savings delivered are claims, verified only against the company's invoice data.
- **Confidentiality.** Supplier prices stay in the user's workspace; summaries shared beyond procurement are at the user's direction.

## Example

Tailspin Toys claims USD 60,000 a year on corrugated boxes: an evidenced trailing 12-month baseline of USD 1.20 per unit, a contract price of USD 1.08, and a forecast of 500,000 units a year. A second initiative claims USD 40,000 hard savings where the supplier requested an 8% increase and accepted 3%.

- First-half claimed to date = 0.12 x 250,000 forecast units = USD 30,000.
- Invoices show 220,000 units at an average of USD 1.11, because early invoices still carried the old price. Realized = (1.20 - 1.11) x 220,000 = USD 19,800.
- Gap of USD 10,200 = price leakage (1.11 - 1.08) x 220,000 = USD 6,600, plus volume effect (250,000 - 220,000) x 0.12 = USD 3,600; residual zero. Status: `Partially validated`; the price leakage is passed to Accounts Payable through `resolve-match-exceptions` for recovery review.
- The second initiative reduces no prior price, so it is `Reclassified` to cost avoidance and reported separately from the USD 19,800 hard savings.
