# OpportunityHistory (Opportunity History)

Mirror table `sf_opportunity_history_runs` · 732 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Opportunity History ID |
| OpportunityId | reference | 100% | Opportunity ID · → Opportunity |
| CreatedById | reference | 100% | Created By ID · → User |
| CreatedDate | datetime | 100% | Created Date · 2025-04-07 16:58:51 … 2026-09-29 13:39:22 |
| StageName | picklist | 100% | Stage Name · Project In Progress (205), Project Completion (135), Discovery (122), Proposal (95), Contract (61), Closed Won (51), Closed Lost (32), Creds Presentation (21), Kick-off (8), Negotiation (2) |
| Amount | currency | 93% | 0 … 27000000 |
| ExpectedRevenue | currency | 93% | Expected Revenue · 0 … 20250000 |
| CloseDate | date | 100% | Close Date · 2024-09-25 … 2027-12-30 |
| Probability | percent | 100% | 0 … 100 |
| ForecastCategory | picklist | 100% | To Forecast Category · Forecast (254), Closed (201), Pipeline (150), BestCase (95), Omitted (32) |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (654), USD (78) |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-04-07 16:59:36 … 2026-09-29 13:39:22 |
| IsDeleted | boolean | 100% | Deleted · false (732) |
| PrevAmount | currency | 45% | Previous Amount · 0 … 27000000 |
| PrevCloseDate | date | 51% | Previous Close Date · 2024-09-25 … 2027-04-30 |

Bulk creation days: 2025-05-27 (128), 2026-07-08 (76).
