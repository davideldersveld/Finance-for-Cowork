# Priority score — default rule and tie-breakers

Use the rule in the user's Finance Profile when one exists. Use this default only when the user confirms it on the question card; label it "Default rule — confirmed by user on <date>". Every parameter in brackets is set by the user; nothing here is a policy threshold.

## Default rule

`Priority score = Amount-at-risk points x DPD factor x Risk factor x Promise factor + Event bonus`

| Component | Definition |
|---|---|
| Amount-at-risk points | `Amount at risk (reporting currency) / [scale]`, where scale is a round unit such as 1,000. Amount at risk = undisputed past due - amount covered by open promises not yet due - plan installments not yet due. |
| DPD factor | From the maximum days past due on undisputed items: 1-30 = [f1], 31-60 = [f2], 61-90 = [f3], over 90 = [f4]. Factors rise with age. |
| Risk factor | From the segment list: Low = [r1], Medium = [r2], High = [r3]. |
| Promise factor | No promise history = 1.0; at least one broken promise in the last [n] days = [p1] (greater than 1.0). |
| Event bonus | Points added for events that need action today regardless of size: broken promise yesterday = [b1]; returned payment = [b2]; remittance to confirm = [b3]. |

Translate foreign-currency amounts at the rate the user or profile names before scoring; record the rate and date. If no rate is supplied, rank within each currency separately and say so.

## Tie-breakers (in order)

1. Higher amount at risk.
2. Older maximum days past due.
3. Longer time since last contact.
4. Customer ID ascending (deterministic).

## Worked check (fictitious, parameters as confirmed by a user)

Scale 1,000; DPD factors 1.0 / 1.3 / 1.6 / 2.0; risk factors 0.8 / 1.0 / 1.3; broken-promise factor 1.5; broken-promise-yesterday bonus 25.

- Proseware: amount at risk USD 15,000, max DPD 41, risk Medium, broken promise. Score = 15 x 1.3 x 1.0 x 1.5 + 25 = 29.25 + 25 = 54.25.
- Wide World Importers: amount at risk USD 24,000, max DPD 52, risk Medium, no broken promise. Score = 24 x 1.3 x 1.0 x 1.0 = 31.2.
- Adventure Works: amount at risk USD 60,000, max DPD 18, risk Low. Score = 60 x 1.0 x 0.8 x 1.0 = 48.0.

Ranking: Proseware (54.25), Adventure Works (48.0), Wide World Importers (31.2).

## Statuses used on the worklist

| Status | Applies when |
|---|---|
| `Work today` | Within the collector's daily capacity after ranking. |
| `Overflow` | Ranked but beyond capacity; carried to the next day's list. |
| `Skip — in dispute` | All past-due items disputed. |
| `Skip — payment plan` | Plan in good standing; next installment not due. |
| `Skip — promise not yet due` | Promised date plus grace not yet passed and promise covers the amount at risk. |
| `Skip — contacted recently` | Last contact inside the minimum interval. |
| `Skip — escalated` | Referred to agency or counsel, or insolvency. |
| `Hold — compliance review` | Possible consumer debt pending the user's compliance review. |
| `Override` | Supervisor moved the account; reason recorded. |
