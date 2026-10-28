# SoD rules, register columns and statuses

## 1. Illustrative starter rule list (draft only — user must confirm)

These function pairs are common finance conflicts. Offer them only when the user has no rule set, labeled "Illustrative — not the company's rule set until confirmed". Risk ratings are left for the user to assign.

| Rule ID | Function A | Function B | Typical risk |
|---|---|---|---|
| S-01 | Create or change supplier master data | Enter supplier invoices | Fictitious supplier invoicing |
| S-02 | Create or change supplier master data | Release or approve payment runs | Payment diversion |
| S-03 | Enter supplier invoices | Release or approve payment runs | Unauthorized payment |
| S-04 | Create purchase orders | Record goods receipts | Payment for goods not received |
| S-05 | Create or change customer master data or credit limits | Enter sales orders or invoices | Unauthorized sales or credit |
| S-06 | Enter customer invoices or credit memos | Apply cash receipts | Concealment of misappropriated receipts |
| S-07 | Create journal entries | Approve or post journal entries | Unauthorized or unreviewed entries |
| S-08 | Maintain chart of accounts or posting periods | Create journal entries | Posting to closed periods or new accounts unreviewed |
| S-09 | Maintain fixed asset master data | Approve asset disposals or retirements | Unrecorded asset loss |
| S-10 | Maintain employee master or pay rates | Approve or release payroll | Ghost employees or pay manipulation |
| S-11 | Security administration (assign roles) | Any financial transaction function | Self-granted access |
| S-12 | Program change development | Migrate changes to production | Unauthorized changes |
| S-13 | Maintain bank master or payment files | Approve payment runs | Altered payment files |
| S-14 | Inventory count adjustments | Inventory receiving or shipping | Concealment of inventory loss |

## 2. Conflict Register columns

Register ID; System; User ID; Name; Department and job role (from HR); Match label; Issue type (SoD conflict / Privileged access / Generic or shared / Orphan / Leaver / Mover / Joiner / Dormant); Rule ID and description; Risk rating (from rule set); Roles granting function A; Roles granting function B; Evidence (listing file and row; HR row); Days metric (days after termination, days since last login, as applicable); Mitigating control ID; Mitigation status; Activity check (Performed both functions / Did not perform both / Activity check needed); Recommended action (Remove role / Disable account / Assign owner / Document and test mitigation / Request exception approval); Action owner role (role owner, line manager, system owner); Register status; Due date (left blank for the owner); Notes.

## 3. Register statuses

| Status | Applies when |
|---|---|
| Open — unmitigated | Conflict or issue present and no mitigating control linked |
| Open — mitigation documented, not tested | Mitigation exists in the library but no test workpaper is cited |
| Mitigated — tested | Mitigation has a cited test with no exceptions for the period |
| Accepted risk — approved exception | Written approval with approver role and expiry date; expired approvals revert to Open |
| Resolved — access removed | Evidence shows removal, with date |
| Leaver — active access | Leaver account active as of the listing date |
| Leaver — removed late | Removed, but days active after termination exceeded policy |
| Leaver — activity after termination | A login is recorded after the termination date; for access-owner follow-up only |
| Mover — prior access retained | Prior-role access held beyond policy days |
| Dormant | Days since last login above the policy dormancy period |
| Orphan account | No HR match, not generic, service or external |

## 4. Summary counts (formulas)

- `Accounts = Matched — ID + Matched — email + Matched — name only + No HR match`
- `No HR match = Generic or shared + Service or system + External + Orphan`
- `Conflicts total = SUM(conflicts by rule)`; also by risk rating, system and mitigation status.
- Leaver rate = leavers with active access / leavers in period (1 dp).
