# Finance Profile — section structure (schema version 1)

This file defines the exact shape of `Finance-Profile.md`, the file saved in the user's Cowork folder in OneDrive. Every Finance skill in every Finance for Cowork plugin reads this file by section heading and row key. Keep headings, section numbers, table columns and row keys exactly as written here so consuming skills can rely on them. Add rows; never rename or reorder sections.

## Conventions that apply to every section

- **Value status.** Every value row carries a Status column with one of three labels:
  - `Confirmed` — the user stated or approved the value, or it was read from a cited policy document and the user accepted it.
  - `Provisional` — proposed from a document or prior practice but not yet confirmed by the user. Consuming skills may use a Provisional value only after telling the user they are doing so.
  - `Not provided` — the user has not supplied the value. Consuming skills must treat this as missing and ask for the value they need; they never substitute a default.
- **Amounts.** Always state the amount, the currency (ISO 4217 code) and the unit (units, thousands, millions). Never write a bare number.
- **Percentages.** Written as a percent with up to two decimals, e.g. `5.00%`.
- **Combination rule.** Where a threshold has both an amount and a percentage, the Rule column states `AND` (both must be exceeded) or `OR` (either exceeded). No rule is ever implied.
- **Locations.** A location is a OneDrive or SharePoint link, or a site/library/folder path the user can open, plus the file name. Never a local desktop path.
- **People.** Named by full name and role, with a work contact channel (work email or Teams). Roles are preferred to names where a policy is role-based.
- **Dates.** ISO format `YYYY-MM-DD`.

## Data the profile must never contain

The profile stores thresholds, structures and locations only. Never record, even if the user offers them:

- bank account numbers, IBANs, sort codes, routing numbers, card numbers;
- tax identification numbers of any kind (EIN, VAT registration, national IDs);
- salaries, bonuses or compensation of identifiable individuals;
- passwords, tokens, system credentials, security answers;
- home addresses, personal phone numbers, health or other special-category data.

If such data appears in a source document used to pre-fill the profile, skip it and record only where the authoritative register is kept (for example, "Bank account inventory — Treasury site, Bank Accounts library").

---

## Section 0. Profile header

| Key | Value | Status |
|---|---|---|
| Organization name | | |
| Profile owner (name, role) | | |
| Schema version | 1 | Confirmed |
| Profile version | e.g. 1.0 | |
| Created on | YYYY-MM-DD | |
| Last updated on | YYYY-MM-DD | |
| Default output language | e.g. US English | |
| Default number presentation | e.g. USD thousands, negatives in parentheses | |

## Section 1. Entities

| Entity code | Legal name | Country | Functional currency | Ledger / ERP | Consolidation parent | Ownership % | Consolidation method | In scope | Status |
|---|---|---|---|---|---|---|---|---|---|

- Consolidation method: Full / Equity method / Proportionate / Not consolidated.
- In scope: Yes / No (No keeps a dormant or divested entity on record).

## Section 2. Currencies and rates

### 2.1 Currency roles

| Key | Value | Status |
|---|---|---|
| Group reporting (presentation) currency | ISO code | |
| Additional reporting currencies | ISO codes | |
| Default presentation unit | units / thousands / millions | |

### 2.2 Rate sources by rate type

| Rate type | Use | Rate source (provider or internal table) | Location | Rate date convention | Quotation convention | Status |
|---|---|---|---|---|---|---|
| Closing (spot) | Balance sheet translation | | | e.g. last business day of fiscal period | e.g. units of reporting currency per 1 foreign | |
| Period average | Income statement translation | | | e.g. monthly simple average of daily closing | | |
| Historical | Equity and non-monetary items | | | rate at transaction date | | |
| Budget / plan | Constant-currency and plan comparisons | | | fixed for fiscal year | | |

## Section 3. Fiscal calendar

| Key | Value | Status |
|---|---|---|
| Fiscal year start (month and day) | | |
| Period pattern | Calendar months / 4-4-5 / 4-5-4 / 5-4-4 / 52-53 week | |
| Week end day (week-based calendars only) | | |
| 53rd week rule and next 53-week year | | |
| Periods per year (including adjustment periods) | e.g. 12 + 1 adjustment | |
| Period naming convention | e.g. FY27-P01 | |
| Current fiscal year label and dates | | |
| Quarter end periods | e.g. P03, P06, P09, P12 | |

## Section 4. Close calendar

| Key | Value | Status |
|---|---|---|
| Workday convention | e.g. WD1 = first business day after period end; WD-1 = last business day of period | |
| Holiday calendar used | name and location | |
| Close tracker location | | |
| Subledger cutoff | e.g. WD-1 | |
| AP invoice cutoff | | |
| Intercompany cutoff and agreement deadline | | |
| Accruals and journals deadline | | |
| Balance sheet reconciliations due | | |
| Flux analysis due | | |
| Ledger hard close | | |
| Management reporting package due | | |
| Quarter-end and year-end differences | | |

## Section 5. Chart of accounts and mapping

