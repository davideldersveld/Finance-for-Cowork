# Journal upload file specification and validation checks

## 1. Default upload columns (used only when the user has no ERP template)

| # | Column | Rule |
|---|---|---|
| 1 | Journal reference | Unique within the batch; pattern agreed with the user (for example ENTITY-PERIOD-TYPE-NNN). |
| 2 | Entity | Company code from the profile entity list. |
| 3 | Journal type | Standard, Recurring, Adjusting, Reclassification, Correction. |
| 4 | Posting date | Within the posting period; ISO date format. |
| 5 | Period | Fiscal period per the profile calendar (for example 2026-09 or P09 FY26). |
| 6 | Line number | Sequential within the journal. |
| 7 | Account | Natural account from the chart of accounts. |
| 8 | Cost centre | Required where the account's dimension rule requires it. |
| 9 | Other dimensions | Department, project, product, location, as the chart requires; one column each. |
| 10 | Intercompany partner | Required for intercompany accounts; blank otherwise. |
| 11 | Transaction currency | ISO 4217 code. |
| 12 | Debit (transaction currency) | Positive number or blank. |
| 13 | Credit (transaction currency) | Positive number or blank. Never both debit and credit on one line. |
| 14 | Exchange rate | Rate to functional currency, with source and date recorded in About. Blank or 1 when currencies match. |
| 15 | Debit (functional currency) | Debit x rate, rounded to the currency's minor unit. |
| 16 | Credit (functional currency) | Credit x rate, rounded to the currency's minor unit. |
| 17 | Line description | What, why, period, source. |
| 18 | Auto-reverse | Y or N. |
| 19 | Reversal date | Required when Auto-reverse is Y; normally the first day of the next period, as the user states. |
| 20 | Support reference | File and sheet and range, or document and page. |

## 2. Validation checks (each reported Pass / Fail / Not tested)

| Check | Rule |
|---|---|
| V1 Balance - transaction currency | For each journal and each transaction currency, sum of debits = sum of credits exactly. |
| V2 Balance - functional currency | For each journal, sum of functional debits = sum of functional credits. A rounding difference arising only from translation is shown, never absorbed by a new line; the user decides where to place it within the rounding tolerance in the profile. |
| V3 Balance - entity | Each entity's lines within a journal balance on their own (cross-entity journals are split, or the ERP's intercompany mechanism is named by the user). |
| V4 Account exists and is active | Account present in the chart of accounts version used, status active, valid for the entity. |
| V5 Account is postable | Not a header or summary account. Subledger-controlled accounts (AP control, AR control, fixed asset cost and accumulated depreciation, inventory where perpetual) fail unless the user confirms a manual posting is permitted. |
| V6 Dimensions | Required dimensions present; each value exists and is active; combinations allowed by any cross-validation rule the user supplies. |
| V7 Intercompany | Partner code present for intercompany accounts; partner is a different entity in the profile; counterparty side is either in the batch or listed for the partner entity. |
| V8 Period and date | Period is the period being closed, posting date falls within it, and the period is open according to the close calendar or the user. |
| V9 Line integrity | No line with both debit and credit, no zero-amount lines, no negative amounts, description present. |
| V10 Duplicate | No other journal in the batch, or posted journal listing supplied, with the same entity, account, amount, period and support reference. |
| V11 Reversal | Auto-reversing journals have a reversal date in the following period; non-reversing adjusting journals say why. |
| V12 Support | Every journal has at least one support reference that opens to the stated file and range. |
| V13 Approval level | Journal total compared with profile approval limits; required approver level recorded, or `Not provided`. |

## 3. Correction entries

- Reverse the original exactly: same entity, accounts, dimensions and amounts, opposite side, referencing the original document number and posting date.
- Book the correct entry as separate lines in the same journal (or a linked journal) with its own support.
- If the original sits in a closed prior period, flag for the controller; whether to correct in the current period or revise prior periods is a judgement under ASC 250 or IAS 8.

## 4. Support memo section template

1. Journal reference, type, entity, period, posting date, currency.
2. Purpose - one sentence.
3. Lines table.
4. Calculation - formula in plain notation and source range.
5. Evidence - list of documents with references.
6. Reversal plan.
7. Approver level.
8. Status and open questions.
