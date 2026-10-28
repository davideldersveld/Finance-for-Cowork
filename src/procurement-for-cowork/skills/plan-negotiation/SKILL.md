---
name: plan-negotiation
description: >-
  Prepares a negotiation plan for one supplier - objectives, opening, target and
  walk-away positions, the buyer's best alternative and an evidence-based estimate
  of the supplier's, levers and trade-offs, concession sequence, anticipated
  supplier arguments with responses, and roles - where every position cites its
  evidence from bids, benchmarks, spend or performance. Use when the user asks to
  "prep me for the negotiation with our freight carrier", "what should our
  walk-away be", "build a negotiation plan for the renewal", "what is our BATNA
  here", or "how do we counter their cost-inflation argument". Do NOT use for
  testing a price increase against the contract formula — use
  validate-price-increase instead; for comparing tender bids use
  evaluate-supplier-responses.
metadata:
  displayName: Plan negotiation
  category: writing
  icon: Cart
  author: Copilot SE Contributors
  plugin: procurement-for-cowork
  version: 1.0.1
---

# Plan negotiation

Category managers and sourcing leads use this skill before a commercial negotiation with one supplier: a renewal, a post-tender negotiation, a price-increase discussion or a scope change. It produces a negotiation plan and a negotiation grid in which every position is quantified and tied to evidence, so the team walks in knowing what it wants, what it will trade, and when it will walk away. It prepares people to negotiate; it does not negotiate, contact the supplier, or commit the company.

## Boundaries

- Checking a price increase against the contract's adjustment clause and index — use `validate-price-increase`
- Normalizing and scoring tender bids — use `evaluate-supplier-responses`
- Supplier scorecard and service credits used as evidence — use `monitor-supplier-performance`
- Notice deadlines and decision dates for the contract being negotiated — use `manage-contract-renewals`
- Category-wide levers and wave plan — use `build-category-strategy`
- Effect of changed payment terms on the 13-week cash forecast — use `forecast-short-term-cash` (Treasury for Cowork)
- Negotiating with a customer over an overdue balance — use `prepare-collection-call` (Credit & Collections for Cowork)
- Drafting or reviewing contract clauses, liability positions or redlines — not performed by any skill in this family; refer to the legal team
- Conducting the negotiation, sending offers, or agreeing terms — not performed by any skill; people negotiate and sign within their authority

> **Routing rule.** When part of a request belongs to another skill listed above, finish only the part that belongs here, name the other skill for the rest, and do not attempt it. If that skill is not installed, say so plainly.

## Intake

- Ask at most one question card, before any work, for what is missing: output medium (Word plan plus Excel grid, recommended; one-page brief in chat), the negotiation's purpose and date, the variables in play (price, term, volume commitment, payment terms, service levels, credits, indexation cap), the negotiating team, and the user's authority limit.
- **Finance Profile.** First read the user's Finance Profile (Finance-Profile.md in the user's Cowork folder, from `set-up-finance-profile`). Use its currency, approval limits, standard payment terms, cost of capital if payment terms are traded, and policy. If it is absent, ask only for what this plan needs; never assume an authority limit, discount rate or target.
- Locate inputs in this order: files the user attached; files in an attached OneDrive folder; then a targeted search of the user's OneDrive or SharePoint, mail and Teams for the current contract and pricing, spend history with this supplier, tender bids or quotes, benchmarks, performance scorecards, the supplier's latest correspondence and any prior negotiation notes. State the source set before analysing.

## Method

