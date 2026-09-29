---
name: tasks_completed
version: 1
status: proposed
kind: base
owner: revops
description: Sales tasks (calls, emails, LinkedIn touches, to-dos) marked completed, by due date, excluding Salesforce sample data.
source: {type: sf_report, ref: 00OKc0000013SqIMAU}
confidence: medium
last_verified: 2026-09-29
topic: activity
format: number
aliases: ["completed activities", "completed tasks", "tasks done", "activities completed"]
grain: task
source_table: Task
measure: {agg: count, column: Id}
base_filters:
  - {field: IsClosed, op: "=", value: true}
  - {field: CreatedById, op: "!=", value: 005Kc0000010gjJIAQ}
time_column: ActivityDate
time_semantics: fiscal
dimensions:
  - {key: task_type, column: TaskSubtype, label: Task type}
  - {key: owner_profile, column: Owner.ProfileId, label: Owner profile (role proxy)}
filters:
  - {key: task_type, column: TaskSubtype, type: picklist, allowed_values: [Task, Email, Call, LinkedIn]}
coverage_checks:
  - {name: no_due_date, sql_predicate: ActivityDate IS NULL, description: Completed task with no due date; outside any period}
  - {name: no_completed_timestamp, sql_predicate: CompletedDateTime IS NULL, description: Completed without a completion timestamp (older or archived tasks)}
  - {name: not_linked, sql_predicate: WhatId IS NULL, description: Not linked to an opportunity or account}
---

Counts Task rows with IsClosed = true (Status = Completed; the only closed status in use).
Dated by ActivityDate (due date), the same date the org's activity reports use
(Sample Report: Completed Activities, closed=closed). ActivityDate is date-only, so there is no time-zone shift.

Excludes the 11 Salesforce sample tasks created at org setup by user 005Kc0000010gjJIAQ.
Includes the completed "Follow-up after Presentation" tasks made by the flow Opportunity_AS_Follow_up_Task
(5, all due in 2025), because a completed follow-up is real work.
Events are not tasks and are counted in `meetings_held`.

Role: UserRoleId is never filled and Title is almost empty, so the owner dimension is the owner's profile id
(00eKc000000WLrmIAG Standard User, 00eKc000000u7IoIAI Client Service - Manager,
00eKc000000u7J3IAI Creative Services - Manager, 00eKc000000WLrlIAG System Administrator).
Never break this out by person.

FY2025 check: 8 completed non-sample tasks with a 2025 due date (3 Email, 5 flow follow-ups); see q60.

## Sweep
Drafted by the activity investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 8
