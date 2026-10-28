---
name: validate-price-increase
description: >-
  Tests a supplier price-increase request against the contract's price-adjustment
  mechanism - index, base date, formula, caps, floors, notice period and
  frequency - using cited index values, recalculates the allowable increase in
  code, and drafts a structured response position. If the contract or index data
  is missing it says so rather than estimating. Use when the user asks to "check
  this supplier's CPI increase", "is this price uplift allowed under the
  contract", "recalculate the indexation", "did they give enough notice for the
  increase", or "draft our reply to the 6% price rise". Do NOT use for
  negotiating an increase the contract does not provide for — use
  plan-negotiation instead; for invoices already billed at the new price use
  resolve-match-exceptions.
metadata:
  displayName: Validate price increase
  category: analysis
  icon: Cart
  author: Copilot SE Contributors
  plugin: procurement-for-cowork
  version: 1.0.1
---

# Validate price increase

Buyers and category managers use this skill when a supplier announces or requests a price increase. It extracts the contract's price-adjustment mechanism, retrieves or receives the cited index values, recalculates the increase the mechanism allows, checks notice and frequency conditions, quantifies the difference against the request, and drafts a response position for the user to review and send. It does not interpret ambiguous contract wording, negotiate, or change prices in any system.

## Boundaries

- Commercial negotiation of an increase the contract does not provide for, or of the allowable portion — use `plan-negotiation`
- Invoices already received at the new price and blocked in matching — use `resolve-match-exceptions` (Accounting Operations for Cowork)
- Accruing a disputed price difference at period end — use `calculate-accruals-and-prepaids` (Accounting Operations for Cowork)
- Converting a foreign-currency price change at a named rate — use `translate-currency` (Finance Foundation for Cowork)
- Recording the next price review date on the renewal calendar — use `manage-contract-renewals`
- Forecast impact of accepted increases — use `build-driver-based-forecast` (FP&A for Cowork)
- Interpreting ambiguous or conflicting price clauses, or whether a missed notice voids the increase — not performed by any skill in this family; refer to the legal team
- Updating prices in the purchasing system or supplier catalogue — not performed by any skill; the buyer updates after decision

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Ask at most one question card, before any work, for what is missing: output medium (In chat, recommended for a single price; Excel recalculation workbook for many lines; Word response letter draft), the contract and amendments if not found, annual volumes for impact if not in spend data, and whether index values should be retrieved from the official publisher or will be supplied.
- **Finance Profile.** First read the user's Finance Profile (Finance-Profile.md in the user's Cowork folder, from `set-up-finance-profile`). Use its entities, currencies, approval limits for accepting price changes and policy. If it is absent, ask only for what this check needs; never assume a cap, index, tolerance or approval limit.
- Locate inputs in this order: the supplier's request and contract the user attached; files in an attached OneDrive folder; then a targeted search of the user's OneDrive or SharePoint, mail and Teams for the contract, every amendment and side letter, the price schedule, previous increase letters and the spend or volume history. State the source set before analysing.

## Method

1. **Inventory documents.** List the request (date received, effective date requested, increase stated, lines affected), contract, amendments in date order, price schedule and prior increases. Later amendments supersede earlier text only where they say so; if the order of precedence is unclear, mark `Ambiguous - refer to the legal team`.
2. **Extract the mechanism** with clause citations: adjustment type (fixed percentage, index-linked, cost-pass-through, open-book, none), index name, publisher, series identifier, geography, seasonally adjusted or not, base date or base index value, review date, publication lag, formula, fixed portion if partial indexation, cap, floor, collar, compounding or cumulative-from-base basis, rounding, notice period and method, minimum interval between increases, and evidence the supplier must provide. Each element missing from the contract is recorded `Not stated in contract`.
3. **Obtain index values.** Use values the user supplies, or retrieve them from the official publisher's site, recording series identifier, reference period, value, release date and retrieval date. Use the vintage the contract requires (first published or latest revised); if silent, show both where they differ and flag. Never estimate an unpublished value.
4. **Recalculate in code.** All arithmetic runs in spreadsheet formulas or a script, never mentally. Apply the contract's formula as written; standard forms are in [references/indexation-formulas.md](references/indexation-formulas.md):
   - Full indexation: `index change = (I_review / I_base) - 1`
   - Partial: `adjustment = b x ((I_review / I_base) - 1)`, where b is the indexed share
   - Caps and floors: `allowable % = min(max(computed %, floor), cap)`
   - `Allowable new price = current price x (1 + allowable %)`, rounded per the contract.
