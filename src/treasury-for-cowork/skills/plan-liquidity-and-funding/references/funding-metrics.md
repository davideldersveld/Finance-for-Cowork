# Funding metrics and option comparison

All inputs come from term sheets, credit agreements, the debt register, the forecast or the user. Label indicative pricing as indicative.

## Liquidity measures

| Measure | Formula |
|---|---|
| Undrawn committed availability | Commitment − Drawn − Letters of credit issued − Swingline outstanding |
| Borrowing base availability (asset-based facilities) | min(Commitment, Borrowing base per latest certificate) − Drawn − Letters of credit − Reserves imposed by agent |
| Covenant capacity (maximum leverage test) | Max ratio × Covenant EBITDA − Covenant debt (net or gross per the agreement) |
| Usable headroom | min(Undrawn availability, Borrowing base availability, Covenant capacity) |
| Committed liquidity | Usable cash + Undrawn committed availability |
| Usable liquidity | Usable cash + Usable headroom |
| Runway month | First month where projected usable liquidity < Minimum liquidity |

Facilities expiring inside the horizon drop out of availability from their expiry date. Springing covenants (tested only above a utilization trigger) are modeled on the trigger the agreement states.

## Runway status

| Status | Rule (thresholds from the profile or user) |
|---|---|
| Adequate | No month below minimum within the horizon |
| Watch | First breach falls after the watch window |
| Shortfall | First breach falls within the watch window |

## Cost of an option

- Base rate: forward curve or fixed rate the user supplies, with source and date. If only a spot rate is supplied, say so and hold it flat.
- `All-in drawn cost (annual, simple) = Base rate + Margin + Upfront fee ÷ Expected life in years + Annual agency and other fees ÷ Average drawn amount`.
- `Undrawn cost (annual) = Commitment fee rate × Average undrawn amount`; where the agreement sets the commitment fee as a percentage of margin, compute it from the applicable grid level.
- Utilization fees: apply the tier the forecast utilization falls into.
- Bonds and private placements: `All-in cost = Yield to maturity at issue price + Issue costs amortized over the expected life`, or an effective-rate calculation in code when cash flows are irregular.
- Original issue discount: treat as an upfront cost over the expected life.
- State the day-count convention used for each instrument (for example ACT/360 for SOFR-based loans, ACT/365 for SONIA-based loans) as given in the documents.

## Comparison rows (one column per option)

| Row | What to record |
|---|---|
| Instrument and market | Bank loan, revolver, term loan A or B, bond, private placement, commercial paper, receivables finance |
| Amount and currency | As per term sheet |
| Tenor and amortization | Final maturity, scheduled repayments |
| Base rate and floor | Reference rate, floor |
| Margin or coupon | Fixed or grid; current grid level |
| Fees | Upfront, commitment, utilization, agency, ticking |
| All-in drawn cost | Formula above |
| Undrawn cost | Formula above |
| Prepayment flexibility | Prepayable at par, soft call, make-whole, non-call period |
| Covenant package | Maintenance or incurrence; ratios and levels |
| Security and guarantees | Secured or unsecured; guarantor coverage |
| Pro forma covenant impact | Ratio after the transaction, computed with the agreement's definitions via the covenant workpaper |
| Execution time and certainty | Stated timeline; commitment status |
| Rating and disclosure considerations | As stated by the user or advisers |
| Source | Term sheet name and date |

No ranking, scoring or recommended option. Where the user asks "which is best", restate the trade-offs and note that the decision rests with the treasurer and board.

## Maturity wall checks

- Sum of maturities across years equals principal outstanding in the register.
- Revolver commitments are shown as commitment expiries, separately from drawn principal.
- Any maturity within 12 months after the next balance sheet date is flagged for classification review by Controllership.
