---
name: accounts_with_activity
version: 1
status: proposed
kind: base
owner: revops
description: Distinct client accounts with at least one sales task due in the period, excluding sample data.
source: {type: sf_report, ref: 00OKc0000013Sr1MAE}
confidence: low
last_verified: 2026-09-29
topic: activity
format: number
aliases: ["accounts with activities", "accounts touched", "active accounts", "clients worked"]
grain: account
source_table: Task
measure: {agg: count_distinct, column: AccountId}
base_filters:
  - {field: CreatedById, op: "!=", value: 005Kc0000010gjJIAQ}
  - {field: AccountId, op: is_not_null}
time_column: ActivityDate
time_semantics: fiscal
dimensions:
  - {key: task_type, column: TaskSubtype, label: Task type}
coverage_checks:
  - {name: no_due_date, sql_predicate: ActivityDate IS NULL, description: "Task with no due date; outside any period"}
---

Task.AccountId is set by Salesforce from the task's related record (the opportunity's account, or the contact's account).
Every opportunity-linked task has the same account as its opportunity (q20).
The org's "Accounts with Activities" report groups by Account and TaskSubtype but dates by Account.CreatedDate, which
only answers "new accounts with activity". This metric dates by the task's due date instead, which answers "accounts worked in the period".
Only tasks count, not events, as in the report type. Flow-generated presentation follow-ups make up most of the 2025 volume.


## Reviewer note
15 of the 18 FY2025 accounts have only automated presentation reminders (q125: 3 have any other task). The aliases 'active accounts' and 'clients worked' would mislead; drop them or qualify them in the description. The source is given as report 00OKc0000013Sr1MAE, but the metric deliberately dates differently from that report (by task due date instead of Account.CreatedDate), so its numbers won't match the report. Mark it as a manual or derived definition, not a copy of the report.

## Sweep
Drafted by the activity investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 18
