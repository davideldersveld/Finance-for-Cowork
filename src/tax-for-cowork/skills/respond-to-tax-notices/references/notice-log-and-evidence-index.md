# Notice log and evidence index specification

## Notice types

| Type | What it usually asks | First actions |
|---|---|---|
| Information document request | Documents or explanations for named periods | Number each request; index evidence per request |
| Audit or examination commencement | Scope, periods, taxes, first meeting, initial requests | Log scope; confirm internal owner and adviser; start evidence index |
| Proposed adjustment or assessment | Recalculated tax with basis | Figure Comparison; identify agreed versus disputed items for the adviser |
| Penalty or interest notice | Penalty amount and basis | Log amounts separately; list facts relevant to any relief the adviser may consider |
| Return query or mismatch letter | Difference between return and third-party data | Re-perform the tie-out (route return reconciliation to reconcile-indirect-tax-returns) |
| Registration or activity questionnaire | Whether the business operates in the jurisdiction | Route activity analysis to assess-nexus-and-registration |
| Refund query | Support for a claimed refund | Index the claim calculation and invoices |

## Notice Log columns

Notice ID, Authority, Notice type, Authority reference, Entity, Tax type, Periods, Tax amount stated, Penalty stated, Interest stated, Total stated, Currency, Issue summary, Notice date, Received date, Received channel, Authenticity screen (Passed / Suspected phishing / Not performed), External deadline, Deadline basis (quote or citation), Internal deadline, Owner, Adviser, Status, Last update, Source page references.

## Evidence Index columns

| Column | Content |
|---|---|
| Evidence ID | E-01, E-02 ... |
| Issue IDs | Issues the item supports |
| Document | Title and type (return, workpaper, ledger extract, invoice, contract, certificate, bank confirmation) |
| Location | OneDrive or SharePoint path, mail item subject and date, or ledger account and period |
| Period | Period the document covers |
| What it shows | One sentence, factual |
| Contains personal data | Yes / No; if Yes, redaction note |
| Privileged | Yes / No / Adviser to decide |
| Status | Located / Requested from owner / Not available |
| Requested from, Date requested | Internal owner and date |
| Provided to adviser | Date or blank |

## Draft response structure

1. Reference block — authority, reference, entity (tax ID masked), periods, date of draft.
2. Summary — what the response covers and what remains outstanding.
3. Responses by issue — in the authority's own numbering; each paragraph cites Evidence IDs.
4. Evidence schedule — list of enclosures by Evidence ID.
5. Items outstanding — what, owner, expected date.
6. Header and footer — "Draft — for adviser review — not for submission".

Placeholders used: `[Adviser to confirm]` for positions, `[Adviser — concession or settlement wording]`, `[Adviser — extension request if required]`.

## Deadline computation

- Stated date: use as stated; cite page and sentence.
- Stated period from a date: `Deadline = Anchor date + N days` (or months), computed in code; the anchor (notice date, date of service, received date) is the one the notice names. If the anchor is ambiguous, compute both and use the earlier as the working deadline, labelled Assumption for adviser confirmation.
- No deadline stated: `Not provided`; ask the adviser; retrieve a rule only from an authoritative source with citation and retrieval date.

## Status rules

Logged -> Evidence in progress -> Draft for review -> Adviser reviewed -> Submitted by user (evidence required) -> Closed (closure letter required). At risk and Overdue override the stage when their date conditions hold.
