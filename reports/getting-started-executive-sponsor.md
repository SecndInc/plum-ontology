# Reports: Getting Started - Executive Sponsor

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### ES: Closed Won Opportunities By FY/QT [00OKc000001YCsuMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH (FiscalQuarter)
aggregates: Sum of Amount

### ES: Closed Lost Opportunities FYTD [00OKc000001YCssMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Matrix · last run 2021-02-03
filters: 1. WON equals "False"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.CloseDate (FiscalQuarter)
aggregates: Sum of Amount, Record count

### ES: Average Deal Size [00OKc000001YCsrMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Summary · last run 2021-02-03
filters: 1. Opportunity.Amount notEqual ""
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.CreatedDate (Month)
aggregates: Average Deal Size, Record count
formulas: Average Deal Size: AMOUNT:SUM / RowCount

### ES: Closed Won Opportunities By FY/Month [00OKc000001YCstMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name, CLOSE_MONTH (Month)
aggregates: Sum of Amount

### ES: FYTD Won Opportunities by Acct [00OKc000001YCswMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Account.Name, Opportunity.Account.Owner.Name, Opportunity.CloseDate (Month)
aggregates: Sum of Amount, Record count

### ES: FYTD Open Opportunities by Acct [00OKc000001YCsvMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Matrix · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Account.Name, Opportunity.Account.Owner.Name, Opportunity.CloseDate (Month)
aggregates: Sum of Amount, Record count

### ES: Open Opportunities in the Pipeline [00OKc000001YCsyMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount, Record count

### ES: Total Win Ratio [00OKc000001YCszMAG]
folder Getting Started - Executive Sponsor · type Opportunity · Summary · last run 2021-02-03
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.StageName
aggregates: Sum of Amount, Win Ratio, Record count
formulas: Win Ratio: WON:SUM/CLOSED:SUM
