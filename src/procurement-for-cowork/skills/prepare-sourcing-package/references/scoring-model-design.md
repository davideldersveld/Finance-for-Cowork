# Scoring model design rules

The scoring model is designed, approved and locked before any response is opened. These rules make it defensible.

## Structure

| Element | Rule |
|---|---|
| Criteria | 3 to 6 top-level criteria; each sub-criterion belongs to exactly one criterion |
| Weights | Expressed in percent; top-level weights sum to exactly 100.0; sub-criterion weights sum to their parent weight |
| Price weight | Stated explicitly; RFQ often 60 to 100 percent, RFP typically lower; the user decides, the skill records |
| Mandatory gate | Pass/fail before any scoring; a fail excludes the bid from scoring unless the model states a cure period |
| Quality threshold | Optional minimum quality score (for example 60 percent of available quality points); bids below it are not price-scored; record only if the user sets it |
| Panel | At least two evaluators per scored criterion where practical; each signs a conflict-of-interest declaration before reading responses |
| Tie rule | Stated in advance (for example higher quality score prevails) |

## Anchored scale (0 to 5)

| Score | Anchor |
|---|---|
| 0 | No response, or response does not address the requirement |
| 1 | Major gaps or significant concerns; little evidence |
| 2 | Partially meets; some gaps or weak evidence |
| 3 | Meets the requirement with adequate evidence |
| 4 | Meets fully with strong evidence and some added value |
| 5 | Exceeds with compelling evidence and clear added value |

Weighted criterion score = (score / 5) x criterion weight.

## Price scoring formulas (choose one, record it)

| Method | Formula | Behaviour |
|---|---|---|
| Lowest-price ratio | (Lowest compliant TCO / bidder TCO) x price weight | Lowest bid gets full points; others proportional; never negative |
| Linear deduction | Price weight x max(0, 1 - (bidder TCO - lowest TCO) / lowest TCO) | Steeper; a bid at double the lowest scores 0 |
| Banded | Points by percent above lowest TCO in fixed bands | Simple; record bands explicitly |

TCO for price scoring is the total computed by the response template formulas over the stated term and volumes, in the stated currency, including one-off and recurring charges. State whether optional years are included.

## Missing and abnormal prices

- A missing mandatory price line makes the bid `Incomplete`; the model states whether a clarification round is allowed. Never fill missing prices with averages unless the model, before issue, defines a loading rule and it is disclosed to bidders.
- Abnormally low bids are flagged for clarification using a rule the user sets before issue; the model does not exclude a bid on price alone without clarification.

## Change control

| Field | Content |
|---|---|
| Version | 1.0 at lock; increments on any change |
| Lock date and time | Before response deadline and before any response is opened |
| Approver | Sourcing lead or the approver named in policy |
| Change reason | Required for every version after 1.0 |
| Bidder notification | Date the change was sent to all bidders; changes after the response deadline require a restart decision by the sourcing lead |
