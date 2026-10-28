---
name: manage-contract-renewals
description: >-
  Builds and maintains a supplier renewal calendar from contracts and the contract
  register - expiry, auto-renewal terms, notice deadline, price review dates,
  owner, annual value - and sets a recommended decision date ahead of each notice
  window, flagging register entries that disagree with the contract. Can alert
  owners on a recurring schedule only when explicitly requested. Use when the
  user asks to "build a renewal calendar from our contract register", "which
  contracts auto-renew in the next 90 days", "when is the notice deadline on the
  SaaS agreements", "remind contract owners before notice windows", or "what
  renewals are coming up this quarter". Do NOT use for negotiating the renewal —
  use plan-negotiation instead; for testing a price review under the indexation
  clause use validate-price-increase.
metadata:
  displayName: Manage contract renewals
  category: productivity
  icon: Cart
  author: Copilot SE Contributors
  plugin: procurement-for-cowork
  version: 1.0.1
---

# Manage contract renewals

Contract managers, category managers and procurement operations use this skill to stop supplier contracts from rolling over unnoticed. It reads the contract register and the underlying contracts, computes notice deadlines and decision dates, highlights what needs attention now, and reports where the register disagrees with the signed documents. It keeps the calendar current on request and, only when the user explicitly asks for a recurring schedule, prepares alerts to owners. It does not decide whether to renew, serve notice, or interpret termination rights.

## Boundaries

- Negotiation preparation for a renewal — use `plan-negotiation`
- Retendering a contract that will not be renewed — use `prepare-sourcing-package`
- Testing a price review or indexation uplift that falls due — use `validate-price-increase`
- Supplier performance evidence for the renewal decision — use `monitor-supplier-performance`
- Category-wide wave planning built on these dates — use `build-category-strategy`
- Debt facility maturities and lender notice dates — use `maintain-debt-register` (Treasury for Cowork)
- Lease terms and options for lease accounting — use `abstract-lease-for-accounting` (Controllership & External Reporting for Cowork)
- The company's own insurance policy renewals — use `prepare-insurance-renewal` (Treasury for Cowork)
- Tax filing deadlines — use `maintain-tax-compliance-calendar` (Tax for Cowork)
- Interpreting unclear renewal, termination or notice clauses, or drafting a termination notice — not performed by any skill in this family; refer to the legal team
- Serving notice on a supplier or updating the system of record — not performed by any skill; the contract owner acts

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Ask at most one question card, before any work, for what is missing: output medium (Excel renewal calendar, recommended; In chat list for a short window), the look-ahead window (for example 90 or 180 days), the as-of date (default today), entity scope, and whether owner alerts should be prepared once or on a recurring schedule.
- **Finance Profile.** First read the user's Finance Profile (Finance-Profile.md in the user's Cowork folder, from `set-up-finance-profile`). Use its entities, currency, business-day calendar, contract register location, decision lead times by value band or sourcing route, and owners. If it is absent, ask only for the lead times and window this task needs; never assume a lead time or window.
- Locate inputs in this order: the register and contracts the user attached; files in an attached OneDrive folder; then a targeted search of the user's OneDrive or SharePoint for the contract register and the signed contracts, amendments and renewal letters it references, and of mail and Teams for notices already sent or received. State the source set before analysing.

## Method

1. **Inventory.** List register rows, contracts located, contracts referenced but not found, and amendments. Report the count of register rows without a located contract; those dates are labelled `Register only - unverified`.
2. **Extract terms from each contract and its latest amendment,** with clause citations: start date, current term end, renewal type, renewal term length, number of renewals remaining, notice period, notice unit (calendar days, business days, months), notice method and recipient, termination-for-convenience rights, price review dates and mechanism reference, annual value, currency, owner, entity. Renewal types are defined in [references/renewal-date-rules.md](references/renewal-date-rules.md).
3. **Compare register to contract.** Where register dates, values or renewal type differ from the signed documents, record `Register mismatch` with both values and the clause; the contract governs unless a later amendment is missing, in which case say so.
4. **Compute dates in code.** All date and amount arithmetic runs in spreadsheet formulas or a script, never mentally:
   - `Notice deadline = current term end - notice period` in the contract's unit; where notice must be received by a date, subtract the delivery time the method needs.
   - If the deadline falls on a non-business day and the contract is silent, move it to the previous business day and label the adjustment.
   - `Recommended decision date = notice deadline - decision lead time` from the profile for the contract's value band or likely sourcing route.
   - For evergreen or auto-renewing contracts already past the notice deadline, compute the next term end and the next notice deadline (`Locked in until`).
   - `Annual value` from the contract or the last 12 months of spend, with the basis stated; `remaining commitment = annual value x years remaining`.
