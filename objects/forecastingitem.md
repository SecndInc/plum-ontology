# ForecastingItem (Forecasting Item)

Mirror table `sf_forecasting_item_runs` · 222 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Forecasting Item ID |
| OwnerId | reference | 100% | Owner ID · → User |
| PeriodId | reference | 100% | Period ID · → Period |
| ForecastingCustomCategoryId | reference | 15% | Forecasting Custom Category ID · → ForecastingCustomCategory |
| ForecastingItemCategory | picklist | 100% | Forecasting Item Category · BestCaseForecast (43), CommitForecast (42), CustomCategory (34), ClosedOnly (33), OpenPipeline (26), PipelineOnly (22), CommitOnly (17), BestCaseOnly (5) |
| ForecastCategoryName | picklist | 35% | Forecast Category · (blank) (145), Closed (33), Pipeline (22), Commit (17), Best Case (5) |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (222) |
| OwnerOnlyAmount | currency | 100% | Owner Only Amount · 0 … 1004958.18 |
| AmountWithoutAdjustments | currency | 100% | Amount Without Adjustments · 0 … 1004958.18 |
| AmountWithoutManagerAdjustment | currency | 100% | Amount Without Manager Adjustment · 0 … 1004958.18 |
| ForecastAmount | currency | 100% | Forecast Amount · 0 … 1004958.18 |
| AmountWithoutOwnerAdjustment | currency | 100% | Amount Without Owner Adjustments · 0 … 1004958.18 |
| IsQuantity | boolean | 100% | Is Quantity · false (222) |
| IsAmount | boolean | 100% | Is Amount · true (222) |
| HasAdjustment | boolean | 100% | Has Adjustment · false (222) |
| HasOwnerAdjustment | boolean | 100% | Has Owner Adjustment · false (222) |
| IsUpToDate | boolean | 100% | Is up to date · true (222) |
| SystemModstamp | datetime | 100% | System Modstamp · 2026-02-10 08:06:43 … 2026-09-29 13:39:22 |
| ForecastingTypeId | reference | 100% | Forecasting Type ID · → ForecastingType |
| SubordinateOverrides | int | 100% | Subordinate Overrides · 0 … 0 |

Never filled: ParentForecastingItemId, ProductFamily, ForecastingGroupItemId, OwnerOnlyQuantity, QuantityWithoutAdjustments, QuantityWithoutManagerAdjustment, ForecastQuantity, QuantityWithoutOwnerAdjustment, Territory2Id.
