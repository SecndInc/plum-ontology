# ForecastingFact (Forecasting Fact)

Mirror table `sf_forecasting_fact_runs` · 31 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Forecasting Fact ID |
| OwnerId | reference | 100% | Owner ID · → User |
| PeriodId | reference | 100% | Period ID · → Period |
| ForecastingCustomCategoryId | reference | 42% | Forecasting Custom Category ID · → ForecastingCustomCategory |
| ForecastCategoryName | picklist | 100% | Forecast Category · Closed (26), Commit (3), Pipeline (1), Best Case (1) |
| OpportunityId | reference | 100% | Opportunity ID · → Opportunity |
| ForecastingItemId | reference | 100% | Forecasting Item ID · → ForecastingItem |
| SystemModstamp | datetime | 100% | System Modstamp · 2026-02-10 08:06:43 … 2026-09-15 19:13:14 |
| ForecastingTypeId | reference | 100% | Forecasting Type ID · → ForecastingType |
| TargetValue | double | 100% | Target Value · 0 … 999958.18 |

Never filled: ForecastedObjectId, Territory2Id.
