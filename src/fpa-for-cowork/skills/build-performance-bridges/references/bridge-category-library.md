# Bridge category library and reconciliation tests

Pick one set, edit with the user, then freeze definitions and order before calculating. Categories must not overlap and together must cover the whole movement (the remainder bar catches what they do not).

## Revenue bridge (default order)

| # | Category | Formula | Data needed |
|---|---|---|---|
| 1 | FX | End at end rates − End at start (or plan) rates | Rates by currency and period |
| 2 | Scope | Revenue of acquired units in End not in Start; minus revenue of divested units in Start | Entity list with dates |
| 3 | Volume | (ΣQ_end − ΣQ_start) × P̄_start | Units by item |
| 4 | Mix | Σ(Q_end,i × P_start,i) − ΣQ_end × P̄_start | Units and prices by item |
| 5 | Price | Σ(P_end,i − P_start,i) × Q_end,i | Prices by item |
| 6 | New items | Σ R_end,i where item absent in Start | Item list |
| 7 | Discontinued items | −Σ R_start,i where item absent in End | Item list |
| 8 | Remainder | (End − Start) − Σ(1..7) | — |

Convention: FX, then scope, then volume, mix, price on constant-currency like-for-like items. Price is measured on End quantities, so the joint price × volume effect sits in Price.

## Gross margin bridge

FX; Scope; Volume = (ΣQ_end − ΣQ_start) × Ū_start; Mix = Σ(Q_end,i × U_start,i) − ΣQ_end × Ū_start; Price = Σ(P_end,i − P_start,i) × Q_end,i; Unit cost = −Σ(C_end,i − C_start,i) × Q_end,i; New and discontinued; Remainder.

## EBITDA bridge

Revenue categories (or a single gross margin block) followed by cost categories, each with Effect = −(Cost_end − Cost_start):
- Input cost inflation (price of materials, energy, freight)
- Productivity or efficiency
- People cost (pay increases, headcount, mix) — band level only
- Other opex by agreed grouping
- One-off items (each named and evidenced)
- Remainder

## Operating cash flow bridge (from EBITDA)

| Category | Formula |
|---|---|
| EBITDA (start bar) | Source P&L |
| Receivables | −(AR_end − AR_start) |
| Inventory | −(Inv_end − Inv_start) |
| Payables | +(AP_end − AP_start) |
| Other working capital | −(Other NWC_end − Other NWC_start) |
| Non-cash items in EBITDA | + provisions charged − provisions used, etc. |
| Taxes paid | −cash taxes |
| Operating cash flow (end bar) | Source cash flow statement |

State whether interest paid is inside operating cash flow under the user's policy (IFRS allows a choice under IAS 7; US GAAP classifies interest paid as operating under ASC 230).

## Version bridge (Budget to Forecast, Forecast to Forecast)

Group by driver from the assumptions register: volume drivers, price drivers, cost drivers, timing shifts, scope, FX, other. Each amount links to the register IDs that changed.

## Headcount bridge

Opening headcount (or FTE) + Hires − Leavers + Transfers in − Transfers out ± Scope = Closing. Use one unit throughout (heads or FTE) and state it. Closing must equal the HR closing count; any difference is the remainder.

## Reconciliation tests (all must pass or be reported)

1. Start equals the source cell; End equals the source cell.
2. Σ categories + Remainder = End − Start (exact, computed).
3. Last running total = End.
4. Each subtotal = Start + Σ preceding categories.
5. |Remainder| ≤ tolerance → label Rounding; otherwise label Other — unexplained and list as open item.

## Chart-ready table rules

- Running before (row n) = Running after (row n−1); Running after = Running before + Amount.
- Invisible base = min(Running before, Running after) for increase and decrease bars; 0 for Start, Subtotal and End bars.
- Visible height = |Amount|; for Start, Subtotal and End bars, Visible height = the total.
- A bar crossing zero cannot be drawn with a single invisible base; split it at zero into two segments or use the native waterfall chart type.