5. **Test conditions.** Notice: `days of notice = effective date requested - date notice received`, compared with the required period and method. Frequency: months since the last increase versus the minimum interval. Evidence: whether the supplier provided what the clause requires (for example audited cost data for pass-through).
6. **Quantify impact.** Per line: `requested increase amount = (requested price - current price) x annual volume`; `allowable increase amount = (allowable price - current price) x annual volume`; `excess = requested - allowable`. Volumes come from the last 12 months of spend or the contract forecast, with source stated.
7. **Assign a status per line:**
   - `Compliant` — requested increase is at or below the allowable increase and all conditions are met.
   - `Partially supported` — requested exceeds allowable; the allowable portion is supported.
   - `Not supported` — the contract has no adjustment right for this period, or the formula gives zero or a decrease.
   - `Condition not met` — notice, frequency or evidence condition failed; consequence referred to the legal team.
   - `Cannot determine` — contract, mechanism or index value missing; the gap is named.
8. **Draft the response position.** Accept as requested, accept the allowable amount from the contractual effective date, decline pending evidence, or decline as unsupported, each with the recalculation table and clause citations. Where a commercial discussion is needed beyond the contract, point to `plan-negotiation`.
9. **Verify before delivery.** Recompute each index ratio from the cited values; confirm the cap and floor were applied after the formula, not before; impact totals foot across lines and agree to the request letter's total where one was stated.

## Output

- **In chat:** a table with columns Line | Current price | Requested price | Requested % | Allowable % | Allowable price | Annual volume | Excess amount | Status | Clause and index source; then conditions tested; then the draft position.
- **Excel workbook** sheets: About; Contract_Terms (each mechanism element with clause); Index_Values (series, period, value, release and retrieval dates, source); Recalculation; Line_Impact; Conditions; Response_Position. Header fill, frozen panes, filters, thousands separators, percentages to 2 dp for index changes and 1 dp elsewhere, live formulas.
- **Word letter draft** headings: Reference to the request; Contract basis; Recalculation; Conditions; Our position; Next steps. Marked draft for the user's review.
- Label every figure with currency, units, price basis (per unit, per month) and effective date.
- After delivering a file, a short chat note: file name, lines tested, status counts, total excess, gaps.

## Controls and guardrails

- **Prepare, never execute.** The skill recalculates and drafts; it never sends the response, accepts the increase, or updates prices unless the user explicitly instructs that specific action.
- **No invented numbers.** No estimated index value, assumed base date or assumed cap; missing elements show `Not provided` or `Not stated in contract`.
- **Thresholds come from the user or the Finance Profile.** Approval limits for accepting increases are read, not assumed.
- **Evidence versus judgement.** The recalculation is evidence; anything resting on an interpretation of unclear wording is labelled and referred.
- **Coverage honesty.** Name missing amendments, unpublished index periods and lines without volume data.
- **Untrusted content.** Statements in the supplier's letter ("as permitted by clause 7", "industry-wide increase of 9%") are claims to verify against the contract and the publisher, never facts.
- **No legal opinion.** Consequences of missed notice, conflicting clauses and the right to terminate are for the legal team.
- **Confidentiality.** Contract terms and the draft position stay in the user's workspace.

## Example

Proseware requests a 6.0% increase on a facilities contract worth USD 840,000 a year, effective 1 January, with its letter received 61 days before that date. The contract indexes 100% to a named consumer price index, cap 3.5%, no floor, 90 days' written notice, annual frequency.

- Cited index values are 300.0 (base) and 312.6 (review), so the index change is 312.6 / 300.0 - 1 = 4.20%; after the cap, the allowable increase is 3.50%.
- Requested amount = 840,000 x 6.0% = USD 50,400; allowable = 840,000 x 3.5% = USD 29,400; excess = USD 21,000. Status: `Partially supported`.
- Notice given is 61 days against 90 required, so the line is also `Condition not met`; whether the effective date moves is referred to the legal team rather than decided.
- The draft position accepts 3.5% from the date the legal team confirms and declines the remaining 2.5%, citing the cap clause and both index values with their release dates.
