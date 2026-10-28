# Statement build rules

Paragraph references are navigation aids. Retrieve authoritative text before relying on a presentation requirement, and follow the entity's prior issued statements for line structure unless the user directs a change.

## Mapping rules

1. One account maps to one face line, one account class (Asset, Liability, Equity, Income, Expense) and one cash flow category.
2. Accounts that change sign between periods (bank accounts in overdraft, intercompany positions) carry a sign-dependent rule stated on the Mapping sheet, for example "debit to Cash and cash equivalents, credit to Short-term borrowings", applied consistently with the cash definition in the policy.
3. Suspense, clearing and unallocated accounts with a balance are listed on Open_Items and referred for reconciliation; they are mapped only on user direction.
4. Record the mapping version and its source (Finance Profile, prior statements or user template).

## Balance sheet

- Classify current versus non-current using the operating cycle and the 12-month rule (ASC 210-10-45; IAS 1.66 and 1.69). Debt with covenant breaches or callable features needs controller confirmation of classification; list it on Open_Items.
- Present non-controlling interests within equity, separately from parent equity (ASC 810-10-45-16; IFRS 10.22).

## Income statement and comprehensive income

- Use the function or nature format the entity already uses. For IFRS reporters in annual periods beginning on or after 1 January 2027, apply IFRS 18 categories (operating, investing, financing, income taxes, discontinued operations) and required subtotals; retrieve the standard for the classification rules and note management-defined performance measures for disclosure.
- Present comprehensive income either as one continuous statement or two consecutive statements, per prior practice.
- Attribute net income and comprehensive income between the parent and non-controlling interests.

## Statement of changes in equity

Columns by component: share capital, additional paid-in capital or share premium, treasury shares, retained earnings, each accumulated other comprehensive income component, parent total, non-controlling interests, total. Rows: opening balance, adjustments for restatement or change in accounting policy, net income, other comprehensive income, dividends declared, share issuances, share-based payment, treasury share transactions, transactions with non-controlling interests, closing balance.

## Cash flow statement - indirect method

### Starting point

- US GAAP: net income, including the amount attributable to non-controlling interests (ASC 230-10-45-28).
- IFRS: use the starting subtotal required by IAS 7 as currently amended; when IFRS 18 applies, retrieve the amended IAS 7.18 and 7.20 to confirm the starting subtotal and the classification of interest and dividends. Bridge the starting subtotal to net income on the CF_Workings sheet so C3 can run.

### Adjustments and working capital

1. Add back non-cash items: depreciation, amortization, impairment, share-based payment, deferred tax, unrealized gains and losses, equity-method results net of dividends received, gains or losses on disposal (the proceeds go to investing).
2. Working capital changes come from balance sheet movements after removing non-cash and non-operating parts of each movement: acquisitions and disposals of subsidiaries, foreign currency translation, reclassifications, accrued capital expenditure in payables, interest payable where interest paid is classified outside operating.
3. Under US GAAP, interest paid and income taxes paid are disclosed (ASC 230-10-50-2); under IFRS, interest and dividends are classified consistently per the entity's policy and IAS 7 as amended.

### Investing and financing

- Capital expenditure = additions per the fixed asset roll-forward - unpaid additions at period end + prior-period accrued additions paid this period. Right-of-use asset additions are non-cash.
- Disposal proceeds = carrying amount disposed + gain (or - loss), adjusted for proceeds receivable.
- Borrowings and repayments from the debt schedule, gross where required; principal portion of finance lease payments in financing.
- Equity: proceeds from share issuances, treasury share purchases, dividends paid (declared minus movement in dividends payable).

### Exchange rate effect and cash definition

- Present the effect of exchange rate changes on cash held in foreign currencies as a separate reconciling line (ASC 830-230-45-1; IAS 7.28). Source it from translation workings.
- Cash and cash equivalents follow the entity's definition. Under US GAAP the reconciliation includes restricted cash and restricted cash equivalents; under IFRS, bank overdrafts repayable on demand may form part of cash where they are integral to cash management (IAS 7.8).

### Non-cash activities

List significant non-cash investing and financing transactions for disclosure: right-of-use assets obtained for lease liabilities, debt-to-equity conversions, accrued capital expenditure, and acquisitions settled in shares (ASC 230-10-50-3 to 50-6; IAS 7.43).

## CF_Workings layout

| Balance sheet line | Opening | Closing | Movement | Operating | Investing | Financing | Non-cash | FX translation | Residual |
|---|---|---|---|---|---|---|---|---|---|

`Residual = Movement - sum of allocation columns`. Every residual must be zero (check C7).
