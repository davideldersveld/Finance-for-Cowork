# Normalization and total cost of ownership rules

Apply the same rule to every bidder. Record each rule on the About sheet.

## Order of operations

1. Transcribe each bidder's pricing exactly as submitted (Price_Normalization, "as submitted" columns), with file and cell or page reference.
2. Convert units of measure to the package unit (for example price per case of 12 to price per unit = case price / 12). Record the conversion factor and its source.
3. Apply tiers to the package's indicative volumes.
4. Convert currency at the single rate set named in the model or by the user.
5. Build the TCO by year.
6. Apply any pre-declared loadings in a separate column.
7. Feed the TCO into the price-scoring formula.

## Tier structures

| Type | Calculation for annual volume V |
|---|---|
| Incremental (stepped) | Sum over tiers of (units falling in the tier x tier price) |
| All-units | V x price of the tier that V falls in |
| Retrospective rebate | V x base price - rebate earned at V; rebate shown separately as conditional |

If a bidder does not state the tier type, record it as an assumption, compute both, and raise a clarification.

## TCO components

| Component | Rule |
|---|---|
| One-off charges | Setup, onboarding, installation, transition, tooling; counted once in year 1 unless the bid states otherwise |
| Recurring fixed | Monthly x 12 or annual fee, per year of the term |
| Volume-driven | Unit price x package volume per year |
| Indexation | Only if the model specifies an assumed index rate for evaluation; applied identically; otherwise nominal prices held flat and stated as such |
| Optional years | Shown separately; included in the scored TCO only if the model says so |
| Buyer-side costs | Transition, internal implementation, exit costs from incumbent; included only if the model lists them and applied with the same evidence standard to all bidders |
| Discounts | Unconditional discounts applied; conditional discounts (early payment, volume commitments above package volumes) shown separately and excluded from scored TCO unless the model says otherwise |
| Taxes | Excluded where recoverable; state the treatment |

`TCO over term = sum over years (one-off + recurring fixed + volume-driven)`

Present-value view (optional, only with a user or profile discount rate r): `PV = sum over years t of cash out in year t / (1 + r)^t`, shown beside nominal TCO, never replacing the model's basis.

## Currency

- One rate per currency pair for the whole evaluation, with rate type, source and date.
- Show original-currency totals beside converted totals.
- If the rate set is missing, leave converted totals as `Not provided`; do not choose a rate.

## Missing and inconsistent items

| Situation | Treatment |
|---|---|
| Price line blank | `Not provided`; clarification raised; total shown as "known subtotal + named missing items" |
| Line priced as "included" | Zero for that line, with the bidder's statement cited |
| Arithmetic error in bidder's own total | Recompute from unit prices x quantities; show bidder's total and the recomputed total; clarification raised; the model's rule decides which governs |
| Price conflicts between schedule and narrative | Use the pricing schedule; cite the conflict; clarification raised |
| Bid validity shorter than requested | Flag; status `Compliant with exceptions` |

## Evaluator moderation table

Criterion | Evaluator | Score | Evidence reference | Mean | Spread (max - min) | Moderation needed (spread at or above the stated trigger) | Moderated score | Moderation note
