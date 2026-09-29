# Reports: Sales Engagement Dashboard Reports

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Users with Engagements by Day [00OKc0000013SqsMAE]
folder Sales Engagement Dashboard Reports · type Users_with_Daily_Metrics__c · Summary · last run 2023-09-18
date: User.ChatterAdoptionStageModifiedDate CUSTOM
grouped by: User.Name

### Contact Engagement by Account [00OKc0000013SqpMAE]
folder Sales Engagement Dashboard Reports · type Accounts_with_Contacts_with_Daily_Engagements__c · Summary · last run 2023-09-18
date: Account.CreatedDate CUSTOM
grouped by: Account.Name, Contact.Name

### Leads with Engagements by Day [00OKc0000013SqrMAE]
folder Sales Engagement Dashboard Reports · type Leads_with_Daily_Engagements__c · Summary · last run 2023-09-18
date: Lead.ConvertedDate CUSTOM
grouped by: Lead.Name

### Engagement by Sales Rep and Month [00OKc0000013SqqMAE]
folder Sales Engagement Dashboard Reports · type Users_with_Monthly_Engagements__c · Summary · last run 2023-09-18
date: User.ChatterAdoptionStageModifiedDate CUSTOM
grouped by: User.Name
aggregates: Record count

### Leads Converted by Sales Rep [00OKc0000013SqwMAE]
folder Sales Engagement Dashboard Reports · type Leads_and_Sales_Cadence_Trackers__c · Summary · last run 2023-09-18
filters: 1. Lead.IsConverted equals "True"; 2. Lead.ConvertedDate equals "LAST 30 DAYS"; 3. Lead.LastModifiedDate equals "LAST 30 DAYS"
date: Lead.ConvertedDate CUSTOM
grouped by: Lead.Id
aggregates: Sum of Converted

### Lead Conversions by Cadence [00OKc0000013SqxMAE]
folder Sales Engagement Dashboard Reports · type Leads_With_or_Without_Sales_Cadence_Trackers__c · Matrix · last run 2023-09-18
filters: 1. Lead.IsConverted equals "True"; 2. Lead.ConvertedDate equals "LAST 30 DAYS"
date: Lead.LastModifiedDate LAST_N_DAYS:30 (2026-08-31 to 2026-09-29)
aggregates: Sum of Converted, Record count

### Leads with Cadence Trackers [00OKc0000013SqyMAE]
folder Sales Engagement Dashboard Reports · type Leads_and_Sales_Cadence_Trackers__c · Summary · last run 2023-09-18
date: Lead.ConvertedDate CUSTOM
grouped by: Lead.Id

### Contacts with Cadence Trackers [00OKc0000013SqzMAE]
folder Sales Engagement Dashboard Reports · type Contacts_and_Sales_Cadence_Trackers__c · Summary · last run 2023-09-18
date: Contact.CreatedDate CUSTOM
grouped by: Contact.Id
