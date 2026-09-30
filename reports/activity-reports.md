# Reports: Activity Reports

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Accounts with Activities [00OKc0000013Sr1MAE]
folder Activity Reports · type Accounts_with_Activities__c · Summary · last run 2026-07-08
date: Account.CreatedDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
grouped by: Account.Name, Activity.TaskSubtype
aggregates: Record count

### Opportunities with Activities this Month [00OKc0000013Sr0MAE]
folder Activity Reports · type Opportunities_with_Activities__c · Summary · last run 2026-07-08
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
grouped by: Activity.TaskSubtype, Opportunity.Name
aggregates: Sum of Amount, Record count

### Sales Rep Activities [00OKc0000013Sr3MAE]
folder Activity Reports · type User_Activities__c · Summary · last run 2026-07-08
date: Activity.ActivityDate THIS_MONTH (2026-09-01 to 2026-09-30)
grouped by: User.Name, Activity.TaskSubtype
aggregates: Record count
