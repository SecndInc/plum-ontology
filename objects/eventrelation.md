# EventRelation (Event Relation)

Mirror table `sf_event_relation_runs` · 20 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Event Relation ID |
| RelationId | reference | 100% | Relation ID · → Account, ApprovalSubmission, ApprovalSubmissionDetail, ApprovalWorkItem, Asset, AssetRelationship, Calendar, Campaign, Case, Contact, ContactRequest, Contract, CreditMemo, DataQueryWorkspace, GoalAssignment, GoalDefinition, Image, In_App_Checklist_Settings__c, Invoice, Lead, ListEmail, Location, Monthly_Revenue_Plan__c, OperatingHoursHoliday, Opportunity, Order, ProcessException, Product2, Quote, Solution, User, WorkOrder, WorkOrderLineItem |
| EventId | reference | 100% | Event ID · → Event |
| IsWhat | boolean | 100% | Is What · true (11), false (9) |
| IsParent | boolean | 100% | Is Parent · true (20) |
| IsInvitee | boolean | 100% | Is Invitee · false (19), true (1) |
| AccountId | reference | 80% | Account ID · → Account |
| Status | picklist | 5% | (blank) (19), New (1) |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-09-17 20:07:07 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2026-09-17 20:07:07 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-01-20 05:42:53 … 2026-09-17 20:07:07 |
| IsDeleted | boolean | 100% | Deleted · false (20) |

Never filled: RespondedDate, Response.
