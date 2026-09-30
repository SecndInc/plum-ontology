# Opportunity

Mirror table `sf_opportunity_runs` · 359 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Opportunity ID |
| IsDeleted | boolean | 100% | Deleted · false (359) |
| AccountId | reference | 100% | Account ID · → Account |
| RecordTypeId | reference | 100% | Record Type ID · → RecordType · 012Kc000000xd9cIAA (197), 012Kc000000xcSYIAY (162) |
| Name | string | 100% |  |
| Description | textarea | 39% |  |
| StageName | picklist | 100% | Stage · Project Completion (116), Proposal (48), Discovery (44), Project In Progress (43), Closed Won (41), Closed Lost (30), Contract (27), Creds Presentation (8), Kick-off (2) |
| Amount | currency | 98% | 0 … 27000000 |
| Probability | percent | 100% | Probability (%) · 0 … 100 |
| CloseDate | date | 100% | Close Date · 2024-09-25 … 2027-12-30 |
| Type | picklist | 99% | Opportunity Type · Media (167), Creative (111), Agency (79), (blank) (2) |
| NextStep | string | 9% | Next Step |
| LeadSource | picklist | 6% | Lead Source · (blank) (338), Referral - Team (10), Referral - Partner (6), Website (4), Advertisement (1) |
| IsClosed | boolean | 100% | Closed · true (232), false (127) |
| IsWon | boolean | 100% | Won · true (202), false (157) |
| ForecastCategory | picklist | 100% | Forecast Category · Closed (202), Pipeline (52), BestCase (49), Omitted (30), Forecast (26) |
| ForecastCategoryName | picklist | 100% | Forecast Category · Closed (202), Pipeline (52), Best Case (49), Omitted (30), Commit (26) |
| CurrencyIsoCode | picklist | 100% | Opportunity Currency · CAD (303), USD (56) |
| CampaignId | reference | 15% | Campaign ID · → Campaign |
| HasOpportunityLineItem | boolean | 100% | Has Line Item · false (359) |
| OwnerId | reference | 100% | Owner ID · → User |
| IsExcludedFromTerritory2Filter | boolean | 100% | Exclude from the territory assignment filter logic · false (359) |
| CreatedDate | datetime | 100% | Created Date · 2025-04-07 16:58:51 … 2026-09-21 14:24:44 |
| AgeInDays | int | 100% | Age · 8 … 539 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-05-28 03:44:14 … 2026-09-29 13:39:22 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-06-23 19:53:05 … 2026-09-29 13:39:22 |
| LastActivityDate | date | 4% | Last Activity · 2025-01-10 … 2026-09-16 |
| LastActivityInDays | int | 4% | Recent Activity · 13 … 627 |
| PushCount | int | 100% | Push Count · 0 … 2 |
| LastStageChangeDate | datetime | 30% | Last Stage Change Date · 2025-04-07 16:59:36 … 2026-09-29 13:39:22 |
| LastStageChangeInDays | int | 100% | Days In Stage · 0 … 539 |
| FiscalQuarter | int | 100% | Fiscal Quarter · 1 … 4 |
| FiscalYear | int | 100% | Fiscal Year · 2024 … 2027 |
| Fiscal | string | 100% | Fiscal Period |
| ContactId | reference | 10% | Contact ID · → Contact |
| HasOpenActivity | boolean | 100% | Has Open Activity · false (274), true (85) |
| HasOverdueTask | boolean | 100% | Has Overdue Task · false (305), true (54) |
| LastAmountChangedHistoryId | reference | 34% | Opportunity History ID · → OpportunityHistory |
| LastCloseDateChangedHistoryId | reference | 17% | Opportunity History ID · → OpportunityHistory |
| IsPriorityRecord | boolean | 100% | Important · false (359) |
| Budget_Confirmed__c | boolean | 100% | Budget Confirmed · false (359) |
| Discovery_Completed__c | boolean | 100% | Discovery Completed · false (359) |
| ROI_Analysis_Completed__c | boolean | 100% | ROI Analysis Completed · false (359) |
| Loss_Reason_Explained__c | textarea | 8% | Loss Reason Explained |
| Loss_Reason__c | picklist | 9% | Loss Reason · (blank) (327), Other (17), Lost to Competitor (7), No Decision / Non-Responsive (4), No Budget / Lost Funding (3), Price (1) |
| Next_Step_Date__c | date | 1% | Next Step Date · 2025-07-21 … 2025-08-20 |
| Decision_Maker__c | reference | 23% | Decision Maker · → Contact |
| Questions_Sent__c | boolean | 100% | Questions Sent? · false (305), true (54) |
| Parent_Opportunity__c | reference | 48% | Parent Opportunity · → Opportunity |
| Questions_Reviewed__c | boolean | 100% | Questions Reviewed? · false (305), true (54) |
| Billing_Method__c | picklist | 2% | Billing Method · (blank) (352), Media - Planned (4), Media - Actuals (2), Project (1) |
| MSA_Sent__c | boolean | 100% | MSA Sent? · false (353), true (6) |
| SOW_Sent__c | boolean | 100% | SOW Sent? · false (353), true (6) |
| Estimate_Sent__c | boolean | 100% | Estimate Sent? · false (355), true (4) |
| Business_Type__c | picklist | 99% | Business Type · Exisiting (236), New (101), Organic Growth (11), New - RFP (9), (blank) (2) |
| Proposal_Date__c | date | 15% | Proposal Date · 2024-12-31 … 2026-08-21 |
| Project_ID__c | double | 12% | Project ID · 1230 … 1410 |
| Media_Spend_1stMo__c | currency | 100% | Media Spend-1stMo · 0 … 958774.08 |
| Media_Spend_2ndMo__c | currency | 100% | Media Spend-2ndMo · 0 … 947172.83 |
| Media_Spend_3rdMo__c | currency | 99% | Media Spend-3rdMo · 0 … 1015326.17 |
| Media_Spend_4thMo__c | currency | 100% | Media Spend-4thMo · 0 … 223410.03 |
| Media_Spend_5thMo__c | currency | 100% | Media Spend-5thMo · 0 … 204347.85 |
| Media_Spend_6thMo__c | currency | 100% | Media Spend-6thMo · 0 … 148300.56 |
| Media_Spend_7thMo__c | currency | 100% | Media Spend-7thMo · 0 … 14054.4 |
| Media_Spend_8thMo__c | currency | 100% | Media Spend-8thMo · 0 … 19976.32 |
| Media_Spend_9thMo__c | currency | 100% | Media Spend-9thMo · 0 … 18466.25 |
| Media_Spend_10thMo__c | currency | 100% | Media Spend-10thMo · 0 … 0 |
| Media_Spend_11thMo__c | currency | 100% | Media Spend-11thMo · 0 … 0 |
| Media_Spend_12thMo__c | currency | 100% | Media Spend-12thMo · 0 … 0 |
| Total_Media_Spend__c | currency | 100% | Total Media Spend · 0 … 2921273.08 · formula `Media_Spend_1stMo__c + Media_Spend_2ndMo__c + Media_Spend_3rdMo__c + Media_Spend_4thMo__c + Media_Spend_5thMo__c + Media_Spend_6thMo__c + Media_Spend_7thMo__c +` |
| Commission_Amount__c | currency | 100% | Commission Amount · 0 … 0 · formula `If( Commission_Percent__c > 0,Amount * Commission_Percent__c, Commission_Lump_Amount__c )` |
| Sum_of_Sales_Opportunities__c | currency | 12% | Sum of Sales Opportunities · 1720 … 3500000 |
| Vendor_Cost__c | currency | 5% | Vendor Cost · 0 … 30836 |
| PUSH_Revenue__c | currency | 100% | PUSH Revenue · 0 … 9848550 · formula `IF( ISPICKVAL(Type, "Media"), (Total_Media_Spend__c * Media_Fee__c), (Amount - Vendor_Cost__c) )` |
| PUSH_Revenue_Percentage__c | percent | 94% | PUSH Revenue Percentage · 0 … 100 · formula `(PUSH_Revenue__c / Amount)` |
| Media_Fee__c | percent | 11% | Media Fee % · 0 … 20 |
| Spent_Amount__c | currency | 100% | Spent Amount · 0 … 9848550 · formula `Total_Media_Spend__c + PUSH_Revenue__c` |
| Approved__c | boolean | 100% | Approved · false (359) |
| Fees_Amount__c | currency | 57% | Fees Amount · 0 … 3480000 |
| Sum_of_Fees__c | currency | 12% | Sum of Fees · 0 … 3480000 |
| Sum_of_Media_Spend__c | currency | 12% | Sum of Media Spend · 0 … 3401272.08 |
| Operating_Entity__c | picklist | 50% | Operating Entity · (blank) (181), Push USA (97), Stratis (45), Push Canada (36) |
| Operating_Entity_Logo__c | string | 50% | Operating Entity Logo · formula `CASE(Operating_Entity__c, "Push Canada", IMAGE("/resource/Logo_PushCanada", "Push Canada"), "Push USA", IMAGE("/resource/Logo_PushUSA", "Push USA"), "Stratis", ` |

Never filled: Pricebook2Id, Territory2Id, LastViewedDate, LastReferencedDate, SyncedQuoteId, ContractId, Proposal_Hours__c, Commission_Percent__c, Commission_Lump_Amount__c, Vendor__c, Teamwork_ID__c.

Bulk creation days: 2026-07-08 (76).
