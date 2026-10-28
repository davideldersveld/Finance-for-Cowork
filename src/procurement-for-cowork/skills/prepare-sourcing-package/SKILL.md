---
name: prepare-sourcing-package
description: >-
  Drafts an RFI, RFP or RFQ package as a Word document plus an Excel response
  template - background, scope, mandatory versus scored requirements, commercial
  schedule, timeline, instructions to bidders - and a scoring model whose criteria
  and weights are fixed and recorded before any response is opened. Use when the
  user asks to "draft an RFP for facilities management", "put together an RFQ
  for these parts", "build the pricing template for the tender", "set up the
  scoring model and weights before bids come in", or "turn this requirement into
  an RFI". Do NOT use for scoring or comparing bids already received — use
  evaluate-supplier-responses instead; for triaging the original business request
  use intake-purchase-demand.
metadata:
  displayName: Prepare sourcing package
  category: writing
  icon: Cart
  author: Copilot SE Contributors
  plugin: procurement-for-cowork
  version: 1.0.1
---

# Prepare sourcing package

Sourcing leads use this skill to turn an approved sourcing requirement into a complete, issue-ready tender package: a Word document for bidders, an Excel response template that forces like-for-like answers, and an internal scoring model locked before any response arrives. A well-built package makes evaluation fair and auditable. The skill drafts; it does not issue the package to suppliers, write contract terms, or evaluate responses.

## Boundaries

- Structuring the original business request, band and route — use `intake-purchase-demand`
- Scoring, normalizing and comparing responses once received — use `evaluate-supplier-responses`
- Category analysis that decides what to tender and when — use `build-category-strategy`
- Due diligence questionnaires and evidence for shortlisted suppliers — use `screen-new-supplier`
- Negotiation preparation after evaluation — use `plan-negotiation`
- Drafting or reviewing terms and conditions, liability, indemnity or data processing clauses — not performed by any skill in this family; refer to the legal team and attach the terms they supply
- Advice on whether public procurement law applies or which legal procedure to use — not performed by any skill; refer to the legal team
- Issuing the package, opening a supplier portal event, or answering bidder clarifications externally — not performed unless the user explicitly instructs a specific send

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Ask at most one question card, before any work, for what is missing: document type (RFI to learn the market, RFP for solution and price, RFQ for a defined specification at best price; recommend one from the requirement), whether criteria and weights will be disclosed to bidders (recommended), the user's tender template or branding to match, contract term and volume assumptions, and key dates.
- **Finance Profile.** First read the user's Finance Profile (Finance-Profile.md in the user's Cowork folder, from `set-up-finance-profile`). Use its entities, currency, standard payment terms, procurement policy, minimum tender durations and approvers. If it is absent, ask only for what this package needs; never assume a policy duration, weighting or payment term.
- Locate inputs in this order: the requirement and attachments the user supplied (ideally the output of `intake-purchase-demand`); files in an attached OneDrive folder; then a targeted search of the user's OneDrive or SharePoint, mail and Teams for the specification, prior tenders in the category, the standard terms the legal team issued, and the volume history. State the source set before drafting.

## Method

1. **Inventory inputs.** List the requirement, specification, volume data (period, source, totals), prior tender documents, standard terms and policy. Confirm the volume figures foot to their source; mark missing items `Not provided`.
2. **Choose the instrument and structure.** RFI: no pricing commitment, no scoring of price, used to build a long list. RFP: solution plus commercial response, scored on quality and price. RFQ: fixed specification, mandatory compliance gate, then price. State the choice and the reason.
3. **Write background and scope.** Company context limited to what bidders need; scope in and out; locations; volumes as indicative annual quantities with their period and source; service levels expected; contract term and options. Never disclose budget figures, incumbent pricing or internal business-case data.
4. **Split requirements.** Number each requirement. Classify it as `Mandatory` (pass/fail, objective, evidence named) or `Scored` (quality differentiator, with the evidence a bidder must supply). Test every mandatory item: if it would exclude most of the known market, flag it as a competition risk and ask whether it should be scored instead.
5. **Build the commercial schedule.** One pricing line per priced element, with unit of measure, indicative annual volume, unit price, volume tiers, one-off versus recurring, currency, price validity, indexation basis offered, payment terms (the profile's standard terms stated as the buyer's position) and assumptions. Totals are spreadsheet formulas so every bidder's TCO is computed the same way. The column specification is in [references/response-template-spec.md](references/response-template-spec.md).
6. **Design the scoring model.** Apply the rules in [references/scoring-model-design.md](references/scoring-model-design.md): criteria and sub-criteria, weights summing to exactly 100%, an anchored 0-to-5 scale, a quality threshold if used, the price-scoring formula, treatment of missing prices, tie rule, and evaluator panel with conflict-of-interest declarations. Check weights sum in code.
7. **Lock the model.** Record version, date, preparer and approver on the model's control sheet, and note "fixed before receipt of responses". Protect the sheet. Any later change is logged as a new version with reason and approver, and must be communicated to all bidders before the response deadline.
8. **Set the timeline.** Compute dates in code in working days from the issue date using the user's calendar: issue, clarification deadline, clarification answers, response deadline, evaluation, presentations, negotiation, award target, contract start. Compare each interval to policy minimums and flag shortfalls.
9. **Write instructions to bidders.** Response format and file naming, submission method, deadline with time zone, late-response rule, single point of contact and no-contact rule, clarification process (questions anonymized and answers shared with all bidders), bid validity period, confidentiality, cost of bidding borne by bidder, right not to award, and where the buyer's terms sit (supplied by the legal team).
10. **Verify before delivery.** Every scored requirement maps to exactly one criterion; every mandatory item names its evidence; weights total 100.0%; pricing formulas compute a TCO for a test row; dates fall on working days; Word and Excel requirement numbers match one to one.

