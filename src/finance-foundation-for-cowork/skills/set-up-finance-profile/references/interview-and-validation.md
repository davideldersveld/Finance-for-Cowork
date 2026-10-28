# Finance Profile — interview rounds and validation checks

## Interview rounds

Ask in rounds, one question card per round, pre-filled with any value harvested from documents (shown with its source). Skip a round entirely when every value in it is already Confirmed. Each card offers "Not provided — skip for now" for every item.

| Round | Profile sections | Questions to ask |
|---|---|---|
| 1. Organization and entities | 0, 1 | Organization name; profile owner; list of entities with code, legal name, country, functional currency, ledger, parent, ownership %, consolidation method; any dormant or divested entities to keep on record |
| 2. Currencies and calendar | 2, 3 | Group reporting currency; other reporting currencies; default presentation unit; rate source and location for closing, average, historical and budget rates; rate date and quotation conventions; fiscal year start; period pattern; adjustment periods; period naming; quarter ends; 53-week rule |
| 3. Close and chart of accounts | 4, 5 | Workday convention; holiday calendar; close tracker location; cutoff and deadline workdays; chart of accounts and mapping file locations; mapping levels; sign convention; intercompany accounts |
| 4. Thresholds | 6 | For each process the user runs: amount, currency and unit, percent, AND/OR rule, aging limit, source policy clause, approving role. Ask only for processes the user's team performs; mark the rest Not provided |
| 5. Approval limits | 7 | Transaction types in the delegation of authority; approver roles and limits; dual-approval levels; source clause |
| 6. Policies and owners | 8, 9 | Policy and working-document locations, owners, versions, review dates; team owners and backups by area |

## Harvesting candidates from documents

When the user names or attaches a delegation of authority, close calendar, entity list, reconciliation policy or chart of accounts:

- Extract only the values that map to a profile row; record each as Provisional with "Source — <document>, <page/section/clause>".
- Where two documents disagree (for example the reconciliation policy says 60 days aging and the close calendar note says 90), show both with sources in the card and let the user choose. Never pick one silently.
- Ignore and do not copy bank details, tax IDs, salaries or personal data even when present in the document.

## Validation checks before saving

Run every check in code where it involves arithmetic or pattern matching. A failed check blocks the save until the user fixes or explicitly accepts it (accepted failures are logged in the version log Reason column).

| Check | Rule |
|---|---|
| Entity codes unique | No duplicate codes in Section 1 |
| Functional currency present | Every in-scope entity has a functional currency |
| ISO currency codes | Every currency is a three-letter ISO 4217 code |
| Ownership range | 0% < ownership <= 100%; consolidation method consistent (Full normally above 50% — flag for confirmation, do not change) |
| Parent exists | Every consolidation parent is itself an entity in Section 1 or is marked as the top parent |
| Fiscal calendar arithmetic | Week-based patterns sum to 52 weeks per year (53 in a 53-week year); 4-4-5 style patterns have 13 weeks per quarter |
| Period count | Periods per year equals the pattern (12 or 13, plus adjustment periods) |
| Threshold completeness | Each threshold row with any value has currency and unit; rows with both amount and percent have an AND/OR rule |
| Threshold sense | Amounts > 0; percents between 0% and 100%; aging limits whole days |
| Approval ladder | Within each transaction type, limits ascend with approver seniority; no gaps or overlaps between bands |
| Location form | Every location is a link or a library/folder path plus file name; flag local drive letters |
| Sensitive data screen | No string matching bank account, IBAN, card, routing, tax ID or salary patterns; no compensation figures tied to a named person |
| Status filled | Every row has Confirmed, Provisional or Not provided |

## Worked check — fiscal calendar

A 4-4-5 calendar: quarter weeks = 4 + 4 + 5 = 13; year weeks = 13 x 4 = 52. In a 53-week year the extra week is added to the period the user names (commonly P12, making it 6 weeks). If the user states "4-4-5 with the extra week in P03", flag it: P03 becomes 6 weeks only in the 53-week year, and that year's Q1 is 14 weeks; confirm before saving.

## View output layout

When the user asks to view the profile, render in chat:

1. Header line — organization, profile version, last updated, owner.
2. Completeness table — section, rows Confirmed, rows Provisional, rows Not provided.
3. The sections the user asked for, as tables, exactly as stored.
4. Provisional and Not provided items list, so the user can complete them.
