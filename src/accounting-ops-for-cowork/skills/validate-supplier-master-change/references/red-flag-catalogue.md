# Red-flag catalogue for supplier master changes

Each flag is recorded with its evidence and marked Unresolved until specific evidence (not the requester's own explanation) resolves it.

## Channel and identity

| Flag | Test |
|---|---|
| R1 Look-alike domain | Sender domain differs from the baseline domain by character substitution (rn for m, 1 for l, 0 for o), added hyphen or word, different top-level domain, or homoglyph characters |
| R2 Reply-to mismatch | Reply-to or return-path differs from the sender address |
| R3 Free webmail | Request from a consumer mailbox when the supplier normally uses a corporate domain |
| R4 Changed signature | Signature block differs from genuine prior correspondence in phone number, name format, title, logo or address |
| R5 Unusual channel | Request arrives through a channel the supplier has not used before |
| R6 Unknown requester | Sender not a contact in the trusted baseline |

## Content and pressure

| Flag | Test |
|---|---|
| R7 Urgency | Deadline tied to a payment run, threats of supply stop or late fees, "today" |
| R8 Secrecy or call avoidance | "Do not call", "email only", "confidential", "auditors require" |
| R9 Combined changes | Contact details and bank details changed in one request, or contact changed shortly before a bank change |
| R10 Document anomalies | Bank letter with inconsistent fonts, missing contact, mismatched dates, generic letterhead |

## Account characteristics

| Flag | Test |
|---|---|
| R11 New-country account | Bank country differs from the supplier's registered country and prior bank country |
| R12 Personal or individual account | Account holder is a person, or account type is personal, for a corporate supplier |
| R13 Name mismatch | Account holder name differs from the supplier's legal name |
| R14 Shared account | Same bank and last 4 already on another supplier or an employee record |

## Timing and pattern

| Flag | Test |
|---|---|
| R15 Payment proximity | Request within days of a large scheduled payment or immediately after an invoice |
| R16 Out-of-hours or holiday | Sent or processed outside business hours or during holidays |
| R17 Multiple suppliers | Several suppliers asking for changes in the same period, or to the same bank |
| R18 Internal shortcut | Internal requester also approves, or asks to bypass the call-back |

Any single Unresolved flag makes the outcome Red flags.
