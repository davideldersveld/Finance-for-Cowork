# Investment policy test catalog

Build the catalog from the policy in force at the as-of date. Each row cites its clause. Rows the policy does not address are omitted, not invented.

## Catalog structure

| Test family | Typical policy content to extract | Measure | Denominator |
|---|---|---|---|
| Permitted instruments | List of eligible types (bank deposits, certificates of deposit, commercial paper, government and agency securities, money market funds by type, repurchase agreements with eligible collateral) | Holding type in list | Not applicable |
| Minimum rating — short term | For example A-1 / P-1 / F1 minimum | Rating per the policy rule | Not applicable |
| Minimum rating — long term | For example A / A2 / A minimum for issuers or deposit banks | Rating per the policy rule | Not applicable |
| Money market fund rating and type | For example government or treasury fund, AAAm or equivalent | Fund rating and type | Not applicable |
| Maximum maturity by instrument | For example deposits 6 months, commercial paper 270 days, government securities 2 years | Days to final maturity | Not applicable |
| Portfolio WAM | Maximum days | WAM | Market value |
| Portfolio WAL | Maximum days | WAL | Market value |
| Issuer concentration | Percent and absolute limit per issuer, often tiered by rating | Exposure | Total portfolio (or as defined) |
| Bank-group concentration | Aggregated across deposits, CDs, CP, repo and current-account balances where the policy includes them | Exposure by ultimate parent | Total portfolio (or as defined) |
| Sector or instrument-type limits | For example financial sector maximum, commercial paper maximum | Exposure | Total portfolio |
| Money market fund limits | Maximum per fund; maximum share of a fund's assets | Holding ÷ Portfolio; Holding ÷ Fund AUM | As stated |
| Liquidity tiers | Minimum amount or percent in each access tier | Tier total | Total portfolio or forecast need |
| Repo collateral | Eligible collateral, margin (haircut), custodian | Collateral value ÷ Repo amount | Not applicable |
| Downgrade procedure | Hold or sell requirement, notification deadline, approval | Evidence of procedure followed | Not applicable |
| Currency | Permitted currencies per entity | Holding currency | Not applicable |

## Rating rules

- **Lowest of** — use the lowest rating among the agencies the policy recognizes.
- **Second highest** (or "middle of three") — use the second-highest among available ratings; if only one exists, the policy usually requires that one to meet the floor.
- **Named agency** — use only that agency.
- Map equivalents (for example A-1 / P-1 / F1; A / A2 / A) only through the policy's own table if it has one; otherwise record each agency's rating and test each against the floor stated for it.
- A rating without a date or source is not used; mark `Not testable`.

## Formulas

- `Days to maturity = Final maturity date − As-of date` (calendar days).
- `WAM = Σ(MV × Days to maturity or next reset) ÷ Σ MV`.
- `WAL = Σ(MV × Days to final maturity) ÷ Σ MV`.
- `Concentration % = Exposure ÷ Denominator`.
- `Utilization of limit = Actual ÷ Limit` (for maximum limits); near breach when utilization ≥ the near-breach threshold.
- `Portfolio yield = Σ(MV × Yield) ÷ Σ MV`; spread to benchmark in basis points = (Portfolio yield − Benchmark yield) × 10,000 when yields are decimals.

## Status vocabulary

| Status | Rule |
|---|---|
| Compliant | Within limit and below the near-breach threshold |
| Near breach | Within limit, utilization at or above the near-breach threshold |
| Breach | Limit exceeded, rating below floor, or maturity beyond maximum |
| Permitted exception | The policy's own exception clause applies and its conditions are evidenced |
| Not permitted | Instrument type not in the permitted list |
| Not testable | Required data (rating, maturity, policy clause) missing |
