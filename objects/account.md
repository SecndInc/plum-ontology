# Account

Mirror table `sf_account_runs` · 147 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Account ID |
| IsDeleted | boolean | 100% | Deleted · false (147) |
| Name | string | 100% | Account Name |
| Type | picklist | 41% | Account Type · (blank) (87), Customer (31), Prospect (21), Partner (8) |
| ParentId | reference | 7% | Parent Account ID · → Account |
| BillingStreet | textarea | 18% | Billing Street |
| BillingCity | string | 18% | Billing City |
| BillingState | string | 18% | Billing State/Province |
| BillingPostalCode | string | 18% | Billing Zip/Postal Code |
| BillingCountry | string | 46% | Billing Country |
| Website | url | 18% |  |
| PhotoUrl | url | 100% | Photo URL |
| Industry | picklist | 24% | (blank) (112), Banking (6), Retail (5), Technology (4), Other (3), Media (3), Food & Beverage (3), Telecommunications (2), Insurance (2), Finance (2) |
| NumberOfEmployees | int | 9% | Employees · 10 … 20000 |
| Description | textarea | 16% | Account Description |
| CurrencyIsoCode | picklist | 100% | Account Currency · CAD (118), USD (29) |
| OwnerId | reference | 100% | Owner ID · → User |
| CreatedDate | datetime | 100% | Created Date · 2025-03-14 19:46:15 … 2026-09-21 14:23:31 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-03-14 19:47:30 … 2026-09-21 14:23:31 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-03-19 04:02:16 … 2026-09-21 14:23:31 |
| LastActivityDate | date | 9% | Last Activity · 2025-01-10 … 2026-09-16 |
| IsCustomerPortal | boolean | 100% | Customer Portal Account · false (147) |
| AccountSource | picklist | 14% | Account Source · (blank) (126), Referral - Team (11), Referral - Partner (5), Website (4), Advertisement (1) |
| IsPriorityRecord | boolean | 100% | Important · false (147) |
| Quickbooks_Code__c | double | 18% | Quickbooks Code · 21 … 1712 |
| Decision_Maker__c | reference | 1% | Decision Maker · → Contact |

Never filled: MasterRecordId, BillingLatitude, BillingLongitude, BillingGeocodeAccuracy, ShippingStreet, ShippingCity, ShippingState, ShippingPostalCode, ShippingCountry, ShippingLatitude, ShippingLongitude, ShippingGeocodeAccuracy, LastViewedDate, LastReferencedDate, Jigsaw, JigsawCompanyId, SicDesc.

Bulk creation days: 2026-07-08 (46), 2025-03-19 (27).
