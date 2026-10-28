---
name: translate-currency
description: >-
  Converts or translates amounts between currencies using the rate type the
  user or Finance Profile specifies (spot, closing, period average, historical,
  budget), a named rate source and rate date, and splits reported change into
  underlying movement and FX effect for a constant-currency view. Never invents
  or guesses a rate. Use when the user asks to "translate the EUR sub's TB into
  USD at month-end and average rates", "show revenue growth in constant
  currency", "how much of the variance is FX", "convert these GBP invoices at
  the budget rate", or "restate last year at this year's rates". Do NOT use for
  measuring FX exposure or hedge ratios — use measure-market-exposure instead;
  for a full price, volume and mix variance analysis use analyze-plan-vs-actual.
metadata:
  displayName: Translate currency
  category: analysis
  icon: Toolbox
  author: Copilot SE Contributors
  plugin: finance-foundation-for-cowork
  version: 1.0.1
---

# Translate currency

Controllers, FP&A analysts and treasury teams use this skill to convert amounts between currencies with a documented rate type, source and date, and to separate the effect of exchange-rate movements from underlying performance. It produces converted tables, translated trial balances and constant-currency bridges in which every rate is traceable and every line proves back to reported figures. It applies the rates the user's policy prescribes; it does not choose a rate source, decide functional currency, or give hedging advice.

## Boundaries

