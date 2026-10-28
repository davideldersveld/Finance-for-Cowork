# Reconciliation status, item types and aging buckets

## 1. Core equation and sign convention

- Debit balances are positive, credit balances negative, for both GL and support.
- Reconciling items are signed so that: **Support balance + Sum of reconciling items + Unexplained difference = GL balance**.
- An item that makes the GL higher than the support (for example a deposit recorded in the GL but not yet on the bank statement) is positive; an item that makes the GL lower (for example a check recorded in the GL but not yet cleared) is negative.
- Unexplained difference = GL balance - Support balance - Sum of reconciling items. It is calculated, never entered.

## 2. Reconciliation status (one per account, first match in this order)

| Precedence | Status | Exact condition |
|---|---|---|
| 1 | Not reconciled - support missing | No independent support balance exists at the as-of date (statement, subledger report or schedule not provided, unreadable, or at a different date that cannot be rolled back). |
| 2 | Unreconciled difference | Absolute unexplained difference > tolerance from the profile or user. If no tolerance is set, any non-zero unexplained difference. |
| 3 | Reconciled with exceptions | Absolute unexplained difference <= tolerance, and at least one item is flagged (see section 4). |
| 4 | Reconciled | Absolute unexplained difference <= tolerance, and no flagged items. |

A reconciliation is never labelled reviewed or approved by this skill. Reviewer fields are left blank.

## 3. Reconciling item types

| Type | Definition | Typical examples | Resolution |
|---|---|---|---|
| Timing | Recorded correctly on one side; will appear on the other side in the normal course within the expected clearance period. | Deposit in transit, outstanding check, subledger posted after GL cutoff with matching entry next day. | Monitor; confirm clearance date. |
| Ledger error | The GL is wrong (duplicate, wrong account, wrong amount, wrong period). | Receipt posted twice; expense coded to clearing account. | Correcting entry proposed. |
| Support error | The support is wrong (bank error, subledger interface failure, schedule error). | Bank debited another customer's charge; subledger report excludes a batch. | Raise with bank or system owner; evidence the correction. |
| Unrecorded in ledger | Valid item on the support not yet recorded in the GL. | Bank fees, interest, direct debits, automatic sweeps. | Entry proposed. |
| Unidentified | Cause not yet determined. | Unknown bank credit; unexplained clearing balance. | Investigate; always flagged. |

## 4. Flags (any one makes the account Reconciled with exceptions)

- F1 - Absolute item amount >= item threshold from the profile or user.
- F2 - Item age > aging policy limit from the profile or user.
- F3 - Item type Unidentified, any amount.
- F4 - Item carried forward with an unchanged explanation for two or more consecutive period ends.
- F5 - Item type Ledger error or Unrecorded in ledger (an adjustment is required).
- F6 - Clearing or suspense account with any open item older than the clearing policy limit from the profile or user.

## 5. Aging

- Origination date = the date the item first arose: transaction date on the side where it is recorded (for example check issue date, deposit date, posting date of a misposting).
- Age in days = as-of date - origination date, in calendar days (an item dated on the as-of date has age 0).
- Buckets are inclusive and non-overlapping:

| Bucket | Age in days |
|---|---|
| 0-30 | 0 to 30 |
| 31-60 | 31 to 60 |
| 61-90 | 61 to 90 |
| 91-180 | 91 to 180 |
| 181-365 | 181 to 365 |
| Over 365 | 366 and above |

- An item with a future origination date (after the as-of date) is an error in the item list and is shown as `Date after as-of - check`, not aged.
- Where the user's policy uses different buckets, use the policy's buckets and state them in Sources & Assumptions.

## 6. Sign-off fields on the Reconciliation sheet

Preparer name, preparation date, reviewer name (blank), review date (blank), reviewer comments (blank).
