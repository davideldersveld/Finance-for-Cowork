# Root cause and evidence matrix

Assign one primary root cause per case. Record each evidence item as `Found`, `Not found` or `Not accessible` with its document and page or row.

| Root cause | Typical customer reason | Evidence to gather | Recalculation | Common resolution | Default owner (confirm in profile) |
|---|---|---|---|---|---|
| Pricing | "Wrong price", "price per contract" | Customer PO price, contract or price list in force on order date, price change notices, quote, invoice line | `Expected = Price in force x Invoiced quantity`; `Variance = Invoiced - Expected` | Credit note for variance, or rebill if every line is wrong | Sales operations or pricing |
| Quantity or short shipment | "Short shipped", "received less" | Sales order, pick and pack records, delivery note, signed POD with exceptions noted, carrier records | `Variance = (Invoiced qty - Delivered qty per POD) x Unit price` | Credit for undelivered units if POD shows shortage; deny if clean signed POD | Logistics or warehouse |
| Damage or quality | "Damaged", "defective", "rejected" | POD exception notes, photos, returns authorization, quality inspection, warranty terms, return receipt | Credit amount = units returned or accepted as defective x unit price, within contract remedy | Credit after return or inspection; carrier claim if transit damage | Quality or customer service; logistics for carrier claim |
| Proof of delivery | "Not received" | Signed POD, carrier tracking, delivery address against order | None unless partial | Deny with POD, or reship or credit if no POD | Logistics |
| Promotion or trade deduction | Promotion code, "allowance", "co-op", "rebate" | Trade or promotion agreement (dates, eligible products, rate, caps), proof of performance, accrual records, prior settlements | `Allowable = Eligible qty in promotion period x Agreed rate`, capped per agreement; `Unsupported = Deducted - Allowable` | Settle allowable amount; deny excess or duplicates | Trade marketing or key account management |
| Tax | "Exempt", "wrong rate" | Invoice tax lines, exemption certificate on file and in date, ship-to jurisdiction | Show tax difference only; treatment question goes to Tax | Rebill with corrected tax once Tax confirms | Tax team |
| Duplicate billing | "Billed twice" | Both invoices, orders, deliveries, POs | Same PO, quantity and amount with one delivery equals duplicate | Credit the duplicate invoice | Billing |
| Unauthorized deduction | No reason or unrecognized code | Remittance, customer deduction code list, correspondence | None | Request reason and support from customer; deny if none within policy window | Deduction analyst |
| Not a dispute | "Awaiting funds", "approval pending" | Correspondence | None | Return to collections; not a dispute | Collector |

## Claim window check

`Days to claim = Date raised - Delivery date` (or invoice date if the contract measures from invoice). Compare with the window in the contract, terms and conditions or dispute policy. Record `Within window`, `Outside window` or `Window not provided`. An outside-window claim is presented to the owner with that fact; the owner decides.

## Validity labels

| Label | Rule |
|---|---|
| `Valid` | Recomputed variance supports the claimed amount within tolerance. |
| `Partially valid` | Evidence supports part; valid and invalid portions quantified and summing to the claim. |
| `Invalid` | Evidence contradicts the claim. |
| `Insufficient evidence` | A required evidence item is not found; holder named. |
| `Pending customer documents` | Customer must provide support; request date recorded. |

## Aging and cycle time

- `Case age = As-of date - Date raised` (calendar days).
- `Cycle time (closed cases) = Date resolved - Date raised`.
- Report count, amount, median and mean age by cause and owner.
