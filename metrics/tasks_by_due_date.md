---
name: tasks_by_due_date
version: 1
status: proposed
kind: base
owner: revops
description: All sales tasks, open or completed, due in the period, excluding Salesforce sample data.
source: {type: sf_report, ref: 00OKc000001YCvMMAW}
confidence: medium
last_verified: 2026-09-29
topic: activity
format: number
aliases: ["tasks", "all tasks", "tasks due", "task volume"]
grain: task
source_table: Task
measure: {agg: count, column: Id}
base_filters:
  - {field: CreatedById, op: "!=", value: 005Kc0000010gjJIAQ}
time_column: ActivityDate
time_semantics: fiscal
dimensions:
  - {key: owner_profile, column: Owner.ProfileId, label: Owner profile (role proxy)}
coverage_checks:
  - {name: no_due_date, sql_predicate: ActivityDate IS NULL, description: "Task with no due date; outside any period (31 next-step tasks loaded 2026-07-08)"}
  - {name: still_open, sql_predicate: IsClosed = false, description: "Open (planned or overdue); not done"}
  - {name: not_linked, sql_predicate: WhatId IS NULL, description: "Not linked to an opportunity or account"}
---

Task side of the org's "all activities" reports (Sales Person All Activities, Activities by Salesperson:
closed=all, dated by ActivityDate / due date). Open and completed both count. For work actually done use `tasks_completed`.

Excludes the 11 sample tasks made at org setup by 005Kc0000010gjJIAQ.
Heavily inflated by the flow Opportunity_AS_Follow_up_Task: 56 of the 102 real tasks are automated "Follow-up after Presentation"
reminders, due the day they are created, and 51 of them are still open (q11, q40).
The only dimension is owner profile, so this can be added to `meetings_held` in `total_activities`.

## Sweep
Drafted by the activity investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 54
