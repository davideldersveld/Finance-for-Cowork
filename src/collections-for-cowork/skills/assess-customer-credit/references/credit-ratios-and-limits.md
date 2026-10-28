# Credit ratios, payment metrics and limit rules

Compute every measure in code for each year or period supplied. Show the inputs, the source line and the result. If an input is missing, show `Not provided` and do not compute the ratio.

## Financial statement ratios

| Measure | Formula | Notes |
|---|---|---|
| Current ratio | Current assets / Current liabilities | Below 1.0x indicates reliance on short-term funding. |
| Quick ratio | (Cash and equivalents + Short-term investments + Trade receivables) / Current liabilities | Excludes inventory and prepayments. |
| Working capital | Current assets - Current liabilities | Report in statement currency and units. |
| Tangible net worth (TNW) | Total equity - Goodwill - Other intangible assets | Exclude shareholder loans from equity unless subordinated by written agreement supplied. |
| Gearing | Total interest-bearing debt / Total equity | Include lease liabilities if the statements present them as debt; state the choice. |
| Debt to EBITDA | Total interest-bearing debt / EBITDA | EBITDA = Operating profit + Depreciation + Amortization. Use reported items only; no add-backs unless the statements disclose them. |
| Interest cover | EBITDA / Net interest expense | If net interest is income, show "Not meaningful". |
| EBITDA margin | EBITDA / Revenue | Percent to 1 dp. |
| Revenue growth | (Revenue current year / Revenue prior year) - 1 | Percent to 1 dp. |
| Operating cash flow to debt | Cash from operating activities / Total interest-bearing debt | Only if a cash flow statement is supplied. |
| Customer's own DSO | Trade receivables / Revenue x 365 | Context only; indicates the customer's own collection pressure. |
| Customer's own DPO | Trade payables / Cost of sales x 365 | Rising DPO can signal it is stretching suppliers, including you. |

Integrity checks before use: total assets equal total liabilities plus equity (difference within rounding of the statement's units); net profit agrees between income statement and equity movement where both are presented; the period length is 12 months (annualize a short period only if the user agrees, and label it).

Red flags to list (each with the page or note reference): negative TNW; two or more consecutive net losses; qualified, adverse or disclaimer opinion; material uncertainty related to going concern; covenant breach, waiver or refinancing disclosure; significant related-party receivables; auditor change in the last year; statements more than the policy maximum age.

## Payment behavior

- `Days beyond terms (per invoice) = max(0, Payment date - Due date)` in calendar days.
- `WADBT = sum(Paid amount x Days beyond terms) / sum(Paid amount)` over the window the policy states (default window is whatever the policy names; if none, ask).
- `Paid within terms % = Amount paid on or before due date / Total amount paid`.
- `Dispute rate = Amount disputed in window / Amount invoiced in window`.
- `Promise kept rate = Promises kept / Promises due in window` (count), taken from the promise log if available.
- `Highest exposure` = maximum month-end exposure in the window.
- Returned or dishonored payments: count and amount, with dates.

## Limit rules

The policy's own limit rule always governs. Common structures, to be applied only when the policy specifies them and with its parameters:

- **Needs-based limit** = Expected monthly credit sales x (Terms days + WADBT) / 30. This is what the customer needs to trade at the expected volume without blocking.
- **Net-worth-based capacity** = TNW x band percentage from policy.
- **Agency-based capacity** = Agency suggested limit x policy factor (only if the report is within the policy's age limit).
- **Insurance-based capacity** = Insured limit / insured percentage share, if the policy allows insurance to support the limit.
- **Policy capacity** = the minimum (or other combination stated in the policy) of the capacity measures above.
- **Recommended limit** = lower of the needs-based limit and policy capacity, rounded as the policy states.

## Order-hold release test

1. Exposure after release = Open AR + Open orders not invoiced + Shipped not invoiced + Order under review.
2. Compare with `Current limit x (1 + release tolerance)` from the policy.
3. Apply the policy's past-due rule (for example no undisputed item beyond a stated days-past-due band). Disputed items are excluded from the past-due test only if the policy says so; state which.
4. If the test fails, compute the smallest condition that passes: payment required = Exposure after release - Current limit x (1 + tolerance), and, separately, the amount of over-age undisputed items to be paid. Recommend the larger of the two, and show both.

## Worked check (fictitious)

Litware, statements in USD thousands. Current assets 4,820; current liabilities 3,950; current ratio 4,820 / 3,950 = 1.22x. Equity 2,600; goodwill 900; intangibles 300; TNW 2,600 - 900 - 300 = 1,400. Debt 2,100; EBITDA 700; debt to EBITDA 3.0x. Policy band B allows 5% of TNW, so net-worth capacity is 1,400 x 5% = 70 (USD 70,000). Expected monthly sales USD 30,000 on 30-day terms with WADBT 12 gives a needs-based limit of 30,000 x 42 / 30 = USD 42,000. Recommended limit: USD 42,000.
