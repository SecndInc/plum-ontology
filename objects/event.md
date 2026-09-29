# Event

Mirror table `sf_event_runs` · 13 records on snapshot 20260929T163700Z.

| Field | Type | Filled | Notes |
| --- | --- | --- | --- |
| Id | id | 100% | Activity ID |
| WhoId | reference | 69% | Name ID · → Contact, Lead |
| WhatId | reference | 85% | Related To ID · → Account, ApprovalSubmission, ApprovalSubmissionDetail, ApprovalWorkItem, Asset, AssetRelationship, Campaign, Case, ContactRequest, Contract, CreditMemo, DataQueryWorkspace, GoalAssignment, GoalDefinition, Image, Invoice, ListEmail, Location, Monthly_Revenue_Plan__c, OperatingHoursHoliday, Opportunity, Order, ProcessException, Product2, Quote, Solution, WorkOrder, WorkOrderLineItem |
| WhoCount | int | 100% | Relation Count · 0 … 1 |
| WhatCount | int | 100% | Related To Count · 0 … 1 |
| Subject | combobox | 100% | Universal Technologies Demo (1), Summit (Sample) (1), Meeting with Interac Corp (1), Meeting with Court Elliott (1), Lunch to discuss feedback from demo (Sample) (1), Email sent to Kevin and Blake (1), Email out to Court (1), Demo with Swathi (1), Demo with Jason (1), Demo - STRATIS Platform (1) |
| Location | string | 38% |  |
| IsAllDayEvent | boolean | 100% | All-Day Event · false (13) |
| ActivityDateTime | datetime | 92% | Due Date Time · 2025-02-01 19:00:00 … 2026-09-16 18:00:00 |
| ActivityDate | date | 92% | Due Date Only · 2025-02-01 … 2026-09-16 |
| DurationInMinutes | int | 100% | Duration · 0 … 180 |
| StartDateTime | datetime | 92% | Start Date Time · 2025-02-01 19:00:00 … 2026-09-16 18:00:00 |
| EndDateTime | datetime | 92% | End Date Time · 2025-02-01 20:00:00 … 2026-09-16 19:00:00 |
| EndDate | date | 92% | End Date · 2025-02-01 … 2026-09-16 |
| AccountId | reference | 69% | Account ID · → Account |
| OwnerId | reference | 100% | Assigned To ID · → Calendar, User |
| CurrencyIsoCode | picklist | 100% | Activity Currency · CAD (13) |
| IsPrivate | boolean | 100% | Private · false (13) |
| ShowAs | picklist | 100% | Show Time As · Busy (13) |
| IsDeleted | boolean | 100% | Deleted · false (13) |
| IsChild | boolean | 100% | Is Child · false (13) |
| IsGroupEvent | boolean | 100% | Is Group Event · false (13) |
| GroupEventType | picklist | 8% | Group Event Type · (blank) (12), 2 (1) |
| CreatedDate | datetime | 100% | Created Date · 2025-01-20 05:42:53 … 2026-09-10 20:42:46 |
| CreatedById | reference | 100% | Created By ID · → User |
| LastModifiedDate | datetime | 100% | Last Modified Date · 2025-01-20 05:42:53 … 2026-09-17 20:07:07 |
| LastModifiedById | reference | 100% | Last Modified By ID · → User |
| SystemModstamp | datetime | 100% | System Modstamp · 2025-01-20 05:42:53 … 2026-09-17 20:07:07 |
| IsArchived | boolean | 100% | Archived · false (11), true (2) |
| IsRecurrence | boolean | 100% | Create Recurring Series of Events · false (13) |
| IsReminderSet | boolean | 100% | Reminder Set · false (13) |
| EventSubtype | picklist | 100% | Event Subtype · Event (13) |
| IsRecurrence2Exclusion | boolean | 100% | Historical Event, Not Following Recurrence · false (13) |
| IsRecurrence2 | boolean | 100% | Repeat · false (13) |
| IsRecurrence2Exception | boolean | 100% | Is Exception · false (13) |

Never filled: Type, RecurrenceActivityId, RecurrenceStartDateTime, RecurrenceEndDateOnly, RecurrenceTimeZoneSidKey, RecurrenceType, RecurrenceInterval, RecurrenceDayOfWeekMask, RecurrenceDayOfMonth, RecurrenceInstance, RecurrenceMonthOfYear, ReminderDateTime, Recurrence2PatternVersion, Recurrence2PatternStartDate, Recurrence2PatternTimeZone.
