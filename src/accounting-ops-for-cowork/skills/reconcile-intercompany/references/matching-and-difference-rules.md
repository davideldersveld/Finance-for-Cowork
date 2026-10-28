# Intercompany matching tiers, difference components and readiness rules

## 1. Sign convention and pair views

- Receivables, loans receivable, income and revenue are positive; payables, borrowings, expense and cost are negative.
- For each pair (A, B) and position: Net difference = Side A + Side B. A perfectly agreed pair nets to zero.
- The matrix view of A against B must equal the negative of B against A; any asymmetry is a data error to resolve before analysis.

## 2. Position pairs

| Side A position | Expected Side B position |
|---|---|
| Intercompany receivable | Intercompany payable |
| Intercompany loan receivable | Intercompany borrowing |
| Interest income | Interest expense (or capitalized interest, labelled) |
| Revenue or recharge income | Expense, inventory, or capitalized cost (labelled; unrealized profit is handled in consolidation by `compile-financial-statements`) |
| Dividend receivable or income | Dividend payable or distribution in equity |

## 3. Matching tiers (apply in order; a line matched in one tier is not re-used)

| Tier | Rule | Result |
|---|---|---|
| T1 | Same intercompany reference (invoice, agreement or loan ID) and same transaction-currency amount | Matched |
| T2 | Same reference, different transaction-currency amount | Matched with amount mismatch |
| T3 | No common reference; same transaction-currency amount and posting dates within the cutoff window | Proposed match - reviewer to confirm |
| T4 | One-to-many or many-to-one on reference, with summed amounts equal | Matched (group) |
| - | Anything left | Unmatched - classify as timing, missing side, classification or duplicate |

## 4. Difference components

| Component | Rule | Calculation |
|---|---|---|
| FX difference | Transaction-currency amounts agree, reporting-currency amounts differ | FX = RC difference - (TC difference x closing TC-to-RC rate) |
| Timing | One side posted on or before period end; the other side posted after period end and on or before the cutoff date; supported by the later posting or shipping, delivery or invoice date | Amount of the unrecorded side |
| Missing side | No counterparty entry by the cutoff date | Full amount of the recorded side |
| Amount mismatch | Both sides recorded with different TC amounts | TC difference x closing rate |
| Classification mismatch | Recorded in a non-intercompany account, wrong partner code, or wrong position pair | Amount affected |
| Duplicate | Same reference and amount recorded twice on one side | Duplicate amount |
| Unexplained | Residual | Net difference - sum of identified components |

Notes:
- Unrevalued foreign-currency monetary balances produce FX differences. Proposed revaluation on the entity carrying the foreign-currency item = TC amount / closing rate (in functional currency) - carrying amount, using the rate source and date stated in Sources & Assumptions.
- Flows (revenue and expense) translated at average rates by policy will not equal balance translations; compare flows at the rate type the policy sets for both sides.

## 5. Correcting side rules

1. Follow the intercompany policy where it names the adjusting side (for example, the receiving entity always conforms to the issuing entity's invoice).
2. Otherwise, the side contradicted by the evidence (agreement, invoice, charge schedule, loan statement) adjusts.
3. If the evidence does not resolve it, mark `Counterparty agreement needed`, list both entity controllers, and propose no entry.

## 6. Elimination readiness (per pair, first match in this order)

| Status | Condition |
|---|---|
| Not assessed - data missing | Either side's intercompany data is missing or unreadable. |
| Not ready | Absolute unexplained difference above the pair tolerance, or an item marked Counterparty agreement needed above tolerance. |
| Ready after proposed true-ups | Every difference above tolerance has an identified component and an evidenced proposed entry; unexplained within tolerance. |
| Ready for elimination | Absolute net difference after FX within tolerance and no open items above tolerance. |

## 7. Proposed true-up columns

Entity, Partner, Debit account, Credit account, Currency, Amount, Rate and source (if translated), Component addressed, Rationale, Evidence reference, Correcting side basis, Status (Proposed / Counterparty agreement needed).
