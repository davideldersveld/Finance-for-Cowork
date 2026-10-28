# Variance decomposition formulas

Notation: B = base (budget, forecast or prior year), A = actual. Q = units, P = price per unit, R = revenue = Q × P, C = unit cost, U = unit margin = P − C. i indexes items (product, SKU, customer or whatever level the user chooses; state it). Bars denote averages weighted by quantity: P̄_B = ΣR_B / ΣQ_B.

## 1. Order of decomposition

1. FX (removed first): FX effect = Actual at actual rates − Actual at plan rates.
2. Scope (if relevant and evidenced): acquired or divested units shown separately before price/volume/mix.
3. Volume, then mix, then price, on constant-currency like-for-like items.
4. New and discontinued items.
5. Residual (always shown).

State the convention in the About sheet and above every PVM table. Changing the order changes the split between effects; the total does not change.

## 2. Revenue price, volume, mix (default convention)

- Volume = (ΣQ_A − ΣQ_B) × P̄_B
- Mix = Σ(Q_A,i × P_B,i) − ΣQ_A × P̄_B
- Price = Σ(P_A,i − P_B,i) × Q_A,i
- New items = Σ R_A,i for items with Q_B,i = 0 (no base price exists)
- Discontinued items = −Σ R_B,i for items with Q_A,i = 0
- Residual = (R_A,cc − R_B) − (Volume + Mix + Price + New + Discontinued)

Proof of closure on like-for-like items: Volume + Mix = Σ(Q_A,i × P_B,i) − ΣR_B; adding Price gives ΣR_A − ΣR_B. Residual is therefore zero within rounding; a material residual means mismatched item lists, units, or currency and must be investigated.

Under this convention the joint price × volume effect sits inside Price (price measured on actual quantities).

## 3. Alternative convention (only if the user asks)

Price measured at base quantities, with interaction shown explicitly:
- Price = Σ(P_A,i − P_B,i) × Q_B,i
- Volume and Mix as above
- Interaction (joint effect) = Σ(P_A,i − P_B,i) × (Q_A,i − Q_B,i)
- Residual computed the same way and shown.

## 4. Gross margin decomposition

- Volume = (ΣQ_A − ΣQ_B) × Ū_B, where Ū_B = ΣGM_B / ΣQ_B
- Mix = Σ(Q_A,i × U_B,i) − ΣQ_A × Ū_B
- Price = Σ(P_A,i − P_B,i) × Q_A,i
- Unit cost = −Σ(C_A,i − C_B,i) × Q_A,i
- Residual = (GM_A,cc − GM_B) − (Volume + Mix + Price + Unit cost + New + Discontinued)

## 5. Cost-line decomposition (where drivers exist)

- Rate (price) variance = (Actual rate − Plan rate) × Actual quantity (for example hourly rate, unit purchase price)
- Usage (efficiency) variance = (Actual quantity − Plan quantity for actual output) × Plan rate
- Volume (activity) variance = (Plan quantity for actual output − Plan quantity) × Plan rate
- Sign: for costs, a positive amount is unfavourable.

## 6. Timing

Timing amount = the portion of the variance evidenced to fall in another period within the horizon. Evidence examples: invoice or delivery dated after period end for a period service; phasing where year-to-date variance ≈ 0 while the month differs; a dated purchase order or contract milestone. Without evidence the item is a Hypothesis, not Timing.

## 7. Worked check (two items)

| Item | Q_B | P_B | R_B | Q_A | P_A | R_A,cc |
|---|---|---|---|---|---|---|
| Kites | 100 | 10.00 | 1,000 | 120 | 9.50 | 1,140 |
| Drones | 50 | 20.00 | 1,000 | 40 | 21.00 | 840 |
| Total | 150 | 13.333 | 2,000 | 160 | | 1,980 |

Volume = 10 × 13.333 = 133.3; Mix = 2,000 − 2,133.3 = −133.3; Price = −60 + 40 = −20.0; Residual = −20 − (−20.0) = 0.0.

## 8. Commentary flag logic

- "Both" rule: flag if |Variance| ≥ absolute threshold AND |Variance %| ≥ percentage threshold.
- "Either" rule: flag if either is breached.
- Use the rule exactly as the profile or user states; when Plan = 0, test the absolute threshold only and record that.
