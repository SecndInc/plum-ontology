# Reports: Getting Started - Sales Manager

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### SM: Closed Won Opptys This FY by Rep [00OKc000001YCt7MAG]
folder Getting Started - Sales Manager · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.LeadSource, Opportunity.Fiscal
aggregates: Sum of Amount, Record count

### SM: New Activities Leaderboard [00OKc000001YCt8MAG]
folder Getting Started - Sales Manager · type OpportunityActivity · Matrix · last run 2021-02-03
filters: 1. Activity.CreatedDate greaterOrEqual "LAST 30 DAYS"
date: Activity.CreatedDate CUSTOM
standard: closed=all, type=te
grouped by: Activity.What.Owner.Name, Activity.Owner.Name, Activity.CreatedDate (Month)
aggregates: No. Activities
formulas: No. Activities: RowCount

### SM: New Opportunities Leaderboard [00OKc000001YCt9MAG]
folder Getting Started - Sales Manager · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CreatedDate LAST_N_DAYS:30 (2026-08-31 to 2026-09-29)
standard: terr=all, open=all, probability=>0
grouped by: CLOSE_MONTH (Month), Opportunity.Owner.Name, Opportunity.ForecastCategoryName
aggregates: Sum of Amount, Record count

### SM: Average Days to Close [00OKc000001YCtAMAW]
folder Getting Started - Sales Manager · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.CloseDate (FiscalQuarter)
aggregates: Average Age

### SM: Average Deal Size [00OKc000001YCtBMAW]
folder Getting Started - Sales Manager · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH
aggregates: Sum of Amount, Average Deal Size
formulas: Average Deal Size: AMOUNT:AVG

### SM: Closed Won Opportunities This QT [00OKc000001YCtEMAW]
folder Getting Started - Sales Manager · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Type, Opportunity.Fiscal, Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### SM: Closed Won Opportunities By FY/Month [00OKc000001YCtCMAW]
folder Getting Started - Sales Manager · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH
aggregates: Sum of Amount

### SM: Open Opportunities in the Pipeline [00OKc000001YCtFMAW]
folder Getting Started - Sales Manager · type Opportunity · Summary · last run 2021-02-03
filters: 1. CLOSED equals "False"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount, Record count

### SM: Closed Won Opportunities This Month [00OKc000001YCtDMAW]
folder Getting Started - Sales Manager · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate THIS_MONTH (2026-09-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Type, Opportunity.Fiscal, Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### SM: Win Ratio Current FY [00OKc000001YCtGMAW]
folder Getting Started - Sales Manager · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.StageName
aggregates: Sum of Amount, Win Ratio, Record count
formulas: Win Ratio: WON:SUM/CLOSED:SUM