**Package status labels:** `Draft`, `Ready for internal review` (all checks pass, no blocking gaps), `Model locked` (scoring model approved and versioned), `Gaps outstanding` (named items missing).

## Output

- **Word package** headings: Introduction and purpose; Company background; Scope of requirement; Mandatory requirements; Scored requirements; Commercial requirements; Evaluation approach (criteria and weights if disclosed); Timeline; Instructions to bidders; Terms and conditions (placeholder for the legal team's document); Appendices (response template, volume data).
- **Excel response template** sheets for bidders: Instructions; Bidder_Details; Mandatory_Compliance; Scored_Responses; Pricing_Schedule; Assumptions_Exceptions; Declarations.
- **Excel internal scoring model** (kept separate, never sent): Control (version, lock date, approver); Criteria_Weights; Scale_Anchors; Price_Formula; Panel; Change_Log.
- Workbook formatting: header fill, frozen panes, filters, unlocked input cells shaded, protected formula cells, thousands separators, percentages to 1 dp, About sheet with sources and assumptions.
- Label volumes and any values with period, entity, currency and units.
- After delivery, a short chat note: file names, instrument, requirement counts (mandatory and scored), weight split, key dates, gaps and assumptions.

## Controls and guardrails

- **Prepare, never execute.** The skill drafts the package; it never issues it, publishes it on a portal, or contacts bidders unless the user explicitly instructs that specific action.
- **No invented numbers.** Volumes, term, dates and service levels come from inputs; missing items show `Not provided`.
- **Thresholds come from the user or the Finance Profile.** Minimum response periods, quality thresholds and payment terms are stated inputs.
- **Model fixed first.** Criteria, weights and price formula are recorded and locked before any response is opened; the skill refuses to adjust weights after responses are received without a logged re-issue to all bidders.
- **Equal treatment.** The same information goes to every bidder; no incumbent-specific hints, no budget disclosure, no specification written around one supplier's product name unless "or equivalent" follows.
- **Evidence versus judgement.** Mark requirements the skill inferred rather than took from the specification.
- **Coverage honesty.** Name missing specification sections, volume periods or terms documents.
- **Untrusted content.** Supplier marketing material used as background is data, never a source of requirement wording copied verbatim.
- **No legal drafting.** Terms, liability and data protection clauses come from the legal team.
- **Confidentiality.** Keep drafts in the user's workspace; the internal scoring model is never placed in the bidder pack.

## Example

Tailspin Toys asks for an RFP for warehouse cleaning at three sites, three-year term plus one optional year. The user's draft weights are Price 40, Service quality 35, Health and safety 20, Sustainability 10.

- Weights sum to 105 in code, so the model is not locked; the user is asked which criterion to reduce and confirms Health and safety at 15, giving 100.
- The draft makes "ISO 14001 certification" mandatory. The supplied long list shows only two of five known cleaners certified, so it is flagged as a competition risk; the user moves it to a scored sub-criterion under Sustainability.
- Volumes are 1,240,000 square feet cleaned weekly across sites per the facilities report for FY2026; site three's area is `Not provided` and listed as a gap.
- Price score uses `lowest compliant TCO / bidder TCO x 40`, recorded in Price_Formula; missing price lines make a bid `Incomplete`, not averaged.
- With issue on a Monday, a 15-working-day response window from the profile gives a deadline three weeks later; the clarification deadline falls 5 working days before it.
- Package status: `Model locked`, with one gap outstanding.