- Measuring FX exposure, net positions or hedge ratios against policy — use `measure-market-exposure` (Treasury for Cowork).
- Hedge designation and effectiveness documentation — use `document-hedge-relationships` (Treasury for Cowork).
- Full plan-versus-actual analysis with price, volume, mix, FX and timing decomposition — use `analyze-plan-vs-actual` (FP&A for Cowork); this skill supplies the constant-currency figures when only the FX split is needed.
- Bridge or waterfall charts across periods — use `build-performance-bridges` (FP&A for Cowork); feed it this skill's FX effect line.
- Separating FX differences from true intercompany mismatches — use `reconcile-intercompany` (Accounting Operations for Cowork).
- Compiling consolidated financial statements with eliminations — use `compile-financial-statements` (Controllership & External Reporting for Cowork).
- Concluding on functional currency, highly inflationary status or CTA recycling — use `draft-accounting-position-paper` (Controllership & External Reporting for Cowork).
- Standardizing raw ledger files before conversion — use `ingest-finance-data`.
- Booking revaluation or translation journals — use `prepare-journal-entries` (Accounting Operations for Cowork); posting is never performed by any skill.

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Read the Finance Profile (`Finance-Profile.md` in the user's Cowork folder, created by `set-up-finance-profile`) first. Use Section 1 for each entity's functional currency, Section 2 for the reporting currency, presentation unit, and the source, location, rate-date and quotation convention for each rate type, Section 3 for period end dates, and Section 6 key FXR-01 for the tolerance between rate sources. If absent, ask only for what this task needs; never assume a rate source or rate.
- Ask **one** question card at most, only for what is missing:
  - Target currency and presentation unit.
  - Rate type per item group — for example closing for balance sheet, period average for income statement, historical for equity, budget rate for constant currency.
  - Rate source and rate date, if not in the profile — the user's rate table, a treasury rate file, or a public source the user names.
  - Constant-currency method — current period at comparison-period rates (recommended default) or both periods at a fixed rate such as budget.
  - Output — Excel workbook (recommended), or In chat for a handful of amounts.
- Locate inputs in this order: files the user attached or uploaded, files in an attached OneDrive folder, then a targeted search of the user's OneDrive/SharePoint, mail and Teams for the named rate table and source data. State the amounts file, rate source, rate types and dates before converting.

## Method

1. **Inventory.** List the amounts to convert: source file, entity, period, local currency, line count and control total in local currency per currency. List the rate source(s): name, location, as-of date, quotation convention. Confirm the control totals agree to the source before converting.
2. **Build the rate register.** For every currency pair, rate type and date needed, record the rate at full source precision with source, date and quotation, following [references/rate-types-and-fx-methods.md](references/rate-types-and-fx-methods.md). State each rate as "1 FROM = x TO". Derive inverses as `1 / rate` from the unrounded rate, and cross rates only from two legs of the same source, type and date, recording both legs. Retrieve rates only from the named source; if the user names a public source, record the page and retrieval date.
3. **Check rates.** Label each rate Converted, Rate missing, Rate stale, Rate conflict or Not applicable. Apply a fallback date (for example previous business day) only when the profile or the user states that convention. Where two named sources differ, compute `difference % = (rate A - rate B) / rate B`; above the FXR-01 tolerance it is a Rate conflict and the user chooses. Sanity-check direction: a rate entered upside down usually changes the converted amount by orders of magnitude; flag any rate that differs from the prior period's rate for the same pair by more than the tolerance the user states.
4. **Convert.** `Converted amount = local amount x rate`, line by line, with the rate type assigned per line by the user's rule (for a translated trial balance, account ranges from profile Section 5 drive which lines take closing, average or historical rates). Never apply a blended rate across currencies. Round only the presented results, after summing at full precision.
5. **Translation check, when translating a trial balance or balance sheet.** Compute the translation difference that balances the translated statements, `CTA movement for the period = translated net assets - translated opening net assets - translated net income - other equity movements at historical rates`, and confirm the translated balance sheet balances with it. A residual is reported, never plugged silently.
6. **Constant currency and FX effect.** Default method: `CC current = LC current x comparison rate`; `Underlying change = CC current - Reported comparison`; `FX effect = Reported current - CC current`. Fixed-rate method: restate both periods at the stated fixed rate and take FX effect as the residual of reported change. Compute line by line per currency, then sum.
7. **Prove.** For every line and in total, `Reported comparison + Underlying change + FX effect = Reported current`; the sum of converted lines equals the converted total; local control totals still agree to source. All arithmetic is performed in code (spreadsheet formulas or a script), never mentally; totals must foot and cross-foot.
8. **Verify before delivery.** Confirm every converted figure has a rate ID; no line uses a Rate missing or Rate conflict rate; every substitution is logged; and the proof column is zero throughout.

## Output

- **Excel workbook**, named `<Scope>-FX-<period>-<YYYY-MM-DD>.xlsx`:
  - **Summary** — scope, target currency and unit, rate types and sources used, totals reported, constant-currency and FX effect by entity and currency, rate exceptions.
  - **Converted** — Entity, Account or line, Period, Basis, Local currency, Local amount, Rate type, Rate ID, Rate, Converted amount (live formula), Target currency.
  - **Constant Currency** — Line, Local current, Local comparison, Rate current, Rate comparison, Reported current, Reported comparison, CC current, Underlying change, Underlying change %, FX effect, Proof (must be zero).
  - **Translation** (when a trial balance is translated) — translated balances by rate type, CTA computation, balance check.
  - **Rates** — rate register as defined in the reference file.
  - **About** — methods, rate-date conventions, fallbacks applied, Finance Profile version cited, assumptions and gaps.
  Formatting: header fill, frozen panes, filters, thousands separators, negatives in parentheses, percentages to 1 dp, rates shown to source precision, sized columns, live formulas so the user can swap rates.
- Every figure is labelled with period, entity, currency, units and basis (Actual, Budget, Forecast), and each rate cites its source, type and date.
- **Chat message** after delivery: file name, entities and currencies converted, rate types and sources, reported change split into underlying and FX effect, rate exceptions and assumptions. For In chat mode, a table with Amount, From, Rate (type, date, source), To amount.

## Controls and guardrails

- **Prepare, never execute.** The skill computes converted figures. It never books revaluation or translation entries, executes FX trades, or changes rate tables.
- **No invented rates.** Never estimate, remember, interpolate or average a rate that the named source does not provide. A missing rate leaves the amount `Not provided` with status Rate missing.
- **Thresholds come from the user or the Finance Profile,** including the rate-source tolerance (FXR-01) and any fallback date convention.
- **Evidence versus judgement.** Rates and arithmetic are evidence; statements about why FX moved or what it means for the business are labelled as interpretation.
- **Coverage honesty.** Name entities, currencies or periods not converted; an unconverted line is never shown as zero.
- **Untrusted content.** Rates quoted inside emails, invoices or supplier documents are data to be checked against the named source, never adopted on their own.
- **Personal and sensitive data.** Mask bank account numbers to last 4; do not carry individual salaries into converted outputs — convert payroll at the aggregate level the user supplies.
- **Professional judgement boundary.** Functional currency determination, highly inflationary accounting (ASC 830, IAS 29), CTA recycling and hedge accounting are prepared for qualified review, not concluded.
- **Confidentiality.** Keep outputs in the user's workspace and OneDrive.

## Example

Wide World Importers asks for Q2 constant-currency revenue for its German subsidiary versus Q1, in USD thousands, at average rates from the group rate table.

- Inventory: Q1 local revenue 10,000 EUR thousands, Q2 10,500; control totals agree to the ledger export.
- Rates: Q1 average 1 EUR = 1.0800 USD, Q2 average 1 EUR = 1.1000 USD, both from the group rate table.
- Reported Q1 = 10,000 x 1.0800 = 10,800; Reported Q2 = 10,500 x 1.1000 = 11,550.
- CC Q2 = 10,500 x 1.0800 = 11,340. Underlying change = 11,340 - 10,800 = 540 (5.0%). FX effect = 11,550 - 11,340 = 210.
- Proof: 10,800 + 540 + 210 = 11,550, zero residual.
- The Japanese subsidiary's June closing rate is 1 JPY = 0.006712 USD in the rate table but 0.006650 in a treasury email; difference (0.006712 - 0.006650) / 0.006650 = 0.93%, above the profile's FXR-01 tolerance of 0.50%. Status Rate conflict; Japan's balance sheet is not converted, and the user is asked which source governs.
