# Margin ladder, allocation drivers and concentration measures

## Margin ladder

| Level | Formula | Typical lines |
|---|---|---|
| Net revenue | Gross sales − discounts − rebates − returns − trade deductions | Price waterfall items from billing and deductions data |
| Gross margin | Net revenue − Direct cost of goods | Standard or actual cost of goods, royalties per unit |
| Contribution | Gross margin − Cost-to-serve | Freight, warehousing picks, returns handling, service tickets, payment terms cost, customer-specific marketing |
| Fully allocated margin | Contribution − Allocated shared costs | Sales overhead, marketing brand spend, IT, finance, facilities |

Payment terms cost (optional, if the user supplies a cost of capital) = Average receivable balance × Annual rate × Days in period / 365.

## Cost classification rules

- Direct: traceable per transaction (invoice line, production order).
- Cost-to-serve: traceable per activity; requires activity counts per cohort (orders, shipments, tickets, returns).
- Shared: no causal link in the data; allocated by a stated basis.
- When in doubt, classify as Shared and say so; never move a cost to Direct without transaction evidence.

## Allocation driver options

| Pool | Candidate drivers | Comment |
|---|---|---|
| Sales overhead | Revenue, order count, account count, sales visits | Revenue basis favours small customers with many orders |
| Customer service | Ticket count, handling minutes | Needs service system extract |
| Warehousing | Picks, pallets, cubic volume | Activity data by customer or SKU |
| Marketing (brand) | Revenue, gross margin | No causal driver; show as policy choice |
| IT and finance | Revenue, transaction count, headcount | Often left unallocated in contribution views |

Allocation_i = Pool × Driver_i / Σ Driver. Check Σ Allocation_i = Pool for every pool.

## Sensitivity table layout

| Cohort | Contribution | FA margin, basis 1 | FA margin, basis 2 | FA margin, basis 3 | Min | Max | Sign change | Status |
|---|---|---|---|---|---|---|---|---|

Status rules:
1. Contribution < 0 → Loss-making at contribution.
2. Else if FA margin < 0 under every basis → Loss-making after allocation.
3. Else if FA margin changes sign across bases → Allocation-sensitive.
4. Else if FA margin % < Marginal threshold under any basis → Marginal.
5. Else → Profitable.

## Concentration measures

- Top-N share = Σ top N cohort values / total (revenue and contribution separately).
- Herfindahl-Hirschman index (HHI) = Σ (share_i × 100)^2; 10,000 means one cohort holds everything. Report the number; do not label it high or low unless the user supplies bands.
- Cumulative profit curve: sort cohorts by fully allocated margin descending; plot cumulative margin as % of total against cumulative % of cohorts. Peak value above 100% shows the share of profit consumed by loss-making cohorts: Consumed = Peak − 100%.
- If total margin is zero or negative, the curve in % is undefined; show amounts instead.

## Low-margin driver decomposition (per flagged cohort, versus average)

- Price realization effect = (Cohort net price % of list − Average net price % of list) × Cohort gross sales
- Mix effect = Σ (Cohort product share − Average product share) × Average product margin × Cohort revenue
- Cost-to-serve intensity effect = −(Cohort cost per order − Average cost per order) × Cohort orders
- Remainder shown separately.
