# PricebookEntry (Price Book Entry)

Mirror table `sf_pricebook_entry_runs` · 242 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Price Book Entry ID |
| Name | string | 100% | Product Name |
| Pricebook2Id | reference | 100% | Price Book ID · → Pricebook2 |
| Product2Id | reference | 100% | Product ID · → Product2 |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (242) |
| UnitPrice | currency | 100% | List Price · 0 … 0 |
| IsActive | boolean | 100% | Active · true (242) |
| UseStandardPrice | boolean | 100% | Use Standard Price · false (242) |
| CreatedDate | datetime | 100% | Created Date · 2025-04-03 14:08:03 … 2025-04-03 15:06:31 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-04-03 15:13:00 … 2025-04-03 15:13:00 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-04-03 15:13:00 … 2025-04-03 15:13:01 |
| IsDeleted | boolean | 100% | Deleted · false (242) |
| IsArchived | boolean | 100% | Archived · false (242) |

Never filled: ProductCode.
