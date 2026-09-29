# TaskRelation (Task Relation)

Mirror table `sf_task_relation_runs` · 125 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Task Relation ID |
| RelationId | reference | 100% | Relation ID · → Account, ApprovalSubmission, ApprovalSubmissionDetail, ApprovalWorkItem, Asset, AssetRelationship, Campaign, Case, Contact, ContactRequest, Contract, CreditMemo, DataQueryWorkspace, GoalAssignment, GoalDefinition, Image, In_App_Checklist_Settings__c, Invoice, Lead, ListEmail, Location, Monthly_Revenue_Plan__c, OperatingHoursHoliday, Opportunity, Order, ProcessException, Product2, Quote, Solution, WorkOrder, WorkOrderLineItem |
| TaskId | reference | 100% | Task ID · → Task |
| IsWhat | boolean | 100% | Is What · true (104), false (21) |
| AccountId | reference | 94% | Account ID · → Account |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-09-14 18:29:24 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2026-09-14 18:29:24 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-01-20 05:42:53 … 2026-09-14 18:29:24 |
| IsDeleted | boolean | 100% | Deleted · false (125) |

Bulk creation days: 2026-07-08 (31), 2025-05-13 (20).
