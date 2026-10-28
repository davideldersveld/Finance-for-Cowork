# Sourcing requirement — field list, risk flags and question template

Use this list when the user has no intake register of their own. Keep column order; add the user's own fields at the end.

## Requirement fields

| # | Field | Content rule |
|---|---|---|
| 1 | Request ID | User's reference if given; otherwise date received plus requester surname |
| 2 | Date received | Date of the first message in the thread |
| 3 | Requester | Name and role |
| 4 | Requesting entity | Legal entity from the profile entity list |
| 5 | Budget owner | Name and role; `Not provided` if absent |
| 6 | Cost centre or project | As stated; never inferred from the requester's department alone |
| 7 | Need description | One or two sentences in plain language |
| 8 | Purchase type | Goods / Services / Software or subscription / Works / Mixed |
| 9 | Category | Taxonomy label; `Provisional` suffix if proposed |
| 10 | Requested supplier | As stated by requester; recorded as a preference |
| 11 | Supplier status | Existing (in register) / New / Not named |
| 12 | Need-by date | As stated; flag if fewer working days remain than the route's minimum duration in policy |
| 13 | Term | Months; base term and options listed separately |
| 14 | Currency | Currency of the quote or estimate |
| 15 | Annual value | Formula shown |
| 16 | One-off costs | Setup, onboarding, hardware, transition |
| 17 | Base contract value | Formula shown |
| 18 | Maximum contract value | Includes options and contingent items |
| 19 | Value basis | Quoted / Requester estimate / Historical spend / Not provided |
| 20 | Value range | Low and high where basis is Requester estimate |
| 21 | Aggregated value | Sum with related requests in the policy window, with references |
| 22 | Policy band | Band name and the value measure used |
| 23 | Sourcing route | Single quote / N written quotes / Competitive tender / Framework call-off / Direct award |
| 24 | Existing contract or framework | Contract ID, remaining value and expiry, if a call-off |
| 25 | Single-source justification | Type and evidence, or `Not applicable` |
| 26 | Approval chain | Ordered list with the limit or risk that triggers each approver |
| 27 | Risk flags | See below |
| 28 | Open questions | Count by priority |
| 29 | Status | One of the four statuses in the skill |
| 30 | Sources | Message and attachment references |

## Risk flags

Record each as Yes / No / Unknown with the supporting sentence.

| Flag | Raise when |
|---|---|
| Data access | Supplier will receive, store or process personal data or confidential company data, or receive system credentials |
| On-site work | Supplier staff or subcontractors will work at a company site (health and safety, induction, site insurance) |
| Single source | Requester names only one possible supplier or asks for direct award |
| New supplier | Supplier is not in the supplier register; route to onboarding due diligence |
| Cross-border | Supplier, delivery or data processing is in a different country from the entity |
| Regulated category | Category is subject to sector rules the policy names (for example clinical, financial services outsourcing, export-controlled goods) |
| Intellectual property | Deliverables create IP the company needs to own |
| Subcontracting | Supplier states it will subcontract a material part of the work |
| Retrospective | Work has started or a commitment was made before approval |
| Conflict of interest | Requester or approver discloses a relationship with the supplier |
| Non-standard terms | Supplier quote attaches its own terms; refer to the legal team |

## Requester question template

Write one question per gap, in this form:

> **[Priority]** [Field]: [What is missing and why it matters, in one sentence]. Could you confirm [the specific value or document needed]?

Priorities: **Blocking** (band or route cannot be set), **Before approval**, **Before contract**.

Example:

> **Blocking** Term: The email mentions an extension option but not its length, which decides whether this needs a formal tender. Could you confirm the length of the extension option and whether its pricing is fixed?
