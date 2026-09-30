# OpportunityFieldHistory (Opportunity Field History)

Mirror table `sf_opportunity_field_history_runs` · 908 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Opportunity History ID |
| IsDeleted | boolean | 100% | Deleted · false (908) |
| OpportunityId | reference | 100% | Opportunity ID · → Opportunity |
| CreatedById | reference | 100% | Created By ID · → User |
| CreatedDate | datetime | 100% | Created Date · 2025-04-07 16:58:51 … 2026-09-29 13:39:22 |
| Field | picklist | 100% | Changed Field · created (324), Amount (211), StageName (141), Media_Spend_1stMo__c (68), Media_Spend_2ndMo__c (43), opportunityCreatedFromLead (35), Media_Spend_3rdMo__c (29), Proposal_Date__c (17), Media_Spend_4thMo__c (14), Media_Spend_5thMo__c (9) |
| DataType | picklist | 100% | Datatype · Currency (390), Text (360), DynamicEnum (141), DateOnly (17) |
| OldValue | anyType | 54% | Old Value |
| NewValue | anyType | 60% | New Value |

Bulk creation days: 2025-05-27 (128), 2026-07-08 (76), 2026-01-09 (75).