| Key | Value | Status |
|---|---|---|
| Chart of accounts location | | |
| Account-to-reporting-line mapping location | | |
| Mapping levels | e.g. Account > FS line > FS caption > Segment | |
| Account ranges by type | e.g. 1xxxx assets, 2xxxx liabilities, 3xxxx equity, 4xxxx revenue, 5xxxx-8xxxx expense | |
| Ledger sign convention | e.g. debit positive, credit negative | |
| Cost centre and segment structure location | | |
| Intercompany account range or flag | | |

## Section 6. Materiality and tolerance thresholds by process

One row per process threshold. Keys are stable; consuming skills look rows up by Key.

| Key | Process | Threshold | Amount | Currency and unit | Percent | Rule | Aging limit (days) | Applies to | Source policy and clause | Approved by (role) | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|
| REC-01 | Reconciliation | Reconciling item requiring individual explanation | | | | | | | | | |
| REC-02 | Reconciliation | Unexplained difference tolerance at sign-off | | | | | | | | | |
| REC-03 | Reconciliation | Aged reconciling item escalation | | | | | e.g. 60 | | | | |
| FLX-01 | Flux | Balance sheet movement requiring explanation | | | | AND / OR | | | | | |
| FLX-02 | Flux | Income statement movement requiring explanation | | | | AND / OR | | | | | |
| APM-01 | AP match | Price variance tolerance per line | | | | AND / OR | | | | | |
| APM-02 | AP match | Quantity variance tolerance per line | | | | | | | | | |
| APM-03 | AP match | Invoice total variance tolerance | | | | | | | | | |
| CSH-01 | Cash application | Auto-match tolerance (amount difference accepted) | | | | | | | | | |
| CSH-02 | Cash application | Small-balance write-off limit | | | | | | | | | |
| CSH-03 | Cash application | Unapplied cash aging escalation | | | | | e.g. 30 | | | | |
| COV-01 | Covenant | Headroom warning level | | | | | | per covenant or all | | | |
| KPI-01 | KPI RAG | Default red/amber/green rule | | | | | | | | | |
| TIE-01 | Tie-out | Rounding and presentation tolerance | | | | | | | | | |
| ICO-01 | Intercompany | Mismatch tolerance per entity pair | | | | | | | | | |
| FXR-01 | FX rates | Acceptable difference between two rate sources | | | | | | | | | |
| MAT-01 | Reporting | Overall materiality used by management (if the user states one) | | | | | | | | | |

KPI RAG detail (KPI-01) is written as an explicit rule, for example: "Green = at or better than target; Amber = worse than target by up to 5.00%; Red = worse than target by more than 5.00%; polarity per KPI definition". Covenant warning (COV-01) states whether headroom is measured as a percent of the covenant level or of the metric.

Add rows with the next number in the same family (e.g. REC-04) when the user has further thresholds. Overall materiality for audit or ICFR scoping is recorded only if the user states it; the profile never computes it.

## Section 7. Approval limits (delegation of authority)

| Transaction type | Approver role | Limit amount | Currency and unit | Second approval required above | Source document and clause | Status |
|---|---|---|---|---|---|---|

Typical transaction types: manual journal entry, payment release, purchase order or requisition, contract signature, credit limit, customer credit note or write-off, supplier master data change, capital expenditure, expense report, intercompany settlement, investment or hedge trade. Limits are listed in ascending order within each transaction type. Roles, not individuals.

## Section 8. Policy and working-document locations

| Document | Owner (role) | Location | Version or effective date | Next review date | Status |
|---|---|---|---|---|---|

Typical documents: accounting policy manual, delegation of authority, close policy and calendar, balance sheet reconciliation policy, capitalization and fixed asset policy, revenue recognition policy, travel and expense policy, procurement policy, credit and collections policy, treasury policy, investment policy, hedging policy, tax policy, transfer pricing policy, intercompany policy, record retention policy, disclosure checklist, FX rate table, bank account inventory (location only), contract register, close tracker.

## Section 9. Team owners

| Area | Owner (name) | Role | Backup (name, role) | Work contact channel | Status |
|---|---|---|---|---|---|

Typical areas: controller, general ledger, accounts payable, accounts receivable and collections, credit, treasury, tax, FP&A, procurement, internal controls, external reporting, payroll (owner only), systems (ERP), audit liaison.

## Section 10. Version log

| Profile version | Date | Changed by (name, role) | Sections changed | Summary of change | Reason or source |
|---|---|---|---|---|---|

Rows are appended, newest last, and never deleted. Version numbering: initial save is 1.0; any value change is a minor increment (1.1, 1.2); a change to entity structure, fiscal calendar or reporting currency is a major increment (2.0). A version note without a value change does not change the version number and is logged with "Note only" in Sections changed.

---

## Reading contract for consuming skills

1. Look for the profile before asking the user anything. Read only the sections the task needs.
2. Look thresholds up by Key in Section 6; never infer one from another row.
3. Use `Confirmed` values directly and cite them as "Finance Profile v<version>, Section <n>, <Key or row>".
4. For `Provisional` values, tell the user the value is provisional before relying on it.
5. For `Not provided` or missing rows, ask for the value in the skill's single question card; never assume.
6. If the profile's schema version is higher than the version the skill understands, use matching section headings only and mention the mismatch.
7. Consuming skills never write to the profile. Changes go through `set-up-finance-profile`.
