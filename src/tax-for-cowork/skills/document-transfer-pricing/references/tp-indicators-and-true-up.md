# Transfer pricing indicators and true-up mechanics

Methods are named as in the OECD Transfer Pricing Guidelines; this file defines only the arithmetic the skill performs. Selection, comparability and arm's length conclusions belong to the adviser.

## Profit level indicators

| Indicator | Formula | Typical use in a policy (as the policy states it) | Inputs to cite |
|---|---|---|---|
| Markup on costs | `(Charge − Cost base) ÷ Cost base` | Cost plus method on services or contract manufacturing | Cost base definition, pass-through costs, charge invoices |
| Net cost plus | `Operating profit ÷ Total costs` | Transactional net margin method with a cost-based indicator | Segmented P&L, cost definitions |
| Operating margin | `Operating profit ÷ Net revenue` | Transactional net margin method for distributors | Segmented P&L, revenue definition |
| Gross margin | `Gross profit ÷ Net revenue` | Resale price method | Purchase and resale prices, gross profit definition |
| Berry ratio | `Gross profit ÷ Operating expenses` | Limited-risk distribution or service intermediaries | Gross profit and operating expense definitions |
| Royalty rate | `Royalty ÷ Licensee net sales` | Licences of intangibles | Royalty base per agreement |
| Interest rate achieved | `Interest ÷ Average principal` | Intercompany loans and cash pools | Principal balances, day count, agreement rate |
| Price comparison | `Controlled price − Comparable uncontrolled price` | Comparable uncontrolled price method | Comparable transaction evidence supplied |

Average principal = (opening + closing) ÷ 2 unless daily balances are supplied, in which case use the daily average and say so.

## Cost base rules

- Use the policy's definition, cited by section: which costs are included, which are pass-through at no markup, treatment of share-based payments, depreciation and FX.
- If the policy is silent on a cost category, compute with and without it and label `Review required`.

## Status rules

| Status | Condition |
|---|---|
| At target | `abs(Result − Target) <= tolerance` (tolerance from user or profile) |
| Within range | Range low <= Result <= Range high, not At target |
| Below range | Result < Range low |
| Above range | Result > Range high |
| Policy not provided | No cited target or range |
| Data insufficient | Segmented numerator or denominator missing |

## True-up calculation

1. `Required result = Adjustment point x Base` (for example operating margin target x net revenue; markup target x cost base).
2. `True-up = Required result − Actual result`.
3. Positive true-up: the tested party is owed the amount by its counterparty; negative: it owes the counterparty. State invoicing direction.
4. Adjustment point per policy: Target, Median, or Nearest boundary (`Range low` if below, `Range high` if above). If the policy is silent, show all three and label `Review required`.
5. Some policies adjust only when outside the range; apply that condition only if the policy states it.
6. Translate to the reporting currency at the policy or user rate; record rate type, source and date.
7. Check: sum of true-ups across both sides of each pair = 0.

## Agreement check fields

Exists; signed by both parties; effective from and to covers the period; legal entity names match the ledger; method and pricing terms match the policy; actual charges consistent with the terms; year-end adjustment clause present; governing currency stated.

## Documentation requirement fields

Jurisdiction, Document (master file, local file, country-by-country report, notification, return disclosure form), Threshold, Deadline, Language requirement, Citation, Retrieval date, Status, Owner. Every value from a user-supplied or retrieved authoritative source; otherwise `Requirement not provided`.
