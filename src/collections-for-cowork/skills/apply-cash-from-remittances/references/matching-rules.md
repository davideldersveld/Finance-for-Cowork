# Cash matching hierarchy and rules

Apply the rules in order. Stop at the first rule that produces a match meeting its condition. Record the rule number and confidence on every line.

## Hierarchy

| Rule | Condition | Confidence |
|---|---|---|
| 1. Remittance exact | Remittance lists invoices; each listed invoice is open for the identified customer; sum of remittance lines (net of stated discounts and deductions) equals the receipt amount. | High |
| 2. Remittance with differences | Remittance lists invoices but the sum differs from the receipt; the difference is explained by a stated discount, deduction code or bank charge line. | High if every difference is coded; Medium otherwise |
| 3. Narrative reference | Bank narrative contains invoice numbers that are open for the customer, and their total (less allowable discount) equals the receipt. | High |
| 4. Single amount match | Exactly one open invoice for the customer equals the receipt (or equals it after an allowable discount). If two or more invoices have the same amount, do not pick one; go to rule 6. | Medium |
| 5. Combination match | A unique combination of up to [n] open invoices for the customer sums exactly to the receipt. If more than one combination fits, do not choose; go to rule 6. Search limits are stated on the About sheet. | Medium |
| 6. Oldest first | Only if the customer's terms or the policy allow application to oldest items when no remittance exists. Apply to oldest undisputed items; never to disputed items. | Low |
| 7. On account | Customer identified, no rule above applies. | Not applicable |
| 8. Unapplied | Customer not identified, or currency mismatch without a supplied rate. | Not applicable |

## Customer identification order

1. Customer number in the bank narrative or remittance.
2. Invoice numbers that belong to a single customer.
3. Payer name matched to the customer master's payer names (exact, then normalized for legal-form suffixes and punctuation; fuzzy matches are Medium confidence at best).
4. Payer bank account mapping (compared on masked last 4 digits plus bank identifier; never display the full number).
5. Known third-party payers (parent company, factor, payment service) from the customer master.

## Discount rules

- Discountable base per terms (gross or net of tax as the terms state; record which).
- `Allowed discount = Discountable base x Discount rate` when `Receipt value date <= Discount date + Grace days`.
- `Unearned discount = Discount taken - Allowed discount`; propose as a deduction with code "Unearned discount" unless at or below the write-off threshold.

## Short pay and overpay rules

- `Short pay = Invoice open amount - Allowed discount - Cash applied`.
- If `Short pay <= Write-off threshold` and within tolerance, propose `Write-off per policy` with the approver level; otherwise create a deduction with the customer's reason code (or "No reason given").
- `Overpayment = Receipt - (Sum of invoice open amounts - Allowed discounts)`; record on account with the reason. Never propose a refund.

## Bank charges

If the receipt is short by an amount equal to a bank charge shown on the statement or remittance, propose a bank-charge write-off line only if the policy allows absorbing such charges and the amount is at or below the threshold; otherwise treat as a deduction.

## Anomaly indicators (flag `Review — anomaly`)

- Payer not previously associated with the customer and not in the third-party payer list.
- Remittance requesting changes to bank details, refunds to a new account, or application to another customer's invoices.
- Receipt applied to invoices of a customer in insolvency or referral.
- Several receipts from one payer on the same day summing to an exact invoice, each just below a threshold.
- Remittance format, sender domain or signature differs from the customer's established pattern.
