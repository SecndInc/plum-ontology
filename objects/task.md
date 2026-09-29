# Task

Mirror table `sf_task_runs` · 113 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Activity ID |
| WhoId | reference | 19% | Name ID · → Contact, Lead |
| WhatId | reference | 92% | Related To ID · → Account, ApprovalSubmission, ApprovalSubmissionDetail, ApprovalWorkItem, Asset, AssetRelationship, Campaign, Case, ContactRequest, Contract, CreditMemo, DataQueryWorkspace, GoalAssignment, GoalDefinition, Image, Invoice, ListEmail, Location, Monthly_Revenue_Plan__c, OperatingHoursHoliday, Opportunity, Order, ProcessException, Product2, Quote, Solution, WorkOrder, WorkOrderLineItem |
| WhoCount | int | 100% | Relation Count · 0 … 1 |
| WhatCount | int | 100% | Related To Count · 0 … 1 |
| Subject | combobox | 100% |  |
| ActivityDate | date | 69% | Due Date Only · 2025-01-04 … 2026-09-14 |
| Status | picklist | 100% | Open (93), Completed (20) |
| Priority | picklist | 100% | Normal (113) |
| IsHighPriority | boolean | 100% | High Priority · false (113) |
| OwnerId | reference | 100% | Assigned To ID · → Group, User |
| CurrencyIsoCode | picklist | 100% | Currency ISO Code · CAD (82), USD (31) |
| IsDeleted | boolean | 100% | Deleted · false (113) |
| AccountId | reference | 93% | Account ID · → Account |
| IsClosed | boolean | 100% | Closed · false (93), true (20) |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-09-14 18:29:24 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2026-09-14 18:29:24 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-01-20 05:42:53 … 2026-09-17 19:58:30 |
| IsArchived | boolean | 100% | Archived · false (101), true (12) |
| ReminderDateTime | datetime | 4% | Reminder Date/Time · 2025-05-15 15:00:00 … 2026-09-14 13:30:00 |
| IsReminderSet | boolean | 100% | Reminder Set · false (113) |
| IsRecurrence | boolean | 100% | Create Recurring Series of Tasks · false (113) |
| TaskSubtype | picklist | 100% | Task Subtype · Task (98), Email (12), Call (2), LinkedIn (1) |
| CompletedDateTime | datetime | 14% | Completed Date/Time · 2025-03-21 16:09:30 … 2026-09-01 15:08:54 |

Never filled: CallDurationInSeconds, CallType, CallDisposition, CallObject, RecurrenceActivityId, RecurrenceStartDateOnly, RecurrenceEndDateOnly, RecurrenceTimeZoneSidKey, RecurrenceType, RecurrenceInterval, RecurrenceDayOfWeekMask, RecurrenceDayOfMonth, RecurrenceInstance, RecurrenceMonthOfYear, RecurrenceRegeneratedType.

Bulk creation days: 2026-07-08 (31), 2025-05-13 (20).
