# Correspondence stages and tone rules

Stage timing comes from the segment rulebook or the collections policy. The days shown in brackets are parameters supplied by the user, never defaults.

## Stages

| Stage | Typical trigger | Purpose | Tone | Must contain |
|---|---|---|---|---|
| Friendly reminder | D+[n] after due date, or D-[n] pre-due for selected segments | Make sure the invoice is received and scheduled | Courteous | Invoice list, total, due dates, how to pay, contact for queries |
| Past-due notice | D+[n] with no payment or promise | State the overdue amount and ask for a payment date | Firm and factual | Undisputed overdue items, total, request for payment or a dated commitment by [date], dispute contact |
| Statement of account cover | Monthly, or on request, or with a past-due notice | Give a full picture of open items and credits | Neutral | As-of date, open items including credits and unapplied cash, reference to the attached statement |
| Payment-plan confirmation | After a plan is agreed within authority | Confirm exactly what was agreed | Neutral and precise | Installment schedule (dates and amounts), total, what happens to the plan if an installment is missed per policy, how to pay |
| Final notice before escalation | D+[n] per policy, after at least one past-due notice and a contact attempt | Give a last, real date before a confirmed next step | Formal | Overdue items, total, date by which payment is requested, the specific next step the user has confirmed (for example review by the credit manager, account on credit hold, referral to an agency) and its date |

Payment-plan confirmation arithmetic: the sum of installments must equal the plan total; the plan total must equal the undisputed balance being settled (or the difference is explained, for example disputed items excluded). Check in code.

## Tone rules

Write so that a reasonable customer, a regulator or a judge would read the message as fair.

1. State facts that the ledger and contract support; no estimate of amounts.
2. Name the next step only if it is true, permitted and intended, and the user has confirmed it for this account.
3. Do not use "legal action", "court", "bailiff", "credit bureau" or similar unless the user confirms that the step is authorized and intended, and the policy allows mentioning it at this stage.
4. Do not imply that the sender is a lawyer, a government body or a collection agency.
5. Do not demand disputed amounts; list them as under review.
6. Do not add fees, interest or charges the contract does not provide for.
7. No capital-letter emphasis, red text, "FINAL WARNING" styling, or invented deadlines.
8. Always give a contact for questions and disputes, and accept that a customer may ask for communication in writing only.
9. Keep the internal note out of the message body.

## Consumer debtors

If the debtor is an individual or sole proprietor, the message may be subject to consumer-debt rules on content, disclosures, timing and channel (in the US, for example, the FDCPA and state laws, some of which apply to original creditors). Hold the message as `Held — compliance review` and tell the user it needs their compliance review before any draft is finalized.

## Subject line patterns

- Friendly reminder: "Invoice reminder — <company> account <number>"
- Past-due notice: "Past-due invoices — <company> account <number>"
- Statement: "Statement of account as of <date> — <company>"
- Payment plan: "Confirmation of agreed payment plan — <company>"
- Final notice: "Final notice before <confirmed next step> — <company> account <number>"
