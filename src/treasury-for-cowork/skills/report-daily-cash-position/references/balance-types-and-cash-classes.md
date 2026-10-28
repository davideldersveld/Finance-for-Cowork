# Balance types and cash classes

## Balance types by statement format

Use one balance type per column. Map each file's balance codes before any calculation.

| Concept | MT940 / MT942 | camt.053 / camt.052 | BAI2 type code |
|---|---|---|---|
| Opening ledger (booked) | :60F: or :60M: | OPBD (or PRCD for previous closing) | 010 |
| Closing ledger (booked) | :62F: or :62M: | CLBD | 015 |
| Opening available | not standard | OPAV | 040 |
| Closing available | :64: | CLAV | 045 |
| Forward available | :65: | FWAV | not standard |
| Interim (intraday) booked | :90D: / :90C: counts and sums; :61: lines | ITBD | intraday detail records |
| Interim available | not standard | ITAV | not standard |
| One-day float | not standard | not standard | 072 |
| Two-or-more-day float | not standard | not standard | 074 |
| Total credits / total debits | sum of :61: lines | TtlCdtNtries / TtlDbtNtries | 100 / 400 |

Rules:
- Closing available is the starting point for usable cash. Ledger balance includes uncollected items and is used only for statement integrity tests and reconciliation to the general ledger.
- Float is never usable cash on the as-of date.
- An "M" (intermediate) balance tag means the statement was split across messages; combine all pages before testing.
- Portal CSV exports: confirm with the user or the bank's column legend which column is ledger and which is available; if unclear, mark the account `Classification not provided`.

## Integrity tests

| Test | Formula | Failure label |
|---|---|---|
| Continuity | Opening ledger today − Closing ledger prior day = 0 | Balance break |
| Roll | Opening ledger + Total credits − Total debits − Closing ledger = 0 | Balance break |
| Control totals | Count and sum of transaction lines = trailer / summary totals | Balance break |
| Currency | Statement currency = inventory currency | Inventory mismatch |
| Date | Statement date = as-of date | Stale |

## Cash classes

| Class | Definition | Included in group usable cash |
|---|---|---|
| Restricted | Cash that cannot be used for general purposes — collateral, escrow, cash backing letters of credit or guarantees, court or regulatory deposits, grant or customer-segregated funds | No |
| Trapped | Accessible to the local entity but not freely transferable to the group because of exchange controls, regulatory capital, distributable-reserve limits, or a repatriation cost the user or profile identifies | No (shown as usable in its own entity) |
| Minimum operating balance | Balance the bank, a contract or the treasury policy requires to remain in the account | No |
| Compensating balance | Balance held to offset bank fees or support a facility; treat as minimum unless the profile says otherwise | No |
| Usable | Available − Restricted − Minimum operating balance | Yes |

Classification source must be the bank account inventory, the Finance Profile or the user. Never infer a restriction from the account name alone; flag a likely restriction (for example an account named "escrow") as `Classification not provided` and ask.

## Funding status

| Status | Rule |
|---|---|
| Funding need | Projected end-of-day − Target < 0 |
| Within target | 0 ≤ Projected end-of-day − Target ≤ surplus band from the profile |
| Surplus | Projected end-of-day − Target > surplus band |
| Overdrawn | Projected end-of-day < 0 (also a Funding need) |

## Same-day flow tags

| Tag | Evidence required |
|---|---|
| Confirmed | Bank advice, counterparty confirmation, or settled intraday entry |
| Scheduled | Item in an approved payment run, debt service schedule, payroll calendar, tax calendar or deal ticket |
| Estimated | Pattern, forecast or verbal indication; always listed separately in the summary |
