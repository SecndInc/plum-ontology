# OpportunityStage (Opportunity Stage)

Mirror table `sf_opportunity_stage_runs` · 18 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Opportunity Stage ID |
| MasterLabel | string | 100% | Master Label |
| ApiName | string | 100% | API Name |
| IsActive | boolean | 100% | Is Active · true (12), false (6) |
| SortOrder | int | 67% | Sort Order · 1 … 12 |
| IsClosed | boolean | 100% | Closed · false (12), true (6) |
| IsWon | boolean | 100% | Won · false (13), true (5) |
| ForecastCategory | picklist | 100% | Forecast Category · Pipeline (9), Closed (5), Forecast (2), Omitted (1), BestCase (1) |
| ForecastCategoryName | picklist | 100% | Forecast Category Name · Pipeline (9), Closed (5), Commit (2), Omitted (1), Best Case (1) |
| DefaultProbability | percent | 100% | Probability (%) · 0 … 100 |
| Description | string | 33% |  |
| CreatedById | reference | 100% | Created By ID · → User |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-08-24 16:53:02 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-03-24 14:05:54 … 2026-09-17 18:23:38 |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-03-24 14:05:54 … 2026-09-17 18:23:38 |
