# Duplicate invoice tests

Run every test against (a) AP history for the lookback window in the Finance Profile or stated by the user and (b) the current batch. Compare credit notes only with credit notes.

## Normalization before testing

- Invoice number: uppercase; remove spaces, hyphens, slashes, dots and leading zeros; strip common prefixes (INV, IN, NO, #) only for the comparison key, never in the output.
- Supplier: compare by vendor ID, and also by tax registration number and bank account last 4, so the same supplier under two vendor IDs is caught.
- Amount: compare gross in invoice currency to two decimals.
- Dates: invoice date as a date, not text.

## Tests and risk rating

| Test | Rule | Risk |
|---|---|---|
| D1 Exact | Same vendor ID + same raw invoice number | High |
| D2 Normalized number | Same supplier + same normalized number | High |
| D3 Same supplier, amount, date | Same supplier + same gross + same invoice date, different number | High |
| D4 Cross-vendor | Different vendor IDs sharing tax number or bank last 4 + same gross + invoice dates within 30 days | High |
| D5 Amount and window | Same supplier + same gross + invoice dates within the lookback window, different number | Medium |
| D6 Near number | Same supplier + same gross + numbers differing by one character | Medium |
| D7 Reminder or copy | Document marked copy, duplicate, reminder or re-sent | Medium |
| D8 Recurring look-alike | Same supplier + same gross + monthly pattern with distinct service periods | Low (expected recurring charge; confirm service period differs) |

## Handling

- High: status Hold - possible duplicate; cite the matched invoice number, date, amount, status (paid, open) and source.
- Medium: invoice stays in the batch with status Exception - duplicate review; AP lead confirms.
- Low: note only.
- Report the number of history records searched and the window covered. If history is unavailable, write "Duplicate test limited to current batch" in Sources & Assumptions.
