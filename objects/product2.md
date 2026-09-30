# Product2 (Product)

Mirror table `sf_product2_runs` · 121 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Product ID |
| Name | string | 100% | Product Name |
| IsActive | boolean | 100% | Active · true (121) |
| CreatedDate | datetime | 100% | Created Date · 2025-04-02 15:19:37 … 2025-04-02 15:19:37 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-04-03 04:30:25 … 2025-04-03 04:36:35 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-04-03 15:13:00 … 2025-04-03 15:13:01 |
| Family | picklist | 100% | Product Family · SP (41), Creative (35), Media (25), Other (20) |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (121) |
| IsDeleted | boolean | 100% | Deleted · false (121) |
| IsArchived | boolean | 100% | Archived · false (121) |
| StockKeepingUnit | string | 100% | Product SKU |
| Product_Type__c | picklist | 100% | Product Type · Service (119), Non-inventory (2) |
| Sales_Tax_Code__c | picklist | 100% | Sales Tax Code · HST ON (121) |

Never filled: ProductCode, Description, ExternalDataSourceId, ExternalId, DisplayUrl, QuantityUnitOfMeasure, LastViewedDate, LastReferencedDate.
