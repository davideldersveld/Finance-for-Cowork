# RCM column definitions and attribute vocabularies

Use these columns unless the user supplies a template; when a template is supplied, map these fields onto it and list any field the template lacks on the About sheet.

## RCM sheet columns (one row per risk-control pair)

| Column | Content | Allowed values or format |
|---|---|---|
| Process | Top-level process | e.g. Order-to-cash, Financial close |
| Sub-process | Sub-process | e.g. Billing |
| Narrative step | Step number in the narrative | e.g. OTC-03.2 |
| Risk ID | Unique risk identifier | Prefix + R + number, e.g. OTC-R07 |
| Risk statement | "What could go wrong" in one sentence | Plain text |
| Significant account(s) | Accounts or disclosures affected | Names as in the scoping workpaper |
| Assertions | Relevant assertions | Codes below |
| Fraud risk | Fraud risk designation | Yes (per FRA) / Candidate — confirm / No |
| Control ID | Unique control identifier | Prefix + C + number, e.g. OTC-C04 |
| Control description | Who, what, when, how, evidence, exception follow-up | Full sentences |
| Control objective | What the control achieves for the risk | Plain text |
| Key / non-key | Designation | Key (confirmed) / Candidate key — confirm / Non-key |
| Type | Prevent or detect | Preventive / Detective |
| Nature | How performed | Manual / IT-dependent manual / Automated |
| Frequency | How often performed | Annual / Quarterly / Monthly / Weekly / Daily / Multiple times per day / Event-driven |
| Owner (role) | Performer | Name and role |
| Reviewer (role) | Reviewer, if any | Name and role or None |
| Precision | Threshold or expectation for review controls | Amount with currency and units, or % with base; `Not provided` if absent |
| COSO component / principle | COSO 2013 mapping | e.g. Control Activities / P10 |
| IPE used | Reports or data the control relies on | IPE ID(s) from IPE sheet or None |
| Systems | Applications involved | Names |
| ITGC dependency | ITGC domains relied on | Access / Change management / Operations / None |
| Evidence retained | What and where | Plain text |
| Attribute basis | Evidence basis | Observed / Stated / Inferred |
| Status | Documentation status | Documented / Documented — attribute missing / Inferred — confirm with owner / Conflict — owner to confirm / IPE gap |
| Missing elements | Which of the six elements are absent | Who / What / When / How / Evidence / Exceptions |
| Suggested — management to design | Optional design suggestion | Plain text, clearly a suggestion |
| Source | Citation | Document + page/section, or file + sheet + range |

## Assertion codes

AS 2201 set: **E/O** existence or occurrence; **C** completeness; **V/A** valuation or allocation; **R&O** rights and obligations; **P&D** presentation and disclosure.

Expanded set used by some methodologies (map, do not mix within one RCM): **A** accuracy; **CO** cutoff; **CL** classification; **U** understandability of disclosure. Record the chosen set on the About sheet.

## IPE sheet columns

IPE ID; Report or query name; Source system; Standard / Custom / Spreadsheet; Parameters (entity, period, filters); Controls relying on it; Completeness procedure; Accuracy procedure; Status (Addressed / IPE gap); Source.

## Six-element completeness check

A control description passes when each element is present and specific:

1. **Who** — named role, not "Finance".
2. **What** — the action, such as compares, approves, reconciles, investigates.
3. **When** — frequency or trigger, plus timing (for example by workday 5).
4. **How** — criteria, data used and precision (threshold, disaggregation, expectation).
5. **Evidence** — what is retained and where.
6. **Exceptions** — how items over threshold or errors are followed up and resolved.

## COSO 2013 principles most often cited in an RCM

P7 identifies and analyzes risk; P8 assesses fraud risk; P9 identifies and analyzes significant change; P10 selects and develops control activities; P11 selects and develops general controls over technology; P12 deploys through policies and procedures; P13 uses relevant, quality information; P16 conducts ongoing and separate evaluations; P17 evaluates and communicates deficiencies.
