# Monthly_Revenue_Plan__c (Monthly Revenue Plan)

Mirror table `sf_monthly_revenue_plan_runs` · 45 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Record ID |
| IsDeleted | boolean | 100% | Deleted · false (45) |
| Name | string | 100% | Monthly Revenue Plan |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (45) |
| CreatedDate | datetime | 100% | Created Date · 2026-04-27 02:45:33 … 2026-05-07 13:49:53 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2026-04-27 03:21:44 … 2026-05-07 13:49:53 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2026-04-27 03:21:44 … 2026-05-07 13:49:53 |
| Project__c | reference | 100% | Project · → Opportunity |
| Month__c | date | 100% | Month · 2026-01-01 … 2027-04-01 |
| Hard_Costs_Planned__c | currency | 82% | Hard Costs Planned · 1 … 1 |
| Markup_Planned__c | percent | 100% | Markup Planned · 1 … 21 |
| Markup_Actual__c | percent | 18% | Markup Actual · 21 … 21 |
| Media_Fees_Planned__c | currency | 100% | Media Fees Planned · 1 … 20100 |
| Media_Fees_Actual__c | currency | 16% | Media Fees Actual · 6700 … 20100 |
| Fees_Planned__c | currency | 100% | Fees Planned · 0.01 … 4221 · formula `Media_Fees_Planned__c * Markup_Planned__c` |
| Fees_Actual__c | currency | 100% | Fees Actual · 0 … 4221 · formula `Media_Fees_Actual__c * Markup_Actual__c` |
| Total_Planned__c | currency | 100% | Total Planned · 2.01 … 24321 · formula `Creative_Fees_Planned__c+ Fees_Planned__c + Hard_Costs_Planned__c + Media_Fees_Planned__c` |
| Total_Actual__c | currency | 100% | Total Actual · 0 … 24321 · formula `Creative_Fees_Actual__c + Fees_Actual__c + Hard_Costs_Actual__c + Media_Fees_Actual__c` |
| Variance__c | currency | 100% | Variance · -16214 … 0 · formula `Total_Actual__c - Total_Planned__c` |
| Notes__c | string | 18% | Notes |

Never filled: LastActivityDate, LastViewedDate, LastReferencedDate, Hard_Costs_Actual__c, Creative_Fees_Planned__c, Creative_Fees_Actual__c.
