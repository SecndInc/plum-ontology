# OpportunityContactRole (Opportunity Contact Role)

Mirror table `sf_opportunity_contact_role_runs` · 94 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Contact Role ID |
| OpportunityId | reference | 100% | Opportunity ID · → Opportunity |
| ContactId | reference | 100% | Contact ID · → Contact |
| Role | picklist | 1% | (blank) (93), Influencer (1) |
| IsPrimary | boolean | 100% | Primary · false (59), true (35) |
| CreatedDate | datetime | 100% | Created Date · 2025-06-18 17:14:25 … 2026-09-17 20:07:07 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-06-18 17:14:25 … 2026-09-17 20:07:07 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-06-18 17:14:25 … 2026-09-17 20:07:07 |
| IsDeleted | boolean | 100% | Deleted · false (94) |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · USD (57), CAD (37) |

Bulk creation days: 2026-07-08 (50).
