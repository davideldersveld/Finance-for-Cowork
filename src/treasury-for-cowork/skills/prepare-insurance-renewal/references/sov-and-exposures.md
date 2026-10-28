# Statement of values and exposure data

Use the insurer's or broker's SOV template when supplied and keep its column order. Otherwise use the columns below. Every value cites its source (appraisal, fixed asset register, site survey, finance data) and date.

## SOV columns

| Group | Column | Notes |
|---|---|---|
| Identification | Location number, entity (named insured), site name, street address, city, state or province, postal code, country, latitude and longitude if geocoded | Business addresses only |
| Occupancy | Occupancy description and the insurer's occupancy code if requested | For example warehouse, light manufacturing, office, cold storage |
| Construction | Construction class | ISO classes: 1 Frame, 2 Joisted masonry, 3 Non-combustible, 4 Masonry non-combustible, 5 Modified fire resistive, 6 Fire resistive |
| Construction | Year built; year of last roof, electrical, plumbing and HVAC upgrades | Blank upgrade years are `Incomplete`, not "none" |
| Construction | Number of stories, basement (yes/no), gross floor area | Area in square feet or square meters, stated |
| Secondary modifiers | Roof covering, roof geometry, roof anchorage, cladding, foundation, soft story, glazing protection | Requested for wind and earthquake modeling |
| Protection | Sprinklered percent of area, system type (wet, dry, ESFR), fire alarm (local or central station), public protection class, security | |
| Exposure | Adjacent hazards, flood zone, earthquake zone, distance to coast, wildfire score, elevation | From geocoding or surveys; never inferred from the address |
| Values | Building (replacement cost unless stated) | Excludes land; follow the form on foundations and below-grade items |
| Values | Improvements and betterments | For leased sites |
| Values | Contents / business personal property | Furniture, fixtures, office equipment |
| Values | Stock / inventory | State the basis — cost or selling price — per the form |
| Values | Machinery and equipment | Including production equipment |
| Values | Electronic data processing equipment | If scheduled separately |
| Values | Business income | 12-month value on the form's basis (gross earnings or gross profit); state indemnity period |
| Values | Extra expense, rental income | If insured |
| Values | TIV | Sum of insured components |
| Valuation | Valuation basis, valuation date, last appraisal date, trend factor applied | |

## SOV checks

| Check | Rule | Label when failed |
|---|---|---|
| Footing | Components sum to TIV; locations sum to program TIV | Inconsistent |
| Blanks | Required COPE or value field blank | Incomplete |
| Zero values | Building or contents zero at an owned, occupied site | Inconsistent |
| Unit cost | Building value ÷ area outside the benchmark range the user or appraiser supplies | Inconsistent (for review) |
| Year-over-year | Absolute change by location or component above the profile threshold | Changed beyond threshold (reason required) |
| Trend | Same trend factor applied to like assets unless an appraisal supersedes | Inconsistent |
| Business income | Total BI value reconciles to the financial statements on the form's basis | Inconsistent until reconciled |
| Disposals and acquisitions | Disposed sites removed; acquired sites added with dates | Inconsistent |

Rows passing every check are `Complete`.

### Business income reconciliation

- Gross earnings basis (common on US forms): net sales and other earnings less cost of raw stock, materials and supplies consumed, and services purchased from outsiders for resale, for the next 12 months; ordinary payroll inclusion or limitation per the form.
- Gross profit basis (common on UK and Commonwealth forms): turnover less specified uninsured working expenses.
- Take the basis from the expiring form; never choose it. Use forecast figures labelled Forecast with version; show the reconciliation to reported revenue.

## Exposure data by line

| Line | Exposure items |
|---|---|
| General liability and products | Revenue by country and segment, products sold, US and Canada sales share, contractors used, recalls |
| Auto liability and physical damage | Vehicle count by type (private passenger, light, medium, heavy, extra heavy, trailers), garaging location, radius of operation, values for physical damage |
| Workers' compensation and employers' liability | Payroll by state or country and classification code, headcount, experience modification factor if supplied |
| Umbrella and excess | Schedule of underlying policies and limits |
| D&O | Financial statements, market capitalization if listed, M&A activity, securities offerings, litigation |
| Cyber | Revenue, counts of records held by type (aggregate counts only), security controls questionnaire status, outsourced critical providers |
| Crime | Employee count, financial controls, segregation-of-duties evidence |
| Marine cargo and stock throughput | Annual shipment values by route, maximum value at any one location and conveyance |

Payroll, headcount and records appear only as aggregates by location, state, class or type.
