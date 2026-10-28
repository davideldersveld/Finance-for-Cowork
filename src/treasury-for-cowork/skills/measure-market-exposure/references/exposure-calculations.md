# Exposure calculations

## Sign convention

Positive exposure = long the foreign currency (more assets or inflows than liabilities or outflows). Hedges that sell the foreign currency forward carry negative notional against a long exposure. State the convention at the top of every sheet.

## FX exposure types

| Type | Definition | Where the effect lands |
|---|---|---|
| Balance sheet (remeasurement) | Monetary items denominated in a currency other than the entity's functional currency | Earnings, as the items are remeasured at closing rate (ASC 830 / IAS 21) |
| Forecast transaction | Forecast foreign-currency receipts and payments not yet on the balance sheet | Future cash flows and margins |
| Net investment (translation) | Net assets of a foreign operation with a functional currency different from the reporting currency | Other comprehensive income (cumulative translation adjustment) |

## Tenor buckets

Use the policy's buckets. If the policy is silent and the user agrees, a common presentation is 0-3, 4-6, 7-12 and 13-24 months; label it as presentation only, with no band attached.

## Hedge ratio and band tests

- `Hedge ratio = Hedged notional ÷ Net forecast exposure` (both in the foreign currency, same bucket).
- `Within band` if Lower ≤ Ratio ≤ Upper.
- `Below band` if Ratio < Lower; `Gap = Lower × Exposure − Hedged`.
- `Above band` if Ratio > Upper or Ratio > 100 percent; `Excess = Hedged − Upper × Exposure`.
- Where exposure is zero or has the opposite sign to the hedge, report the ratio as "n/a" and label `Above band` if any hedge exists.

## Interest-rate measures

| Measure | Formula |
|---|---|
| Net floating notional | Floating-rate debt − Pay-fixed swap notional + Receive-fixed swap notional − Floating-rate assets (if the policy allows offset) |
| Fixed proportion | (Fixed-rate debt + Pay-fixed swaps − Receive-fixed swaps) ÷ Total debt |
| First-year interest impact of a parallel shock | Net floating notional × Shock × (Months from next reset to 12 ÷ 12), summed per instrument |
| Floor effect | For a downward shock, the base rate cannot fall below the floor; impact = Notional × (max(Base − Shock, Floor) − Base) |
| Repricing gap | Notional repricing in each bucket (by next reset date for floating, maturity for fixed) |

## Scenario method

1. Use shocks from the policy or the user (for example FX ±10 percent; rates ±100 basis points parallel).
2. FX impact in functional currency: `Net open position (foreign currency) × Shock × Spot rate`.
3. Report remeasurement (earnings) and forecast transaction (cash flow) impacts separately; do not add them to net investment effects.
4. Hedges: the change in hedge value offsets the hedged exposure to the extent of hedged notional; the open position carries the impact.
5. State every result as linear, before tax, holding other variables constant, at the stated spot rate and date.

## Status vocabulary

| Status | Meaning |
|---|---|
| Within band | Policy test met |
| Below band | Hedged less than the policy minimum |
| Above band | Hedged more than the policy maximum or more than the exposure |
| No policy band | Policy does not set a band for this pair or bucket |
| Not testable | Exposure, hedge or rate data missing |
