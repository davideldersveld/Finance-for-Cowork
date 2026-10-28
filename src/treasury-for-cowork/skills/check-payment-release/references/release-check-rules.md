# Release check rules

Parameters in angle brackets come from the Finance Profile or the user. If a parameter is missing, the check reports `Not performed — parameter not provided`, and the run cannot be Release ready.

## Check catalog

| # | Check | Rule | Default effect |
|---|---|---|---|
| 1 | Count and total | File count and total by currency = approved proposal | Hold (run) on difference |
| 2 | Payment-level integrity | Payee ID, beneficiary account, amount, currency and invoice references match the proposal | Hold (payment) on difference |
| 3 | File timing | Last modification of the file or batch is before the approval timestamp | Hold (run) if after |
| 4 | Funding | Projected available − Other same-day outflows − Run total by account ≥ 0 | Hold (account payments) on shortfall without evidenced cover |
| 5 | New beneficiary | No payment to this beneficiary account in <lookback period> | Hold without verification evidence |
| 6 | Recent bank detail change | Change date within <recent-change window> | Hold unless verification result is Verified with call-back to an independently sourced number |
| 7 | Account-name check | Bank or scheme name-check result is a match | Hold on no match or close match pending review |
| 8 | Amount versus history | Amount > <multiple> × payee's maximum (or average) over <lookback period> | Flag; Hold if the profile says so |
| 9 | Round amount | Amount ≥ <threshold> and divisible by <rounding unit> | Flag |
| 10 | First payment size | First payment to a payee ≥ <threshold> | Flag; Hold if the profile says so |
| 11 | Destination change | Beneficiary bank country differs from supplier's registered country or from prior payments | Flag; Hold if combined with check 5 or 6 |
| 12 | Currency change | Payment currency differs from payee's usual currency | Flag |
| 13 | Intermediary bank | Intermediary not seen for the payee before | Flag |
| 14 | Priority change | Urgent or same-day priority added after approval | Hold |
| 15 | Duplicate — exact | Same payee and same normalized invoice number, in run or lookback | Hold |
| 16 | Duplicate — near | Same payee, amount and invoice date; or same beneficiary account and amount under different payee IDs | Hold |
| 17 | Country indicator | Beneficiary, beneficiary bank or intermediary country on <compliance country list> | Hold without cleared, in-date screening evidence |
| 18 | Screening evidence | Screening result for payee is cleared and dated within <validity period> | Hold if missing or stale |
| 19 | Approvers count | Approvals ≥ required by the matrix for the amount | Hold |
| 20 | Segregation | Approvers distinct from each other and from the maker or last editor | Hold |
| 21 | Authority limits | Each approver's limit ≥ amount (or batch total, per the matrix) | Hold |
| 22 | Approval timing | All approvals after the last edit | Hold |
| 23 | Mandate currency | Approvers are current bank mandate holders | Hold |
| 24 | Value date and cut-off | Business day for the currency; release time before bank cut-off | Report risk |

## Invoice number normalization for duplicates

Uppercase; remove spaces, hyphens, slashes, periods and leading zeros; strip common prefixes such as "INV" or "NO"; compare the remaining strings. Report the raw values side by side.

## Red-flag patterns (payment-diversion and invoice fraud)

- Bank detail change requested by email shortly before a large payment.
- Call-back made to a number supplied in the change request rather than one held independently.
- New account in a different country or name from the supplier's.
- Pressure for urgency or confidentiality, or a request to bypass the normal run.
- An executive's name used to request an exceptional payment outside the approval workflow.

## Result rules

- Payment: `Release ready` only if every applicable check passes or is a flag the profile does not treat as blocking; otherwise `Hold` with all reasons.
- Run: `Release ready` only if every payment is Release ready and run-level checks pass; otherwise `Hold`, with the release-ready subset count and total shown.
