# Journal entry risk tests and default parameters

Each test is a binary flag at entry level: an entry is flagged when any of its lines meets the rule. Every rule runs in code, and every parameter shows its value and source on the Parameters sheet.

## 1. Required fields

Entry ID; line number; entity; ledger; account; account description; debit; credit; currency; posting date and time (with time zone); effective (document) date; period; source (manual, system, interface, recurring); creator user ID; approver user ID; approval timestamp; description; reversal indicator and reversal entry ID. A missing field disables the tests that need it; list disabled tests on the About sheet.

## 2. Tests

| ID | Test | Rule (entry flagged when) | Parameters |
|---|---|---|---|
| T01 | Weekend or holiday posting | Posting date falls on a Saturday, Sunday or a date in the holiday calendar | Holiday calendar by entity |
| T02 | Outside business hours | Posting time (entity local time) before start or after end of business hours | Start, end, time zone |
| T03 | Round amount | `MOD(ABS(line amount), round multiple) = 0` and `ABS(line amount) >= minimum` | Round multiple, minimum amount |
| T04 | Rare account combination | The debit-account-class to credit-account-class pair occurs in fewer than N entries in the population, or matches a user-listed unusual pairing | N; unusual pair list |
| T05 | Senior management poster | Creator user ID maps to a role on the user's senior role list | Senior role list |
| T06 | Infrequent poster | Creator posted fewer than N entries in the period | N |
| T07 | Manual entry to sensitive accounts | Source is manual and a line hits an account in the sensitive list (revenue, reserves and estimates, equity, suspense, intercompany) | Sensitive account list |
| T08 | Period-end window or post-close | Posting date within D days before period end, or after period end but posted to the closed period | D; close date per calendar |
| T09 | Missing or non-descriptive description | Description blank, under L characters, or on a generic word list | L; generic word list |
| T10 | Self-approval or no approval | Approver ID blank, or approver ID equals creator ID | none |
| T11 | Backdating | `Posting date - effective date > tolerance days`, or posted into a prior period | Tolerance days |
| T12 | Just below approval limit | `limit x (1 - band %) <= ABS(entry amount) < limit` for the creator's or approver's limit | Approval limits; band % |
| T13 | Reversal shortly after period end | Entry reversed within R days after period end | R |

Entry amount for T12 and amount-based mandatory rules is the sum of debit lines of the entry.

## 3. Default parameter set (offer only; user must confirm)

Label every value "Default — confirm" until the user accepts it. These are common starting points, not standards.

| Parameter | Default offered |
|---|---|
| Business hours | 07:00 to 19:00 entity local time, Monday to Friday |
| Holiday calendar | Entity public holidays from the Finance Profile; if absent, `Not provided` and T01 runs on weekends only |
| Round multiple and minimum | Multiple of 1,000 in entry currency, minimum equal to the user's review threshold; if no threshold, `Not provided` and T03 is disabled |
| Rare combination N | Fewer than 5 entries in the period |
| Infrequent poster N | Fewer than 5 entries in the period |
| Period-end window D | 3 business days before period end |
| Description length L | Fewer than 10 characters; generic words "adj", "misc", "correction", "see attached" |
| Backdating tolerance | 2 days |
| Just-below band | 10% below the limit |
| Reversal window R | 5 business days |
| Weights | 1 per test |
| Tier cut-offs | High at 4 or more; Medium at 2 to 3; Low at 1 |

Senior role list, sensitive account list and approval limits have no default; they come from the user or the Finance Profile.

## 4. Scoring

- `Entry risk score = SUM over tests (weight x flag)`; maximum possible = sum of weights of enabled tests; show both.
- `Tier = High if score >= High cut-off; Medium if score >= Medium cut-off; Low if score >= 1; otherwise Not flagged`.
- Mandatory rules override tier for selection only; they do not change the score.

## 5. Population analytics (population level only)

- First-digit distribution of `ABS(entry amount)` for amounts of 10 or more against Benford expected proportions `log10(1 + 1/d)` for d = 1 to 9; show counts, observed % and expected % (1 dp).
- Entries by hour of day and day of week, by source.
- These analytics never flag or select an individual entry.
