# Reports: Sales & Marketing Dashboards Reports

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Pipeline Report This Q [00OKc0000013SqNMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
filters: 1. WON equals "True"; 2. CLOSED equals "False" · logic 1 OR 2
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount, Record count

### Closed Won This Q by Type [00OKc0000013SqOMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Type, Opportunity.Fiscal, Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### Closed Lost by Reason [00OKc0000013SqQMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
filters: 1. WON equals "False"
date: Opportunity.CloseDate THIS_AND_LAST_FISCAL_YEAR:2 (2025-01-01 to 2026-12-31)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Fiscal, Opportunity.Loss_Reason__c
aggregates: Sum of Amount, Record count

### Open Oppties This Q [00OKc0000013SqTMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Account.Name, Opportunity.Type
aggregates: Sum of Amount, Record count

### Open Oppties This Q - No Acti Last 96hrs [00OKc0000013SqRMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
filters: 1. LAST_ACTIVITY greaterThan "LAST 4 DAYS"
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Account.Name, Opportunity.Type, Opportunity.Probability
aggregates: Sum of Amount, Record count

### Closed Won This Q by Owner [00OKc0000013SqSMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Fiscal, Opportunity.Owner.Name, Opportunity.LeadSource
aggregates: Sum of Amount, Record count

### Closed Won + ≥80% This Q by Owner [00OKc0000013SqPMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=gt70
grouped by: Opportunity.Owner.Name, Opportunity.IsWon, Opportunity.LeadSource
aggregates: Sum of Amount, Record count

### Win Ratio [00OKc0000013SqUMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=closed, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.StageName
aggregates: Sum of Amount, Win Ratio, Record count
formulas: Win Ratio: WON:SUM/CLOSED:SUM

### Closed Won by Type [00OKc0000013SqVMAU]
folder Sales & Marketing Dashboards Reports · type Opportunity · Summary · last run 2025-05-21
date: Opportunity.CloseDate THIS_AND_LAST_FISCAL_YEAR:2 (2025-01-01 to 2026-12-31)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Fiscal, Opportunity.Type, Opportunity.Account.Name
aggregates: Sum of Amount, Average Amount, Record count

### Leads Created Current FQ [00OKc0000013SqYMAU]
folder Sales & Marketing Dashboards Reports · type LeadList · Summary · last run 2025-05-21
date: CREATED_DATE THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
grouped by: Lead.LeadSource
aggregates: Record count

### Leads Converted All Time [00OKc0000013SqWMAU]
folder Sales & Marketing Dashboards Reports · type OpportunityLead · Summary · last run 2025-05-21
date: Converted Date CUSTOM
grouped by: Lead.LeadSource, Lead.Status
aggregates: Sum of Opportunity Amount, Record count

### Leads Converted by FQ [00OKc0000013SqXMAU]
folder Sales & Marketing Dashboards Reports · type OpportunityLead · Summary · last run 2025-05-21
date: CONVERTED_DATE THIS_AND_LAST_FISCAL_YEAR:2 (2025-01-01 to 2026-12-31)
grouped by: CONVERTED_DATE (FiscalQuarter), Lead.LeadSource, Lead.Status
aggregates: Sum of Opportunity Amount, Record count

### Hot Leads w/o Activity >96 Hours [00OKc0000013SqbMAE]
folder Sales & Marketing Dashboards Reports · type LeadList · Summary · last run 2025-05-21
filters: 1. LAST_ACTIVITY greaterThan "LAST 4 DAYS"; 2. Lead.Rating equals "Hot"
date: CREATED_DATE CUSTOM
grouped by: Lead.Owner.Name
aggregates: Record count

### Leads Converted Current FQ [00OKc0000013SqZMAU]
folder Sales & Marketing Dashboards Reports · type OpportunityLead · Summary · last run 2025-05-21
date: Converted Date THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
grouped by: Lead.Owner.Name, Lead.LeadSource, Lead.Status
aggregates: Sum of Opportunity Amount, Record count

### Conversion Rate [00OKc0000013SqaMAE]
folder Sales & Marketing Dashboards Reports · type OpportunityLead · Summary · last run 2015-08-04
date: Lead.CreatedDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
grouped by: Lead.CreatedDate (Month)
aggregates: Sum of Opportunity Amount, Conversion Rate, Record count
formulas: Conversion Rate: CONVERTED:SUM / RowCount
