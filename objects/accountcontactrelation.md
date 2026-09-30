# AccountContactRelation (Account Contact Relationship)

Mirror table `sf_account_contact_relation_runs` · 75 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Account Contact Relationship ID |
| AccountId | reference | 100% | Account ID · → Account |
| ContactId | reference | 100% | Contact ID · → Contact |
| IsDirect | boolean | 100% | Direct · true (74), false (1) |
| IsActive | boolean | 100% | Active · true (75) |
| CurrencyIsoCode | picklist | 100% | Account Contact Relationship Currency · CAD (52), USD (23) |
| IsDeleted | boolean | 100% | Deleted · false (75) |
| CreatedDate | datetime | 100% | Created Date · 2025-03-14 19:52:31 … 2026-09-17 20:07:06 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-03-14 19:52:31 … 2026-09-17 20:07:06 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-03-14 19:52:31 … 2026-09-17 20:07:06 |

Never filled: Roles, StartDate, EndDate, Relationship_Strength__c.

Bulk creation days: 2026-07-08 (18).
