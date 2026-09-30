# Campaign

Mirror table `sf_campaign_runs` · 25 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Campaign ID |
| IsDeleted | boolean | 100% | Deleted · false (25) |
| Name | string | 100% |  |
| ParentId | reference | 96% | Parent Campaign ID · → Campaign |
| Type | picklist | 100% | Sales (25) |
| Status | picklist | 100% | In Progress (22), Planned (3) |
| StartDate | date | 4% | Start Date · 2025-01-01 … 2025-01-01 |
| EndDate | date | 4% | End Date · 2025-12-31 … 2025-12-31 |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (25) |
| ExpectedRevenue | currency | 80% | Expected Revenue in Campaign · 5160 … 20016974.49 |
| ExpectedResponse | percent | 100% | Expected Response (%) · 0 … 0 |
| NumberSent | double | 100% | Num Sent in Campaign · 0 … 0 |
| IsActive | boolean | 100% | Active · true (25) |
| NumberOfLeads | int | 100% | Leads in Campaign · 0 … 0 |
| NumberOfConvertedLeads | int | 100% | Converted Leads in Campaign · 0 … 0 |
| NumberOfContacts | int | 100% | Contacts in Campaign · 0 … 0 |
| NumberOfResponses | int | 100% | Responses in Campaign · 0 … 0 |
| NumberOfOpportunities | int | 100% | Opportunities in Campaign · 0 … 16 |
| NumberOfWonOpportunities | int | 100% | Won Opportunities in Campaign · 0 … 10 |
| AmountAllOpportunities | currency | 100% | Value Opportunities in Campaign · 0 … 96620000 |
| AmountWonOpportunities | currency | 100% | Value Won Opportunities in Campaign · 0 … 5135748.55 |
| OwnerId | reference | 100% | Owner ID · → User |
| CreatedDate | datetime | 100% | Created Date · 2025-12-17 21:48:33 … 2025-12-19 00:50:03 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-12-19 00:48:01 … 2025-12-19 02:39:12 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2026-02-10 15:16:55 … 2026-09-29 13:36:20 |
| Net_Revenue__c | currency | 76% | Net Revenue · 2580 … 4201683.64 |

Never filled: BudgetedCost, ActualCost, Description, LastActivityDate, LastViewedDate, LastReferencedDate, CampaignMemberRecordTypeId.
