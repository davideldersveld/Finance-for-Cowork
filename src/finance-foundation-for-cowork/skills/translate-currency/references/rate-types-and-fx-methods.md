# Rate types, conversion conventions and FX-effect formulas

## Rate types

| Rate type | Typical use | Rate date |
|---|---|---|
| Spot (transaction) | Converting a single transaction or payment on its date | The transaction date, or the date the user names |
| Closing | Translating balance sheet assets and liabilities at period end | Last business day of the fiscal period per the Finance Profile, or the convention recorded there |
| Period average | Translating income and expense where rates do not fluctuate significantly within the period | The period; the averaging method (simple daily, monthly average of daily, weighted) is stated |
| Historical | Equity balances, and non-monetary items under remeasurement | The date of the original transaction (capital contribution, asset acquisition) |
| Budget or plan | Constant-currency comparisons and plan rates | Fixed for the plan year as recorded |

The Finance Profile Section 2.2 records the source, location, rate date convention and quotation convention for each type. The skill uses that record or the user's statement; it never selects a provider on its own.

## Quotation conventions

- State every rate as "1 FROM = x TO" and keep the source's quotation alongside, e.g. source "EUR/USD 1.0850" means 1 EUR = 1.0850 USD.
- Inverse: `rate(TO->FROM) = 1 / rate(FROM->TO)`; keep full precision, never invert a rounded rate when the unrounded one is available.
- Cross rate through a base currency B: `rate(X->Y) = rate(X->B) x rate(B->Y)`, or `rate(X->B) / rate(Y->B)`. Both legs must come from the same source, rate type and date; record the legs.
- Keep rates at source precision (commonly 4 to 6 decimals, more for high-unit currencies such as JPY, KRW, IDR). Round only the presented converted amounts.
- Watch minor-unit conventions (JPY and KRW have 0 decimals; KWD, BHD and OMR have 3) and quote-per-100 conventions some sources use for high-unit currencies.

## Translation (current-rate approach) — framework reference only

Under US GAAP ASC 830 and IFRS IAS 21, a foreign operation's results are generally translated from functional to presentation currency with assets and liabilities at the closing rate, income and expense at transaction-date rates (an average rate is a permitted approximation when rates do not fluctuate significantly), and equity at historical rates; the difference is the cumulative translation adjustment in other comprehensive income. Remeasurement of foreign-currency monetary items into the functional currency, and the temporal approach for an entity whose books are not in its functional currency, follow different rules. Determining functional currency, hyperinflationary status (ASC 830 highly inflationary; IAS 29) and CTA recycling are accounting judgements; the skill applies the rate types the user specifies and does not decide them. Retrieve authoritative text when a treatment question arises.

### Translation check

For a translated trial balance or balance sheet:

`CTA (period movement) = translated net assets at closing rate - translated opening net assets - translated net income at average rate - other equity movements translated at historical rates`

The translated balance sheet must balance after including the CTA line; compute this in code and report any residual.

## Constant-currency and FX-effect formulas

Notation per line item, current period C and comparison period P (prior period, prior year or plan):

- `LC_C`, `LC_P` — amounts in local (functional) currency.
- `r_C`, `r_P` — rates (local to presentation) for each period, of the type stated.
- `Reported_C = LC_C x r_C`; `Reported_P = LC_P x r_P`.

Constant-currency method A (current at comparison rates — the default unless the user or profile states otherwise):

- `CC_C = LC_C x r_P`
- `Underlying change = CC_C - Reported_P = (LC_C - LC_P) x r_P`
- `FX effect = Reported_C - CC_C = LC_C x (r_C - r_P)`
- `Underlying change % = (CC_C - Reported_P) / |Reported_P|`

Constant-currency method B (both periods at a fixed rate R such as the budget rate):

- `CC_C = LC_C x R`; `CC_P = LC_P x R`
- `Underlying change = CC_C - CC_P`
- `FX effect = (Reported_C - Reported_P) - (CC_C - CC_P)`

Proof (must hold to the cent for every line and in total, computed in code):

`Reported_P + Underlying change + FX effect = Reported_C`

Sum of line-level FX effects must equal the total-level FX effect; if a group total is converted from summed local amounts across several currencies, compute FX effect line by line per currency and add, never with a blended rate.

## Rate status labels

| Status | Rule |
|---|---|
| Converted | Rate found from the named source, type and date |
| Rate missing | No rate for the currency pair, type or date in the named source; amount not converted and shown as `Not provided` |
| Rate stale | Nearest available rate date differs from the required date (for example, required month-end is a holiday and the source has no rate); the rate is used only if the user's or profile's rate-date convention allows the fallback (such as previous business day), and the substitution is logged |
| Rate conflict | Two named sources differ by more than the Finance Profile Section 6 FXR-01 tolerance (or the user's tolerance); the skill does not choose, it asks |
| Not applicable | Amount already in the target currency (rate 1.0 recorded explicitly) |

## Rate register columns (sheet "Rates")

Rate ID, From currency, To currency, Rate (full precision), Quotation as in source, Rate type, Rate date, Source name, Source location or document + page, Retrieved on, Inverse or cross (legs), Status.
