# Population and IPE checks

Run every check in code and record the formula and result on the Population sheet.

## 1. Population completeness

| Check | Formula or procedure | Pass criterion |
|---|---|---|
| Count to independent source | `Population count - Source count` | 0, or every difference itemized |
| Amount to independent source | `Population total - Source total` (for example the GL activity for the account and period) | 0, or every difference itemized |
| Period boundaries | Earliest and latest transaction dates | Within the test period; first and last days covered |
| Duplicates | Count of repeated document IDs | 0, or each explained |
| Filters | Parameters on the extract (entity, company code, document types, status) | Match the control's scope |
| Gaps in sequence | Missing numbers in a sequential document series | Each gap explained (void, cancelled) |

Status: **Population complete — reconciled**; **Population not reconciled — test paused**; **Population accepted with explained differences** (each difference listed with evidence).

## 2. Information produced by the entity (IPE)

For each report used either as the population or as evidence within the control (AS 1105.10):

1. Identify the report: name, source system, standard or custom, parameters used, run date and who ran it.
2. Completeness — trace a selection of source records into the report (source to report).
3. Accuracy — trace a selection of report lines back to source records and reperform any calculated fields (report to source).
4. Logic — for custom reports or queries, inspect or obtain evidence over the query logic, or rely on change management ITGCs plus a baseline test, as the methodology permits.
5. Parameters — confirm the run parameters match the intended population.
6. Record whether IPE reliance comes from these procedures, from a separately tested IPE control, or from ITGC reliance.

Status: **IPE addressed**; **IPE partially addressed — named step missing**; **IPE not addressed** (blocks reliance on the report).

## 3. Automated controls

- Confirm the configuration (setting, tolerance, workflow rule) by inspection for one instance per configuration.
- Confirm ITGC reliance for the period — access to programs and data, and program change — by citing the ITGC test results; if ITGCs have exceptions, the automated control result is "Testing incomplete — evidence outstanding" until their effect is evaluated.
- Benchmarking (AS 2201 Appendix B, B28-B33) only when the methodology permits it and change management evidence shows no change to the control since the baseline.

## 4. Evidence quality rules

- Prefer system-generated evidence and documents over inquiry; inquiry alone never supports a Pass.
- A signature or initials alone does not evidence a management review control's precision; look for annotations, investigation of items above threshold and resolution.
- Screenshots must show the date, system and user context.
- Evidence dated or created after the test request is recorded as an exception or as "Evidence not provided", never as a Pass.