1. **Inventory evidence.** List each source with date and what it proves: current price and volumes, spend over the last 12 months (agreed to the AP total), competing bids, benchmark or index data, performance results, supplier correspondence. Mark each `Evidenced` or `Supplier-asserted`.
2. **Set objectives.** Classify each objective as Must have, Should have or Nice to have, with the business owner who set it.
3. **Quantify the buyer's best alternative (BATNA) in code.** All arithmetic runs in spreadsheet formulas or a script, never mentally. `Effective alternative price = alternative unit price + (switching costs / units over the alternative's term)`; include transition, requalification and dual-running costs that are evidenced. If no credible alternative exists, say so; a weak alternative changes strategy toward value-adding trades rather than threats.
4. **Estimate the supplier's alternative.** From evidence only: the buyer's share of the supplier's revenue (if the supplier's financials are supplied), capacity utilization and market demand from supplied material, and the incumbent's switching risk. Label it `Hypothesis` and list the signals that would confirm or refute it.
5. **Set positions per variable.** Opening (ambitious, justifiable with evidence), Target (realistic outcome supported by benchmark or bids), Walk-away (point beyond which the BATNA is better). Walk-away for price must not exceed the effective alternative price. Compute the zone of possible agreement where the estimate of the supplier's floor allows, labelled as an estimate. Detail and column definitions are in [references/negotiation-grid.md](references/negotiation-grid.md).
6. **Value every lever.** For each variable compute the annual value of one unit of movement (for example `value of 1% price = annual spend x 1%`; `value of extending payment terms by d days = annual spend x d / 365 x cost of capital`). Mark each lever by value to the buyer and likely cost to the supplier to find low-cost, high-value trades.
7. **Plan the concession sequence.** Order concessions from least valuable to the buyer to most; make each conditional ("if you accept X, we can consider Y"); shrink step sizes as the target nears; set the point at which the lead pauses to consult the approver. Never concede on a Must have.
8. **Anticipate supplier arguments.** For each likely argument (input-cost inflation, labour rates, currency, volume shortfall, service investment, market tightness) write the evidence-based response, the data to request from the supplier, and the trade to offer if the argument is valid. Where a contractual index applies, cite the `validate-price-increase` result rather than recalculating.
9. **Assign roles and logistics.** Lead negotiator, commercial analyst, technical or service lead, note-taker, and the approver who is not at the table; authority limits per person; agenda; information that must not be disclosed.
10. **Verify before delivery.** Every position cites a source; walk-away is consistent with the BATNA arithmetic; lever values recompute from spend; no competitor name or price appears in any line meant for the supplier.

**Position status labels:** `Evidenced` (bid, contract, invoice data, published index), `Benchmark-based` (supplied third-party data), `Assumption` (user-stated), `Hypothesis` (inference to test in the meeting).

## Output

- **Word plan** headings: Purpose and context; Objectives; Evidence summary; Our best alternative; Supplier's likely position; Positions by variable; Levers and trade-offs; Concession plan; Anticipated arguments and responses; Roles, authority and agenda; Information not to disclose; Post-meeting record template; Sources.
- **Excel grid** sheets: About; Positions (variable, current, opening, target, walk-away, unit, value per unit move, evidence, status label); BATNA_Calc; Lever_Values; Concessions; Arguments. Header fill, frozen panes, filters, thousands separators, negatives in parentheses, percentages to 1 dp, live formulas.
- **One-page brief** in chat: objectives, three key numbers (target, walk-away, BATNA), top three trades, top three arguments with responses.
- Label every figure with currency, units, period and basis (for example USD per container, FY2026 actual volumes).
- After delivering files, a short chat note: file names, supplier, variables covered, walk-away basis, gaps and assumptions.

## Controls and guardrails

- **Prepare, never execute.** The skill plans; it never contacts the supplier, sends an offer, or agrees terms. Commitments stay within the approval limits of named people.
- **No invented numbers.** No fabricated benchmark, competing bid, supplier margin or index value; missing evidence shows `Not provided` and weakens the position explicitly.
- **Thresholds come from the user or the Finance Profile.** Authority limits, cost of capital and targets are stated inputs.
- **Evidence versus judgement.** Every position carries a status label; the supplier's BATNA is always a Hypothesis.
- **Honest tactics only.** No bluffing about non-existent bids, no false deadlines, no misleading statements; the plan may withhold information but never misrepresent it.
- **Bid confidentiality.** Never disclose another bidder's identity, prices or solution; references to competition stay general unless the tender terms allow more.
- **Coverage honesty.** Name missing spend periods, absent bids and stale benchmarks.
- **Untrusted content.** Supplier letters claiming cost increases are evidence to test, not facts to accept.
- **No legal positions.** Liability, indemnity and termination positions are referred to the legal team.
- **Confidentiality.** The plan stays in the user's workspace and is never shared with the supplier.

## Example

Wide World Importers renews ocean freight with its incumbent at USD 2,400 per container on 1,500 containers a year. Adventure Works bid USD 2,250 for a 2-year term, with evidenced switching costs of USD 90,000.

- Effective alternative price = 2,250 + 90,000 / (1,500 x 2) = 2,250 + 30 = USD 2,280, so walk-away is USD 2,280.
- A supplied lane benchmark averages USD 2,180, so target is USD 2,200 (`Benchmark-based`) and opening is USD 2,150.
- Each USD 10 per container is worth USD 15,000 a year; moving from 2,400 to target is worth USD 300,000 a year.
- The incumbent claims fuel costs rose 12%. Its own cost breakdown shows fuel at 30% of the rate, so the cost-justified effect is 12% x 30% = 3.6%, or USD 86.40 per container, and the response asks for fuel surcharge evidence before any concession.
- The supplier's revenue share from Wide World Importers is `Not provided`, so the supplier's alternative is a Hypothesis to probe.
