# Spend analysis rules — formulas, interpretation bands and positioning rubric

All calculations are performed in spreadsheet formulas or a script. Shares are computed on addressable spend unless stated otherwise.

## Core formulas

| Measure | Formula | Notes |
|---|---|---|
| Addressable spend | Total spend - exclusions | Exclusions listed by type with totals |
| Supplier share | Supplier addressable spend / subcategory addressable spend | Parent-level after grouping |
| Cumulative share (Pareto) | Running sum of shares, suppliers sorted descending | Tail = suppliers after cumulative share passes the user's cut-off (80% if the user agrees) |
| Top-N share | Sum of the N largest supplier shares | Report N = 1 and 3 |
| HHI | Sum over suppliers of (share in percent)^2 | Range 0 to 10,000 |
| Contract coverage | Spend with suppliers under an active contract on the transaction date / addressable spend | Active = start date <= transaction date <= end date |
| PO coverage | Spend with a PO reference / addressable spend | Exclude PO numbers created after the invoice date and report them as retrospective POs |
| Unit-price dispersion | (Max unit price - min unit price) / min unit price | Same item code and unit of measure only |
| Price harmonization upper bound | Sum over lines of (unit price - lowest observed unit price) x quantity | Label as upper bound |
| Average transaction size | Spend / transaction count | Low values suggest catalogue or card channel |

## HHI interpretation bands

These bands follow common competition-analysis practice. Use the user's own bands if supplied.

| HHI | Band |
|---|---|
| Below 1,500 | Unconcentrated |
| 1,500 to 2,500 | Moderately concentrated |
| Above 2,500 | Highly concentrated |

Interpret buyer-side HHI as dependency on a few suppliers, not as a market-wide measure; market concentration comes from supplied market material.

## Positioning rubric (supply risk versus spend impact)

Score each subcategory 1 (low) to 5 (high). Record the evidence for each sub-score. Average the sub-scores within each axis; 3.0 and above is High.

**Spend impact**

| Sub-score | 1 | 3 | 5 |
|---|---|---|---|
| Share of total addressable spend | Small share relative to other subcategories | Middle third | Top third |
| Effect on product cost or margin | Overhead only | Indirect effect | Direct input to cost of goods sold |
| Price volatility exposure | Stable, fixed-price contracts | Some indexation | Commodity-linked, frequent changes |

**Supply risk**

| Sub-score | 1 | 3 | 5 |
|---|---|---|---|
| Qualified suppliers available | Many | Few | One or two |
| Switching cost and time | Days, low cost | Months | Requalification over a year or tooling change |
| Market concentration | Fragmented | Moderate | Dominated by few players |
| Lead time and capacity | Short, ample capacity | Moderate | Long or constrained |
| Geographic or regulatory exposure | Local, unregulated | Some cross-border | Single region at risk or heavily regulated |

**Quadrants**

| Spend impact | Supply risk | Position | Typical levers |
|---|---|---|---|
| High | Low | Leverage | Competitive tender, volume consolidation, price harmonization, e-auction |
| High | High | Strategic | Long-term partnership, joint cost reduction, should-cost, dual sourcing, risk sharing |
| Low | High | Bottleneck | Supply assurance, safety stock, specification change, alternative qualification |
| Low | Low | Non-critical | Catalogue, purchasing card, demand management, tail consolidation, automation |

## Wave plan columns

Initiative | Subcategory | Position | Lever | Addressable spend in scope | Opportunity range low | Opportunity range high | Range basis (Assumption source) | Driving date (notice deadline or expiry) | Wave | Start quarter | End quarter | Owner | Dependencies | Evidence label
