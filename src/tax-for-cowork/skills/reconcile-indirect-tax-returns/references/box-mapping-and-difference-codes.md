# Box mapping and difference codes

## Building the box map

1. Start from the user's existing map or the compliance provider's mapping. If neither exists, retrieve the authority's official return guidance for the return version in use, cite title, section and URL with retrieval date, and list each box with its definition in the user's words.
2. For each box record: box or line ID, net or tax, tax codes feeding it, GL accounts, sign convention (output positive, input positive or negative as the return expects).
3. Every tax code active in the period must map to at least one box or be marked Out of scope with a reason. Report unmapped tax codes as `Not provided`.
4. For US sales and use tax, the "box" is the line on the state return per jurisdiction (state, county, city, district) where the return is filed at that level.

## Difference codes

| Code | Meaning | Evidence required | Typical treatment for the preparer |
|---|---|---|---|
| Timing | Tax point, invoice date and posting date fall in different periods | Invoice date, posting date, tax point rule cited | Include in the period the cited rule dictates; note the reversing period |
| Rate | Reported tax differs from Net x cited rate beyond tolerance | Rate source, line listing | Route line-level cause to validate-transaction-tax-treatment |
| Exempt | Supply classified exempt, zero-rated or out of scope inconsistently with the map | Tax code, product category, certificate where relevant | Correct mapping or coding; list for review |
| Reverse charge | Self-accounted output and input not both recorded, or recorded in different boxes | Supplier invoice, self-assessment entry | Both sides must appear; input limited by recovery position |
| Non-recoverable | Restricted input tax left in the input tax account, or recoverable tax expensed | Recovery calculation, blocked-cost list | Reclassify between input tax and expense |
| Manual journal | Entry posted to a tax account outside the tax engine | Journal number, preparer, support | Decide whether it belongs on the return |
| Prior-period correction | Error from an earlier period corrected in this one | Original return, correction support, any cited correction rule | Follow the cited correction method; list for review |
| FX | Translation of foreign-currency invoices or of the return itself | Rate type, rate source, rate date | Use only the rate the user or cited rule specifies |
| Rounding | Line or box rounding | Calculation | Accept within tolerance only |
| Bad debt relief | Output tax adjusted for unpaid debts | Debt aging, cited relief conditions | List conditions met and not met |
| Unexplained | No evidence-backed cause | None | Stays open; blocks Ready for review |

## Formulas

- `D1 = Return amount − Transaction report amount`
- `D2 = Transaction report amount − GL amount`
- `Total difference = D1 + D2 = Return amount − GL amount`
- `Expected tax = Net x Rate`; `Rate difference = Reported tax − Expected tax`
- `Recoverable input tax = Fully recoverable input tax + Mixed-cost input tax x Recovery rate`
- `Over or under collection = Tax collected − Tax due`
- `Closing liability = Opening + Output tax − Recoverable input tax +/- Adjustments − Payments + Refunds`

## Status rules

- Agrees: difference = 0.00.
- Within tolerance: 0 < absolute difference <= tolerance from profile or user.
- Explained difference: every component carries a difference code and evidence reference, and the explained components sum to the difference.
- Unexplained difference: any residual without evidence.
- Not provided: a required source or mapping is missing.
