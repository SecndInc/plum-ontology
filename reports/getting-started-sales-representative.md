# Reports: Getting Started - Sales Representative

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### SR: Closed Won Opportunities MTD [00OKc000001YCtKMAW]
folder Getting Started - Sales Representative · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH
aggregates: Sum of Amount

### SR: Top Accounts by Revenue Amt [00OKc000001YCtHMAW]
folder Getting Started - Sales Representative · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### SR: Closed Won Opportunities By FY/Month [00OKc000001YCtJMAW]
folder Getting Started - Sales Representative · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH
aggregates: Sum of Amount

### SR: Neglected Accounts [00OKc000001YCtMMAW]
folder Getting Started - Sales Representative · type AccountActivity · Summary · last run 2021-02-03
filters: 1. Activity.ActivityDate lessThan "LAST 90 DAYS"
date: Activity.ActivityDate CUSTOM
standard: closed=open, type=te
grouped by: Activity.Account.Name
aggregates: Record count

### SR: Open Opportunities in the Pipeline [00OKc000001YCtNMAW]
folder Getting Started - Sales Representative · type Opportunity · Summary · last run 2021-02-03
filters: 1. CLOSED equals "False"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount, Record count

### SR: Closed Won Oppty This QT [00OKc000001YCtLMAW]
folder Getting Started - Sales Representative · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Type, Opportunity.Fiscal, Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### SR: Stuck Opportunities Report [00OKc000001YCtOMAW]
folder Getting Started - Sales Representative · type Opportunity · Matrix · last run 2021-02-03
filters: 1. Opportunity.CloseDate lessOrEqual "TODAY"; 2. Stage Duration greaterOrEqual "90"
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.StageName, Opportunity.CloseDate (Month)
aggregates: No. Opportunities
formulas: No. Opportunities: RowCount
