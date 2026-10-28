# Sample size and selection

## 1. Source of sample sizes

Sample sizes always come from the user's stated methodology table. Record the table's name, version and location on the About sheet, and look sizes up by formula so the reviewer can see the logic.

## 2. Commonly used default (needs the user's confirmation)

Offer this table only when the user has no methodology table. Present it on the question card as "Commonly used frequency-based default — confirm or replace". Until the user confirms, sample size is `Not provided` and testing does not start. Once confirmed, label the source "Default table — confirmed by user" and record who confirmed and when.

| Control frequency | Typical occurrences per year | Lower risk of failure | Higher risk of failure |
|---|---|---|---|
| Annual | 1 | 1 | 1 |
| Quarterly | 4 | 2 | 2 |
| Monthly | 12 | 2 | 3 |
| Weekly | 52 | 5 | 10 |
| Daily | about 250 | 20 | 30 |
| Multiple times per day | more than 250 | 25 | 40 |
| Automated | n/a | 1 per configuration, with effective ITGCs | 1 per configuration, with effective ITGCs |

Notes that travel with the default:

- Event-driven controls use the band whose occurrences per year are closest to the actual population.
- When the population is smaller than the size, test every item.
- For an interim test, prorate only if the methodology says so; otherwise use the full size for the interim period and a roll-forward size set by the methodology.
- Tolerable exceptions and sample expansion are methodology decisions; the default above assumes zero tolerable exceptions and no expansion unless the user states otherwise.

## 3. Risk of failure

Use the user's rating. Where the methodology asks the tester to rate it, record the AS 2201.47 factors considered: nature and materiality of misstatements the control addresses; inherent risk of the account and assertion; changes in volume or nature of transactions; history of errors; effectiveness of entity-level controls and monitoring; nature of the control and frequency; reliance on other controls such as ITGCs; competence of the performer and changes in key personnel; manual versus automated; complexity and judgement. Label the rating a judgement for the reviewer.

## 4. Selection methods

| Method | When | Procedure recorded |
|---|---|---|
| Random | Default for transactional controls | Seed, generator, population row numbers selected |
| Systematic with random start | Large ordered populations | Interval = population count / sample size (rounded down), random start between 1 and the interval |
| All items | Population at or below sample size | Population count |
| Targeted periods | Periodic controls where methodology requires coverage of quarter-end or year-end occurrences | Rule applied and periods chosen |

Rules:

- Select in code; never pick items by eye.
- Record population file name, modified date, row count, control total and seed.
- Selection is made by the tester; the control owner never chooses or pre-screens items.
- If a selected item is void or out of scope, document why and replace it with the next random selection; never replace an item because evidence is hard to obtain.

## 5. Remediation retest and roll-forward

- Retest only after the remediated control has operated for the minimum period or number of occurrences the methodology requires; `track-remediation` reports that readiness.
- Retest sample sizes come from the methodology; if it gives none, use the confirmed default for the control's frequency.
- Roll-forward procedures cover the period from the interim test date to the assessment date; record inquiry, changes in the control and any additional items tested.
