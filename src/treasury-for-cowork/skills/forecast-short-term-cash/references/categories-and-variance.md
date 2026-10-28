# 13-week forecast — categories, rules and variance

## Default category tree

Use the user's template when one exists. Otherwise use this structure; each line keeps its basis tag.

| Section | Line | Typical source | Default basis |
|---|---|---|---|
| Operating receipts | Customer collections — existing receivables | AR aging, expected-receipts schedule | Modeled |
| Operating receipts | Customer collections — future billings | Sales forecast lagged by terms and days late | Modeled |
| Operating receipts | Other operating receipts (rebates, royalties, refunds) | Contract or notice | Contractual / Management input |
| Operating disbursements | Suppliers — open payables | AP aging mapped to run calendar | Scheduled |
| Operating disbursements | Suppliers — not yet invoiced | Open purchase orders, run-rate | Modeled |
| Operating disbursements | Payroll — net pay | Payroll calendar | Scheduled |
| Operating disbursements | Payroll taxes and benefits | Remittance calendar | Scheduled |
| Operating disbursements | Rent and leases | Lease schedule | Contractual |
| Operating disbursements | Indirect taxes (VAT, GST, sales and use) | Tax calendar | Scheduled |
| Non-operating | Income tax payments | Tax calendar | Scheduled |
| Non-operating | Capex — committed | Purchase orders | Contractual |
| Non-operating | Capex — uncommitted | Capex plan | Management input |
| Non-operating | Intercompany settlements | Settlement plan | Scheduled |
| Non-operating | FX and derivative settlements | Deal tickets | Contractual |
| Financing | Interest and fees | Debt register | Contractual |
| Financing | Scheduled principal | Debt register | Contractual |
| Financing | Contracted draws or repayments | Signed notice | Contractual |
| Financing | Dividends and buybacks | Board approval | Contractual |

## Receipt timing rules

- Customer-level: `Payment date = Due date + Average days late`, where average days late is the weighted average over the trailing period the user names (weight = invoice amount).
- Bucket-level collection curve, when history is thin: percentage of each aging bucket collected in each forward week; the curve and its source period are recorded in the assumptions register and must sum to no more than 100 percent per bucket.
- Exclusions: disputed items, items referred for escalation and items on payment plans are removed from the curve and forecast only from the plan or promise schedule.
- Future billings: `Billing week + Payment terms + Average days late`.

## Disbursement timing rules

- Open payables go to the last payment run on or before the due date (or the first run after, if the profile's payment policy says pay-after-due).
- Discounts: include only if the payment proposal takes them; the amount is net of discount.
- Weekends and bank holidays roll per the payment calendar's business-day convention.

## Liquidity status

| Status | Rule |
|---|---|
| Above minimum | Measure ≥ Minimum + Buffer |
| Within buffer | Minimum ≤ Measure < Minimum + Buffer |
| Below minimum | Measure < Minimum |

Apply separately to ending cash and to liquidity when the profile sets both minimums.

## Variance classification

| Class | Test | Treatment in the roll |
|---|---|---|
| Timing | The item is still expected, in a later week, at the same amount | Move to the new week; reverses over the horizon |
| Permanent | The item will not occur or occurred at a different amount that will not be recovered | Remove or adjust; no reversal |
| New item | Not in last week's forecast | Add with basis tag; investigate why it was missed |

Rules:
- Split a variance when part is timing and part permanent; parts must sum to the total variance.
- Explanation labels: `Evidenced` (bank line, remittance, notice) or `Hypothesis` (inferred, to confirm with an owner).

## Accuracy measures

- Category accuracy for a week: `1 − |Actual − Forecast| / |Forecast|` (report "n/a" when Forecast is zero).
- Bias over the trailing weeks the user names: `Sum(Actual − Forecast) / Sum(|Forecast|)`; a persistent positive or negative bias by category is reported as a pattern for the forecast owner.
- Track accuracy of week 1, week 4 and week 13 forecasts separately when history allows.
