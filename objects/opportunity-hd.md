# Opportunity__hd (Opportunity (Historical))

Mirror table `sf_opportunity_hd_runs` · 630 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Historical Data Table Id |
| ParentId | reference | 100% | Parent ID · → Opportunity |
| IsDeleted | boolean | 100% | Deleted · false (630) |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (552), USD (78) |
| ValidFromDate | datetime | 100% | Valid From · 2025-05-28 03:44:14 … 2026-09-29 13:39:22 |
| ValidToDate | datetime | 100% | Valid To · 2025-10-23 18:33:19 … 3000-01-01 00:00:00 |
| CreatedDate | datetime | 100% | Created Date · 2025-05-28 03:44:15 … 2026-09-29 13:39:22 |
| CreatedById | reference | 100% | Created By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-05-28 03:44:16 … 2026-09-29 13:39:22 |
| Amount__hpr | currency | 49% | Amount (Prior) · 0 … 27000000 |
| Amount__hst | currency | 94% | Amount (Historical) · 0 … 27000000 |
| CloseDate__hpr | date | 55% | Close Date (Prior) · 2024-09-25 … 2027-04-30 |
| CloseDate__hst | date | 100% | Close Date (Historical) · 2024-09-25 … 2027-12-30 |
| StageName__hpr | picklist | 55% | Stage (Prior) · (blank) (283), Project In Progress (148), Discovery (71), Proposal (47), Contract (33), Creds Presentation (14), Project Completion (12), Closed Won (10), Kick-off (8), Negotiation (2) |
| StageName__hst | picklist | 100% | Stage (Historical) · Project In Progress (134), Project Completion (121), Discovery (109), Proposal (93), Contract (56), Closed Won (51), Closed Lost (32), Creds Presentation (22), Kick-off (10), Negotiation (2) |
| Probability__hpr | percent | 55% | Probability (%) (Prior) · 0 … 100 |
| Probability__hst | percent | 100% | Probability (%) (Historical) · 0 … 100 |
| ForecastCategoryName__hpr | picklist | 55% | Forecast Category (Prior) · (blank) (283), Commit (157), Pipeline (92), Closed (50), Best Case (46), Omitted (2) |
| ForecastCategoryName__hst | picklist | 100% | Forecast Category (Historical) · Closed (243), Pipeline (136), Commit (125), Best Case (94), Omitted (32) |
| NextStep__hpr | string | 1% | Next Step (Prior) |
| NextStep__hst | string | 6% | Next Step (Historical) |

Bulk creation days: 2026-07-08 (76), 2025-12-17 (63), 2025-05-27 (60).
