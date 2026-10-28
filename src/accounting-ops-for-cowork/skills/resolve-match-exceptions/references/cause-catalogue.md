# Cause catalogue with evidence tests and resolution paths

| Variance | Candidate cause | Evidence that confirms | Resolution path | Owner |
|---|---|---|---|---|
| Price | Contract or price list updated, PO not amended | Contract or price list version effective on or before invoice date at invoice price | Amend PO price | Buyer |
| Price | Supplier billed wrong price | Contract and PO agree; invoice differs | Request credit note or corrected invoice | Supplier via buyer or AP |
| Price | Index or surcharge applied by supplier | Invoice cites index, fuel or raw-material surcharge | Test entitlement with validate-price-increase (Procurement for Cowork); then amend PO or reject | Buyer |
| Price | Unit-of-measure mismatch | Ratio equals a pack factor | Correct unit on PO or invoice | Buyer or supplier |
| Price | Currency or FX difference | Invoice currency differs from PO currency | Corrected invoice in PO currency or PO amendment | Buyer |
| Price | Volume tier or discount not applied | Contract tier reached by cumulative volume | Request credit note | Supplier |
| Quantity | Receipt not yet posted | Delivery note, carrier proof or receiver confirmation without ERP receipt | Post goods receipt, then release | Receiver |
| Quantity | Partial delivery, invoiced in full | Back-order note or open delivery schedule | Hold until receipt or corrected invoice | Supplier and receiver |
| Quantity | Over-shipment | Received quantity exceeds ordered | Accept with PO increase or return excess | Buyer and receiver |
| Quantity | Return not credited | Return posted, no credit note | Request credit note | Supplier |
| Missing receipt | Goods or services not yet delivered | No delivery evidence | Hold | Receiver or requester |
| Missing receipt | Service PO without service confirmation | Service delivered per requester, no confirmation | Requester confirms service | Requester |
| Closed or exhausted PO | Prior invoice consumed the PO | Earlier invoice against same lines; check for duplicate | Investigate possible duplicate | AP lead |
| Closed or exhausted PO | Scope increase beyond PO | Work order or email extending scope | Change order with approval | Buyer |
| Closed or exhausted PO | PO closed prematurely | PO closure date before final delivery | Reopen PO | Buyer |
| Unmatched line | Freight or charge not on PO | Contract allows freight or charge | Amend PO or accept per policy | Buyer |
| Unmatched line | Item not ordered | No PO line, no contract basis | Reject line, request corrected invoice | Supplier |

Rules:
- A cause is Evidenced only when a document, line and date are cited. Otherwise it is Hypothesis with the confirming evidence named.
- Where two causes fit, keep both and state the deciding evidence.
- A closed or exhausted PO always triggers a duplicate check on prior invoices against the same PO lines.
