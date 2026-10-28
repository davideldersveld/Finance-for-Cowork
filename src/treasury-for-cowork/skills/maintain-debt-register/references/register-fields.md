# Debt register fields

Every field carries a source column (document, section, and amending document where applicable). Use `Not provided` for absent terms and `Pending source` for terms a missing document may have changed.

## Facility and tranche fields

| Field | Notes |
|---|---|
| Facility ID | Stable internal key; never reused |
| Facility name and tranche | For example Revolving Credit Facility; Term Loan A; 2031 Senior Notes |
| Instrument type | Revolver, term loan, delayed-draw term loan, asset-based facility, bond, private placement note, commercial paper program, overdraft, bilateral line |
| Committed or uncommitted | As stated in the document |
| Borrower(s) | Legal entity names |
| Guarantors | Named guarantors or the guarantor coverage test |
| Agent / trustee | Name and role |
| Currency and multicurrency options | Including sublimits per currency |
| Commitment | By facility and tranche |
| Accordion or incremental capacity | Amount and conditions |
| Availability period | Start and end dates for drawing |
| Base rate | For example Term SOFR, Daily Simple SOFR, SONIA compounded in arrears, EURIBOR; tenor options |
| Rate floor | Applied to base rate |
| Benchmark fallback | Section reference only |
| Margin / coupon | Fixed or grid; current level and effective date |
| Pricing grid test metric | For example Consolidated Total Net Leverage Ratio from the latest compliance certificate |
| Credit spread adjustment | If any |
| Commitment fee | Rate or percentage of margin; basis (undrawn commitment) |
| Utilization fee | Tiers and rates |
| Upfront / OID | From fee letter or agreement |
| Agency and other fees | Amount and frequency |
| Letter of credit fees | Rate and fronting fee |
| Day-count convention | ACT/360, ACT/365, 30/360 as stated |
| Interest periods and payment dates | Options and payment timing |
| Default interest | Rate increment |
| Final maturity | Date |
| Extension options | Number, length, conditions, fees |
| Amortization | Schedule with dates and amounts or percentages |
| Mandatory prepayments | Asset sale, debt or equity issuance, excess cash flow sweep percentages and step-downs |
| Voluntary prepayment | Notice period, minimum amounts, breakage, call protection (soft call, make-whole) |
| Security | Collateral description, perfection notes |
| Financial covenants | Ratio, level by test date, test frequency, cure rights (pointer to the covenant workpaper) |
| Negative covenant baskets | Headings and section references (debt, liens, investments, restricted payments) |
| Events of default | Headings and section references, cross-default threshold |
| Governing law | As stated |

## Obligations calendar fields

| Field | Notes |
|---|---|
| Obligation | Quarterly financials, annual audited financials, compliance certificate, budget, borrowing base certificate, insurance certificate, notice events, borrowing notice lead time, prepayment notice lead time |
| Facility and section | Citation |
| Trigger | Period end, event, or request |
| Days or lead time | As stated, with calendar or business days distinguished |
| Due date | Period end + days, adjusted by business-day convention |
| Owner | Name and role |
| Status | Upcoming / Due / Delivered / Overdue / Not applicable |
| Evidence | Sent email, agent acknowledgment, portal upload record |

## Debt service formulas

- `All-in rate = max(Base rate, Floor) + Credit spread adjustment + Margin`
- `Interest = Principal × All-in rate × Days in period ÷ Day-count basis`
- `Commitment fee = Fee rate × Average undrawn commitment × Days ÷ Basis`
- Compounded-in-arrears rates (for example SONIA) are taken from the agent's rate notice; do not recompute daily compounding unless the user supplies the daily rates and lookback convention.

## Reconciliation status

| Status | Rule |
|---|---|
| Agrees | Difference within tolerance from the profile or user |
| Timing | Difference fully explained by a dated notice or settlement around the as-of date, with evidence |
| Unreconciled | Any other difference |
