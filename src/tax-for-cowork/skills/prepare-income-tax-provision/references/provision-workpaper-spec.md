# Provision workpaper specification

## Terminology map (use the framework's own terms in each workpaper)

| Concept | ASC 740 (US GAAP) | IAS 12 (IFRS) |
|---|---|---|
| Differences that never reverse | Permanent differences | Non-deductible expenses / non-taxable income (no defined term) |
| Differences that reverse | Temporary differences (book basis vs tax basis) | Temporary differences (carrying amount vs tax base); taxable or deductible |
| Rate to measure deferred tax | Enacted rate expected to apply | Rate enacted or substantively enacted at reporting date, expected to apply |
| Limiting deferred tax assets | Valuation allowance when not more likely than not to be realized | Recognize only to the extent probable that taxable profit will be available |
| Uncertain positions | Unrecognized tax benefits, ASC 740-10 recognition and measurement | Uncertain tax treatments, IFRIC 23 |
| Interim reporting | ASC 740-270 estimated annual effective tax rate | IAS 34 weighted average annual rate |
| Balance sheet presentation | Noncurrent; offset within a tax-paying component and jurisdiction | Offset when legally enforceable right and same authority, per IAS 12 |

Retrieve authoritative text for any paragraph before quoting it; cite topic and paragraph only.

## Sheet columns

- **Pre-tax Income** — Entity, Jurisdiction, TB source (file, sheet, range), Pre-tax book income, Adjustments to reach jurisdiction income, Pre-tax income for provision.
- **Book-Tax Differences** — Entity, Jurisdiction, Item, Account(s), Book amount, Tax amount, Difference, Type (Permanent / Temporary), Source, Status.
- **Current Tax** — Jurisdiction, Pre-tax income, Permanent, Change in temporary, Loss utilization (with cited limit), Taxable income, Rate (Rule ID), Tax before credits, Credits, Return-to-provision, Other, Current tax.
- **Deferred Roll-forward** — Jurisdiction, Item, Opening temporary difference, Closing temporary difference, Rate, Opening deferred tax, P&L movement, OCI, Equity, Business combinations, FX, Rate change effect, Closing deferred tax, Check (Opening + movements − Closing = 0).
- **Recoverability Considerations** — Jurisdiction, Gross deferred tax assets, Evidence item, Positive or Negative, Source, Weight noted by reviewer (blank for reviewer), Status (Review required).
- **ETR Reconciliation** — Line, Amount, Rate effect (Amount ÷ Pre-tax income), Source; final rows Total tax expense, Expected tax, Residual (must be 0).
- **UTP Inventory** — Position ID, Jurisdiction, Periods, Description, Gross amount, Measured liability (user-supplied), Interest, Penalties, Classification policy, Status, Source.
- **Tax Accounts Tie** — Account, TB balance, Workpaper balance, Difference, Status.
- **Rate Table** — Rule ID, Jurisdiction, Rate, Effective from, Enactment status at reporting date, Citation, URL, Retrieval date.

## Core formulas

- `Taxable income = PTBI + Permanent add-backs − Permanent deductions + Increase in deductible temporary differences − Increase in taxable temporary differences − Loss utilization`
- `Current tax = Taxable income x Rate − Credits + RTP + Other`
- `Deferred tax (item) = Closing temporary difference x Rate`
- `Deferred tax expense = Δ net deferred tax liability − Δ net deferred tax asset, excluding OCI, equity, acquisitions and FX`
- `Total tax expense = Current tax + Deferred tax expense`
- `ETR = Total tax expense ÷ PTBI`
- `Foreign rate differential = PTBI(foreign) x (Foreign rate − Home rate)`
- `Return-to-provision = Tax per filed return − Tax per prior-year provision`, split into current and deferred components

## Verification checklist

1. Each entity's TB foots; PTBI agrees to the income statement.
2. Every rate has a citation and enactment status.
3. Deferred roll-forward check column is zero for every item.
4. ETR residual is zero.
5. Current plus deferred equals total tax expense in the TB.
6. Payable or receivable roll-forward agrees to the TB.
7. Every judgement item is labelled Review required with its evidence listed.
