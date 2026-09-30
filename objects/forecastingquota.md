# ForecastingQuota (Forecasting Quota)

Mirror table `sf_forecasting_quota_runs` · 6 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | ForecastingQuota ID |
| PeriodId | reference | 100% | Period ID · → Period |
| StartDate | date | 100% | Quota Month · 2023-09-01 … 2024-02-01 |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (6) |
| QuotaAmount | currency | 100% | Quota Amount · 30000 … 50000 |
| QuotaQuantity | double | 100% | Quota Quantity · 0 … 0 |
| QuotaOwnerId | reference | 100% | Owner ID · → User |
| IsQuantity | boolean | 100% | Is Quantity · false (6) |
| IsAmount | boolean | 100% | Is Amount · true (6) |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2025-01-20 05:42:53 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2025-01-20 05:42:53 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-01-20 05:42:53 … 2025-01-20 05:42:53 |
| ForecastingTypeId | reference | 100% | Forecasting Type ID · → ForecastingType |

Never filled: ProductFamily, ForecastingGroupItemId, Territory2Id.
