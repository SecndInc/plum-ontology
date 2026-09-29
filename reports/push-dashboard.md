# Reports: PUSH Dashboard

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Spend by Account [00OJQ00000N7Lgo2AF]
folder PUSH Dashboard · type Opportunity · Summary · last run 2025-12-03
filters: 1. ACCOUNT_TYPE equals "Customer"
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name, Opportunity.Name
aggregates: Sum of Amount, Record count

### Parent Opp with Sum of Child Media Spend [00OKc0000014qVgMAI]
folder PUSH Dashboard · type Opportunity · Summary · last run 2025-08-18
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Sum of Media Spend, Record count

### Parent Opp with Sum of Child Estimates [00OKc0000014qVbMAI]
folder PUSH Dashboard · type Opportunity · Summary · last run 2025-08-18
filters: 1. RECORDTYPE equals "Master Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Sum of Fees, Record count

### Media Spend/Estimate/Amount by Parent [00OKc0000014qVWMAY]
folder PUSH Dashboard · type Opportunity · Summary · last run 2025-06-17
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Parent_Opportunity__c
aggregates: Sum of Amount, Sum of Fees Amount, Sum of Total Media Spend, Record count

### Child Estimate Amount to Media Spend [00OKc0000014qVlMAI]
folder PUSH Dashboard · type Opportunity · Summary · last run 2025-05-28
filters: 1. RECORDTYPE equals "Sales Opportunity"
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Fees Amount, Sum of Total Media Spend, Record count
