# Reports: Public Reports

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Sample Report: Top Accounts [00OKc0000013SpwMAE]
folder Public Reports · type Opportunity · Summary · last run 2025-11-20
date: Opportunity.CloseDate THIS_AND_NEXT_FISCAL_YEAR (2026-01-01 to 2027-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name
aggregates: Sum of Amount

### Sample Report: # of Leads [00OKc0000013Sq9MAE]
folder Public Reports · type LeadList · Summary · last run 2025-11-20
date: Lead.CreatedDate CUSTOM
grouped by: Lead.CreatedDate (Month)
aggregates: Record count

### New Opportunities Report [00OJQ00000N7Rav2AF]
folder Public Reports · type Opportunity · Summary · last run 2025-11-20
date: Opportunity.CloseDate THIS_FISCAL_YEAR (2026-01-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.Account.Name, Opportunity.Amount
aggregates: Record count

### Opportunity Amount by Stage (Sample) [00OKc0000013SqLMAU]
folder Public Reports · type Opportunity · Summary · last run 2025-05-28
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName
aggregates: Sum of Amount, Record count

### Sample Report: Completed Activities [00OKc0000013SqIMAU]
folder Public Reports · type Activity · Matrix · last run 2015-10-22
date: Activity.ActivityDate LAST_N_DAYS:30 (2026-08-31 to 2026-09-29)
standard: closed=closed, type=te
grouped by: Activity.Owner.Name, Activity.Status
aggregates: Record count

### Sample Report: # of Accounts [00OKc0000013SqJMAU]
folder Public Reports · type AccountList · Matrix · last run 2015-10-22
date: Account.CreatedDate CUSTOM
grouped by: Account.CreatedDate (Month)
aggregates: Record count

### Sample Report: Users Logged In [00OKc0000013SqHMAU]
folder Public Reports · type User · Summary · last run 2015-10-22
date: Last Login LAST_N_DAYS:7 (2026-09-23 to 2026-09-29)
standard: active=active
grouped by: User.Username
aggregates: Sum of Active

### Sample Report: # of Reports [00OKc0000013Sq4MAE]
folder Public Reports · type ReportList · Summary · last run 2015-10-18
date: Report.CreatedDate CUSTOM
grouped by: Report.CreatedDate (Month)
aggregates: Record count

### Sample Report: # of Documents [00OKc0000013Sq3MAE]
folder Public Reports · type DocumentList · Summary · last run 2015-10-18
date: Document.CreatedDate CUSTOM
grouped by: Document.CreatedDate (Month)
aggregates: Record count

### Sample Report: # of Solutions [00OKc0000013Sq8MAE]
folder Public Reports · type SolutionList · Summary · last run 2015-10-18
date: Solution.CreatedDate CUSTOM
grouped by: Solution.CreatedDate (Month)
aggregates: Record count

### Sample Report: # of Cases [00OKc0000013Sq6MAE]
folder Public Reports · type CaseList · Summary · last run 2015-10-18
date: CREATED_DATEONLY CUSTOM
standard: units=h
grouped by: Case.CreatedDate (Month)
aggregates: Record count

### Sample Report: # of Contacts [00OKc0000013Sq7MAE]
folder Public Reports · type ContactList · Summary · last run 2015-10-18
date: Contact.CreatedDate CUSTOM
grouped by: Contact.CreatedDate (Month)
aggregates: Record count

### Sample Report: # of Tasks and Activities [00OKc0000013SqBMAU]
folder Public Reports · type Activity · Matrix · last run 2015-10-18
date: Activity.ActivityDate CUSTOM
standard: closed=all, type=te
grouped by: Activity.CreatedDate (Month)
aggregates: Record count

### Sample Report: Last Modified By [00OKc0000013SqCMAU]
folder Public Reports · type ReportList · Summary · last run 2015-10-18
date: Report.LastModifiedDate LAST_N_DAYS:30 (2026-08-31 to 2026-09-29)
grouped by: Report.LastModifiedBy.Name
aggregates: Record count

### Sample Report: Custom Reports by User [00OKc0000013SqEMAU]
folder Public Reports · type ReportList · Summary · last run 2015-10-18
date: Report.CreatedDate LAST_N_DAYS:30 (2026-08-31 to 2026-09-29)
grouped by: Report.CreatedBy.Name
aggregates: Record count

### Sample Report: # of Opportunities [00OKc0000013SqDMAU]
folder Public Reports · type Opportunity · Summary · last run 2015-10-18
date: Opportunity.CloseDate THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.CreatedDate (Month)
aggregates: Record count

### Sample Report: Login Wall of Shame [00OKc0000013Sq5MAE]
folder Public Reports · type User · Summary · last run 2015-10-18
filters: 1. User.IsActive equals "True"; 2. Last Login notEqual "LAST 7 DAYS"
date: Last Login LAST_N_DAYS:7 (2026-09-23 to 2026-09-29)
standard: active=active
grouped by: User.IsActive
aggregates: Sum of Active

### Sample Report: Active Users [00OKc0000013SqAMAU]
folder Public Reports · type User · Summary · last run 2015-10-18
date: Last Login CUSTOM
standard: active=active
grouped by: User.IsActive
aggregates: Record count

### Sample Report: # of Open Tasks [00OKc0000013SqFMAU]
folder Public Reports · type Activity · Matrix · last run 2015-10-18
date: Activity.ActivityDate CUSTOM
standard: closed=open, type=te
grouped by: Activity.Owner.Name, Activity.Status
aggregates: Record count

### Sample Report: Login Leaderboard [00OKc0000013SqGMAU]
folder Public Reports · type User · Summary · last run 2015-10-18
filters: 1. User.IsActive equals "True"
date: Last Login LAST_N_DAYS:7 (2026-09-23 to 2026-09-29)
standard: active=active
grouped by: User.Username
aggregates: Record count

### Sample Report: Cases Status by Rep [00OKc0000013SpxMAE]
folder Public Reports · type CaseList · Matrix · last run 2015-08-07
date: CREATED_DATEONLY THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: units=h
grouped by: Case.Owner.Name, Case.Status
aggregates: Record count

### Sample Reports: Leads by Status [00OKc0000013Sq0MAE]
folder Public Reports · type LeadList · Matrix · last run 2015-08-07
date: Lead.CreatedDate THIS_AND_NEXT_FISCAL_QUARTER (2026-07-01 to 2026-12-31)
grouped by: Lead.Status, Lead.CreatedDate (Month)
aggregates: Record count

### Sample Report: Month to Date Trending [00OKc0000013Sq1MAE]
folder Public Reports · type Opportunity · Matrix · last run 2015-08-07
date: Opportunity.CloseDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.CloseDate (DayInMonth), CLOSE_MONTH (Day)
aggregates: Sum of Amount

### Sample Report: Sales Leaderboard [00OKc0000013SpzMAE]
folder Public Reports · type Opportunity · Matrix · last run 2015-08-07
date: Opportunity.CloseDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Owner.Name
aggregates: Sum of Amount

### Sample Report: Pipeline History [00OKc0000013Sq2MAE]
folder Public Reports · type OpportunityTrend · Matrix · last run 2015-08-07
date: INTERVAL_DATE LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=all, probability=>0
grouped by: INTERVAL_DATE (Month), Opportunity.OpportunityHistory.StageName
aggregates: Sum of Historical Amount

### Sample Report: Leads by Lead Source [00OKc0000013SpvMAE]
folder Public Reports · type LeadList · Summary · last run 2015-08-07
date: CREATED_DATE THIS_AND_NEXT_FISCAL_QUARTER (2026-07-01 to 2026-12-31)
grouped by: Lead.LeadSource

### Sample Report: Open Deals [00OKc0000013SptMAE]
folder Public Reports · type Opportunity · Summary · last run 2015-08-07
date: Opportunity.CloseDate THIS_AND_NEXT_FISCAL_QUARTER (2026-07-01 to 2026-12-31)
standard: terr=all, open=open, probability=>0
grouped by: Opportunity.Name
aggregates: Sum of Amount

### Sample Report: Pipeline By Close Month [00OKc0000013SpuMAE]
folder Public Reports · type Opportunity · Matrix · last run 2015-08-07
date: Opportunity.CloseDate THIS_AND_NEXT_FISCAL_QUARTER (2026-07-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.CloseDate (Month), Opportunity.Type
aggregates: Sum of Amount

### Sample Report: Solutions Added [00OKc0000013SpyMAE]
folder Public Reports · type SolutionList · Matrix · last run 2015-08-07
date: Solution.CreatedDate CUSTOM (2006-06-22 to 2006-06-29)
grouped by: Solution.CreatedDate (Month), Solution.Status
aggregates: Record count

### Sample Report: Closed Sales [00OKc0000013SpqMAE]
folder Public Reports · type Opportunity · Matrix · last run 2015-08-07
date: Opportunity.CloseDate LAST_AND_THIS_FISCAL_QUARTER (2026-04-01 to 2026-09-30)
standard: terr=all, open=closedwon, probability=>0
grouped by: Opportunity.Account.Name, CLOSE_MONTH (Day)
aggregates: Sum of Amount

### Sample Report: Open Cases By Priority [00OKc0000013SpsMAE]
folder Public Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Open equals "True"
date: CREATED_DATEONLY THIS_FISCAL_QUARTER (2026-07-01 to 2026-09-30)
standard: units=h
grouped by: Case.Priority

### Sample Report: Sales Pipeline by Stage [00OKc0000013SprMAE]
folder Public Reports · type Opportunity · Matrix · last run 2015-08-07
date: Opportunity.CloseDate THIS_AND_NEXT_FISCAL_QUARTER (2026-07-01 to 2026-12-31)
standard: terr=all, open=all, probability=>0
grouped by: Opportunity.StageName, Opportunity.Type
aggregates: Sum of Amount
