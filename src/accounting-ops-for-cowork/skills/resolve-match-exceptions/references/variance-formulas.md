# Variance formulas and line reconciliation

All quantities in the PO unit of measure after any confirmed conversion. All amounts in invoice currency unless stated.

## Definitions

- OQ = ordered quantity on the PO line (after change orders)
- RQ = cumulative received quantity on the PO line as of the as-of date
- RT = cumulative returned quantity
- PIQ = quantity already invoiced on earlier invoices (posted or parked)
- IQ = quantity on this invoice line
- PP = PO unit price (current version, with its effective date)
- IP = invoice unit price

## Formulas

| Measure | Formula |
|---|---|
| Available to invoice, three-way | ATI3 = RQ − RT − PIQ |
| Available to invoice, two-way | ATI2 = OQ − PIQ |
| Quantity variance | QV = IQ − ATI (positive means invoiced more than available) |
| Quantity variance value | QVV = max(QV, 0) × PP |
| Price variance | PV = (IP − PP) × IQ |
| Price variance % | PV% = (IP − PP) ÷ PP |
| Matched value | MV = min(IQ, ATI) × PP |
| Amount variance (value-based line) | AV = invoiced amount − (PO line value − amount already invoiced) |
| Line reconciliation | invoice line net = MV + PV + QVV, where QVV uses PP; if QV < 0 the invoice is under available and QVV is zero |

Invoice-level check: sum of line nets + unmatched lines (freight, surcharges, new items) = invoice net. The difference must be zero; show it.

## Tolerance test

- Price: breach if |PV%| > profile percentage, and/or |PV| > profile absolute amount, according to the profile's rule (either-or or both).
- Quantity: breach if QV > 0 beyond the profile quantity tolerance; under-invoicing (QV < 0) is not a breach but is noted.
- Report headroom = tolerance − |variance| (negative means excess).

## Unit-of-measure test

If IP ÷ PP or OQ ÷ IQ is within 0.5% of a common pack factor (6, 10, 12, 24, 48, 100, 1,000) or a factor in the material master, flag "Possible unit-of-measure mismatch" and recompute variances on the converted basis before diagnosing.

## Discount at risk

Discount at risk = gross × discount % when the discount date ≥ as-of date and the block is still open; days remaining = discount date − as-of date.
