# Lease abstract fields and import layout

Every field takes one status: Abstracted - clause cited, Derived - calculation shown, Judgement input - controller to conclude, Conflict - documents disagree, Not provided. Paragraph references are navigation aids; retrieve the authoritative text before citing it in a deliverable.

## 1. Identification

| Field | Definition and rule |
|---|---|
| Lease ID | User's lease system ID if one exists; otherwise a temporary ID marked Temporary |
| Lessee entity | Legal entity as named in the lease; map to the Finance Profile entity code |
| Lessor | Counterparty legal name |
| Asset class | Real estate, vehicles, equipment, IT, other (per the user's policy classes) |
| Asset description and location | Premises, unit, serial or fleet numbers |
| Identified asset evidence | Explicit or implicit specification; substitution rights and whether substantive |
| Economic benefits and direction of use | Who decides how and for what purpose the asset is used |
| Contains a lease | Yes / No / Judgement input |

## 2. Dates

| Field | Rule |
|---|---|
| Inception date | Earlier of agreement date or commitment to principal terms |
| Commencement date | Date the lessor makes the asset available for use (including fit-out access) |
| Rent commencement date | First date rent is payable; may follow commencement |
| Non-cancellable end date | Commencement plus non-cancellable term, less one day |
| Lease term end date | Derived after option conclusions; until concluded show the non-cancellable end date and mark the term as a judgement input |

## 3. Options

One row per option: type (extend, terminate, purchase), clause, holder (lessee, lessor, both), notice period, exercise window, price or rent basis (fixed, percentage of market, market), penalty, and indicators:

- Contract-based: option rent versus current market, penalties, residual value guarantees.
- Asset-based: significant leasehold improvements expected to have value beyond the option date.
- Entity-based: relocation cost and disruption, importance of the asset, past practice, management intent evidenced in plans.
- Market-based: availability and cost of alternatives.

References: ASC 842-10-30-1 and 842-10-55-26; IFRS 16.18 to 16.21 and B34 to B41.

## 4. Payments

| Field | Rule |
|---|---|
| Base payment | Amount, frequency, in advance or arrears |
| Escalation type | Fixed percentage, fixed amount, index-linked, market review, none |
| Escalation rate or index | Rate, or index name, base date and commencement value (from the document or user; never estimated) |
| Escalation dates | Anniversary or calendar dates as stated |
| Caps and floors | For index-linked escalations |
| Free rent periods | Months and amounts waived |
| In-substance fixed payments | Payments variable in form but unavoidable in substance |
| Excluded variable payments | Sales-based, usage-based, actual operating cost recoveries |
| Non-lease components | Services and maintenance amounts, and whether the separation election applies |
| Residual value guarantee | Amount and the framework's measurement basis |
| Purchase option price | Included only if exercise is concluded reasonably certain |
| Termination penalty | Included only if the term reflects exercise of the termination option |

## 5. Incentives, costs and obligations

| Field | Rule |
|---|---|
| Lease incentives | Free rent, tenant improvement allowance, reimbursements; amount, conditions, timing, whether received or receivable at commencement |
| Initial direct costs | Incremental costs of obtaining the lease only (for example a broker commission contingent on signing); list excluded costs and why |
| Prepaid rent at commencement | Payments made at or before commencement |
| Restoration obligation | Clause and description; amount from the user (IFRS includes the estimate in the right-of-use asset; under US GAAP it is assessed separately) |
| Security deposit | Amount and refundability (not a lease payment if refundable) |

## 6. Discount rate

| Field | Rule |
|---|---|
| Rate implicit readily determinable | Yes / No, with reason |
| Rate used | As supplied |
| Rate source and date | Treasury memo, controller schedule |
| Basis | Term-matched, currency, collateralized, entity or group |
| Private company election | Risk-free rate by asset class, if elected (US GAAP) |

## 7. Classification inputs

| Criterion | Input and computation |
|---|---|
| Transfer of ownership | Clause, Yes / No |
| Purchase option reasonably certain | Link to option row |
| Term versus economic life | `Lease term / Remaining economic life`, compared with the policy threshold; economic life from the user or asset register |
| Present value versus fair value | `PV of lease payments plus guaranteed residual / Fair value of asset`, compared with the policy threshold; fair value from the user |
| Specialized asset | Evidence of no alternative use to the lessor |
| End-of-life exception | Whether commencement falls at or near the end of economic life per the policy |

IFRS lessees do not classify; record short-term and low-value eligibility instead.

## 8. Measurement preview formulas

- Monthly rate `i = annual rate / 12` unless the policy compounds differently.
- Payments in advance: `PV = sum of P_t / (1 + i)^(t - 1)` for t = 1 to n.
- Payments in arrears: `PV = sum of P_t / (1 + i)^t`.
- `Right-of-use asset = Lease liability + prepaid rent - incentives received + initial direct costs (+ restoration estimate under IFRS)`.

## 9. Import layout (default)

When the user has no lease system template, use these columns: Lease ID, Entity, Lessor, Asset class, Location, Commencement, End date, Term months, Payment frequency, Timing, Currency, Payment schedule reference, Discount rate, Initial direct costs, Incentives, Prepaid rent, Classification, Exemption applied, Status, Source document.