5. **Assign status as of the as-of date:**
   - `Decision overdue` — as-of date is after the recommended decision date and before the notice deadline.
   - `Notice deadline missed - locked in` — auto-renewal occurred or will occur; next window shown.
   - `Decision due` — recommended decision date is within the look-ahead window.
   - `Upcoming` — notice deadline within the window but decision date later.
   - `Not in window`, `Notice served`, `Renewed`, `Expired`, `Data incomplete` (term end or notice period missing).
6. **Prepare alerts** for owners of `Decision overdue` and `Decision due` items: contract, supplier, notice deadline, decision date, annual value and the decision needed. Draft only; send only when the user explicitly instructs it. On a recurring schedule the user explicitly asked for, refresh statuses each run and alert only on new or changed items.
7. **Maintain.** On each update, log changes (new contracts, amended dates, status transitions) with date and source; never overwrite a prior value without logging it.
8. **Verify before delivery.** Recompute a sample of deadlines independently; every date cites its clause or register row; status counts sum to total rows; annual values total to the summary.

## Output

- **Excel workbook** sheets: About (as-of date, window, entities, lead-time table, sources, assumptions); Renewal_Calendar (Contract ID, Supplier, Title, Entity, Owner, Category, Start, Term end, Renewal type, Renewal term, Notice period, Notice unit, Notice method, Notice deadline, Decision lead time, Recommended decision date, Price review date, Annual value, Currency, Value basis, Status, Clause references); Action_Window (items due within the look-ahead window, sorted by notice deadline); Register_Mismatches; Data_Gaps; Change_Log; Alert_Drafts. Header fill, frozen panes, filters, date format yyyy-mm-dd, thousands separators, conditional formatting by status.
- **In chat:** a table of items in the window with the same key columns, then mismatches and gaps.
- Label values with currency, units and basis (contract value or trailing 12-month spend).
- After delivery, a short chat note: file name, contracts covered, counts by status, total annual value in the window, mismatches and gaps.

## Controls and guardrails

- **Prepare, never execute.** The skill calculates and drafts alerts; it never serves notice, sends alerts, or updates the register or contract system unless the user explicitly instructs that specific action.
- **Recurring only on request.** Scheduled runs and alerts happen only when the user explicitly asks for a recurring schedule.
- **No invented numbers.** No assumed notice period, term end or value; missing items show `Not provided` and the row is `Data incomplete`.
- **Thresholds come from the user or the Finance Profile.** Lead times and look-ahead windows are stated inputs.
- **Evidence versus judgement.** Dates computed from signed documents are evidence; register-only dates are labelled unverified.
- **Coverage honesty.** Name contracts not located, unreadable scans and amendments referenced but missing.
- **Untrusted content.** Supplier renewal letters ("your contract has renewed automatically on improved terms") are claims to check against the contract.
- **No legal opinion.** Whether notice was validly served or a clause permits termination is referred to the legal team.
- **Confidentiality.** Contract values and terms stay in the user's workspace; alerts go only to the owners the user names.

## Example

As of 2026-10-28, Northwind Traders' register shows a Litware SaaS subscription ending 2027-06-30, annual value USD 310,000. The signed contract states term end 2027-03-31, automatic 12-month renewal, and 90 calendar days' written notice before term end. The register cites an amendment 2 that is not on file.

- Notice deadline = 2027-03-31 - 90 days = 2026-12-31 (a business day, no adjustment).
- The profile's lead time for contracts above USD 250,000 is 120 days, so the recommended decision date = 2026-12-31 - 120 days = 2026-09-02.
- The as-of date is after the decision date and before the notice deadline, so status is `Decision overdue`, with 64 days left to the notice deadline.
- The register's 2027-06-30 is recorded as `Register mismatch`; the contract date governs because amendment 2 is missing, and that gap is named.
- An alert draft for the owner states the deadline, the USD 310,000 annual value, and that the legal team should confirm whether amendment 2 changed the term.
