# Receivables metric definitions

All metrics use one AR basis, stated on the About sheet: gross trade receivables (open invoices less open credit notes), excluding unapplied cash and customer credit balances, in reporting currency at the profile's rate. If AR includes sales tax or VAT, credit sales must include it too (and vice versa). Credit sales exclude cash sales and intercompany sales unless the user says otherwise. Days are calendar days.

Notation: `AR_end` closing AR; `AR_open` opening AR; `CurAR_end` closing current (not past due) AR; `S_m` credit sales invoiced in month m; `D_m` calendar days in month m; `S_period` credit sales in the reporting period; `D_period` calendar days in the period.

## DSO — count-back method

Measures how many days of the most recent sales are still sitting in AR.

```
R = AR_end ; DSO = 0 ; m = last month of the period
while R > 0:
    if no sales history for month m: DSO = Not computable (insufficient sales history); stop
    if R >= S_m: DSO = DSO + D_m ; R = R - S_m ; m = previous month
    else:        DSO = DSO + (R / S_m) x D_m ; R = 0
```

- A month with zero or negative credit sales is consumed in full (its days added) and the next earlier month is used; flag it.
- Report to 1 dp. Show the months consumed and the partial fraction on the DSO sheet with live formulas.

Worked check: AR_end 1,500; March sales 800 (31 days); February 600 (28 days); January 700 (31 days). 1,500 - 800 = 700; 700 - 600 = 100; 100 / 700 x 31 = 4.4. DSO = 31 + 28 + 4.4 = 63.4 days.

## DSO — simple average method

Measures average AR relative to average daily sales over the period.

```
Average AR = mean of the AR balances at the opening date and each month end in the period
             (for one month: (AR_open + AR_end) / 2; for a quarter: four points)
DSO (simple average) = Average AR / S_period x D_period
```

If the user's method of record uses closing AR instead of average AR, label it `DSO (period-end balance)`: `AR_end / S_period x D_period`. Never mix variants across periods in a trend.

## Best possible DSO (BPDSO)

Same method as the headline DSO, applied to current AR only:

- Count-back basis: run the count-back algorithm with `R = CurAR_end`.
- Simple average basis: `Average current AR / S_period x D_period`, with average current AR built from the same balance points.

## Average days delinquent (ADD)

`ADD = DSO - BPDSO`, both on the same method and period. Compute from unrounded values.

## Collection effectiveness index (CEI)

```
CEI = (AR_open + S_period - AR_end) / (AR_open + S_period - CurAR_end) x 100
```

- Numerator: amount removed from AR during the period. Denominator: amount that was collectible during the period (everything except what is still current at period end).
- Credit notes and write-offs reduce `AR_end` and therefore inflate the numerator. Always disclose them and show `Adjusted CEI = (AR_open + S_period - AR_end - Credit notes - Write-offs) / (AR_open + S_period - CurAR_end) x 100`.
- 100% means every collectible amount was collected; report to 1 dp.

## Past-due percentage

`Past-due % = (AR_end - CurAR_end) / AR_end x 100`, and per bucket `Bucket balance / AR_end x 100`. Show undisputed and disputed past due separately.

## Aging movement and roll rates

- Buckets from the profile (for example Current, 1-30, 31-60, 61-90, 91-120, over 120 days past due).
- `Roll rate (b to b+1) = Closing balance in bucket b+1 that was in bucket b at opening / Opening balance in bucket b`. With invoice-level data, trace invoices; with bucket totals only, label `Approximate`.

## AR roll-forward

`AR_open + S_period - Cash applied - Credit notes - Write-offs +/- Other adjustments = AR_end`. Other adjustments must be itemized; an unexplained difference is shown.

## Dispute metrics

- Opened, closed and open at end: count and amount.
- `Cycle time = Date resolved - Date raised` for cases closed in the period; median and mean.
- `Disputed share of AR = Open disputed amount / AR_end x 100`.

## Reserve inputs (per the user's policy)

- Provision matrix: `sum over buckets (Bucket balance excluding specifically reserved items x Policy loss rate)`.
- Specific reserves: named accounts and amounts per policy criteria, with evidence.
- `Indicated reserve = Matrix reserve + Specific reserves`; `Difference = Indicated reserve - Booked reserve`.
- Loss rates and forward-looking adjustments come from policy; the estimate under ASC 326 or IFRS 9 (simplified approach, IFRS 9.5.5.15) is the controller's.
