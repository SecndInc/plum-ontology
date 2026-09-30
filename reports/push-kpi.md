# Reports: PUSH KPI

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### BD - # of Opportunities this FY by type [00OJQ00000Nlid32AB]
folder PUSH KPI · type Opportunity · Summary · last run 2026-09-14
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, %
formulas: %: AMOUNT:SUM / PARENTGROUPVAL(AMOUNT:SUM, GRAND_SUMMARY)

### BD - # of Opportunities past FY [00OJQ00000NllSr2AJ]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate LAST_FISCAL_YEAR (2025-01-01 to 2025-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### BD - # of Won Opportunities this FY [00OJQ00000Nla7g2AB]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"; 2. Opportunity.StageName equals "Kick-off,Project In Progress,Project Completion"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### BD - # of Opportunities PFY by month [00OJQ00000Nlm3x2AB]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate LAST_FISCAL_YEAR (2025-01-01 to 2025-12-31)
standard: terr=all, open=all, probability=>0
grouped by: CDF1, Opportunity.Type
aggregates: Sum of Amount, Record count

### BD - # of Won Opportunities PFY [00OJQ00000NllxV2AR]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"; 2. Opportunity.StageName equals "Kick-off,Project In Progress,Project Completion"
date: Opportunity.CloseDate LAST_FISCAL_YEAR (2025-01-01 to 2025-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### BD - Opportunities by Lead FY [00OJQ00000NlrYH2AZ]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Owner.Name, Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### BD - FY Success Rate [00OJQ00000Nlphl2AB]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: BucketField_45479249
aggregates: Sum of Amount, Record count

### BD - # of Opportunities this FY - month [00OJQ00000NljMD2AZ]
folder PUSH KPI · type Opportunity · Summary · last run 2026-08-07
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: CDF1, Opportunity.Type
aggregates: Sum of Amount, Record count

### Forecast - Total [00OJQ00000NjNrI2AV]
folder PUSH KPI · type Opportunity · Summary · last run 2026-06-08
filters: 1. Opportunity.StageName equals "Discovery,Presentation,Proposal,Negotiation,Contract,Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount, Sum of Weighted Forecast, Record count

### PUSH Revenue - Forecast Amount [00OJQ00000Njk332AB]
folder PUSH KPI · type Opportunity · Summary · last run 2026-06-08
filters: 1. Opportunity.StageName equals "Discovery,Presentation,Proposal,Negotiation,Contract,Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of PUSH Revenue, Sum of Weighted Forecast, Record count

### PUSH Revenue - Total [00OJQ00000NjbSo2AJ]
folder PUSH KPI · type Opportunity · Summary · last run 2026-06-08
filters: 1. Opportunity.StageName equals "Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of PUSH Revenue, Sum of PUSH Revenue Percentage, Record count

### Gross Revenue - Total by Month [00OJQ00000NkHv32AF]
folder PUSH KPI · type Opportunity · Summary · last run 2026-06-08
filters: 1. Opportunity.StageName equals "Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: CLOSE_DATE CUSTOM
standard: terr=all, open=all, probability=>0
grouped by: CDF1, Opportunity.Type
aggregates: Sum of Amount, Record count

### PUSH Revenue - Total Monthy [00OJQ00000NkJnB2AV]
folder PUSH KPI · type Opportunity · Summary · last run 2026-06-08
filters: 1. Opportunity.StageName equals "Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=all, probability=>0
grouped by: CDF1, Opportunity.Type
aggregates: Sum of PUSH Revenue, Sum of PUSH Revenue Percentage, Record count

### Gross Revenue - Total [00OKc0000014f5WMAQ]
folder PUSH KPI · type Opportunity · Summary · last run 2026-06-08
filters: 1. Opportunity.StageName equals "Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### Dashboard - Revenue Budget Report [00OJQ00000Npqyc2AB]
folder PUSH KPI · type Revenue_Budget__c · Summary · last run 2025-12-19
filters: 1. Opportunity.RecordType equals "Master Opportunity"
date: Opportunity.CloseDate CUSTOM
grouped by: Opportunity.Campaign.Name, Opportunity.Campaign.ExpectedRevenue
aggregates: Sum of Amount, Sum of %
formulas: %: IF(
  Opportunity.Campaign.ExpectedRevenue:AVG = 0,
  NULL,
  Opportunity.Amount:SUM / Opportunity.Campaign.ExpectedRevenue:AVG
)

### Dashboard - Revenue Budget PUSH [00OJQ00000Npxf72AB]
folder PUSH KPI · type Revenue_Budget__c · Summary · last run 2025-12-19
filters: 1. Opportunity.RecordType equals "Sales Opportunity"; 2. Opportunity.IsWon equals "True"
date: Opportunity.CloseDate CUSTOM
grouped by: BucketField_27100391, Opportunity.CloseDate (FiscalQuarter), Opportunity.Campaign.Name
aggregates: Sum of Amount, Sum of PUSH Revenue, Average Primary Campaign Source: Expected Revenue in Campaign, Sum of %, %
formulas: %: IF(
  Opportunity.Campaign.ExpectedRevenue:AVG = 0,
  NULL,
  Opportunity.Amount:SUM / Opportunity.Campaign.ExpectedRevenue:AVG
)

### Dashboard - Revenue Budget [00OJQ00000Npum52AB]
folder PUSH KPI · type CampaignList · Summary · last run 2025-12-19
filters: 1. CAMPAIGN_TYPE equals "Sales"
grouped by: Campaign.Parent.Name
aggregates: Sum of Expected Revenue in Campaign, Sum of Value Won Opportunities in Campaign, Sum of %, %
formulas: %: IF(EXP_REVENUE:SUM = 0,
  NULL,
  AMOUNT_WON:SUM / EXP_REVENUE:SUM
)

### New Business – Opportunities [00OJQ00000NjSJ52AN]
folder PUSH KPI · type Opportunities_with_Activities__c · Summary · last run 2025-12-17
filters: 1. Opportunity.StageName equals "Discovery,Presentation,Proposal,Negotiation,Contract,Financial Setup"
date: Opportunity.CloseDate CUSTOM
grouped by: Opportunity.Type, Opportunity.Account.Name
aggregates: Sum of Amount, Record count

### BD - # of Opportunities this FY by Indus [00OJQ00000Nlp9t2AB]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-16
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Industry
aggregates: Sum of Amount, %
formulas: %: AMOUNT:SUM / PARENTGROUPVAL(AMOUNT:SUM, GRAND_SUMMARY)

### Gross Revenue - Sold Amount [00OKc0000014cxiMAA]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-15
filters: 1. Opportunity.StageName equals "Financial Setup,Kick-off,Project In Progress"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### Gross Revenue - Forecast Amount [00OKc0000014cxhMAA]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-15
filters: 1. Opportunity.StageName equals "Discovery,Presentation,Proposal,Negotiation,Contract"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### Gross Revenue - Closed Amount [00OKc0000014cxjMAA]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. Opportunity.StageName equals "Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Type
aggregates: Sum of Amount, Record count

### Opportunities Grouped by Parent [00OKc0000014cxmMAA]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. Opportunity.Parent_Opportunity__c notEqual ""; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Parent_Opportunity__c
aggregates: Sum of Amount, Record count

### PUSH Revenue - Media [00OKc0000014dTKMAY]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. TYPE equals "Media"; 2. Opportunity.StageName notEqual "Closed Lost"; 3. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name
aggregates: Sum of Amount, Sum of PUSH Revenue, Sum of PUSH Revenue Percentage, Sum of Total Media Spend, Sum of Commission Percent, Sum of Commission Amount, Record count

### Closed Opportunities by Business Type [00OKc0000014dZJMAY]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. STAGE_NAME equals "Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Business_Type__c
aggregates: Sum of Amount, Sum of PUSH Revenue, Record count

### Opportunities with Vendor Cost [00OKc0000014e3kMAA]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. Opportunity.StageName notEqual "Closed Lost"; 2. Opportunity.Vendor__c notEqual ""; 3. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Vendor__c
aggregates: Sum of Amount, Sum of Vendor Cost, Record count

### PUSH Revenue - Special Projects [00OKc0000014dXcMAI]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. TYPE equals "Special Project"; 2. Opportunity.StageName notEqual "Closed Lost"; 3. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name
aggregates: Sum of PUSH Revenue, Sum of PUSH Revenue Percentage, Sum of Vendor Cost, Record count

### PUSH Revenue - Creative [00OKc0000014dXXMAY]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. TYPE equals "Creative"; 2. Opportunity.StageName notEqual "Closed Lost"; 3. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate LAST_FISCAL_YEAR (2025-01-01 to 2025-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name
aggregates: Sum of PUSH Revenue, Sum of PUSH Revenue Percentage, Sum of Vendor Cost, Record count

### Lifetime Spend By Account [00OKc0000014dZEMAY]
folder PUSH KPI · type Opportunity · Summary · last run 2025-12-12
filters: 1. STAGE_NAME equals "Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate CUSTOM
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name
aggregates: Sum of Amount, Sum of PUSH Revenue, Record count

### Opportunites with Vendor Contacts [00OKc0000014fouMAA]
folder PUSH KPI · type OpportunityContact · Summary · last run 2025-12-12
filters: 1. STAGE_NAME equals "Financial Setup,Kick-off,Project In Progress,Project Completion"; 2. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, include=open
grouped by: Opportunity.OpportunityContactRole.Contact.LastName
aggregates: Sum of Amount, Sum of Vendor Cost, Record count
