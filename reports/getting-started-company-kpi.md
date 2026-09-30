# Reports: Getting Started - Company KPI

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### KPI: Average Days to Close [00OKc000001YCt0MAG]
folder Getting Started - Company KPI · type Opportunity · Matrix · last run 2025-12-12
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.CloseDate (FiscalQuarter)
aggregates: Average Age

### KPI: Average Deal Size [00OKc000001YCt1MAG]
folder Getting Started - Company KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. Opportunity.Amount notEqual ""
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.CreatedDate (Month)
aggregates: Average Deal Size, Record count
formulas: Average Deal Size: AMOUNT:SUM / RowCount

### KPI: Open Opportunities in the Pipeline [00OKc000001YCt4MAG]
folder Getting Started - Company KPI · type Opportunity · Summary · last run 2025-12-12
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount, Record count

### KPI: Total Win Ratio [00OKc000001YCt5MAG]
folder Getting Started - Company KPI · type Opportunity · Summary · last run 2025-12-12
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.StageName
aggregates: Sum of Amount, Win Ratio, Record count
formulas: Win Ratio: WON:SUM/CLOSED:SUM

### KPI: Closed Won and >=70% Prob Opptys [00OKc000001YCt6MAG]
folder Getting Started - Company KPI · type Opportunity · Matrix · last run 2025-12-12
filters: 1. WON equals "True"; 2. CLOSED equals "False"; 3. Opportunity.Probability greaterOrEqual "70" · logic 1 or (2 and 3)
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.CloseDate (FiscalQuarter), Opportunity.ForecastCategoryName
aggregates: Sum of Amount, Record count

### KPI: Closed Won Opptys By FY/Month [00OKc000001YCt2MAG]
folder Getting Started - Company KPI · type Opportunity · Matrix · last run 2025-12-12
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH
aggregates: Sum of Amount

### KPI: Closed Won Opportunities By FY/QT [00OKc000001YCt3MAG]
folder Getting Started - Company KPI · type Opportunity · Summary · last run 2025-12-12
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.CloseDate (FiscalQuarter)
aggregates: Cumulative Total to Date, Total per Quarter, Record count
formulas: Cumulative Total to Date: NULLVALUE(PREVGROUPVAL(AMOUNT:SUM, CLOSE_DATE, 1),0) + 

NULLVALUE(PREVGROUPVAL(AMOUNT:SUM, CLOSE_DATE,2),0) + 

NULLVALUE(PREVGROUPVAL(AMOUNT:SUM, CLOSE_DATE,3),0) + 

NULLVALUE(AMOUNT:SUM,0); Total per Quarter: AMOUNT:SUM
