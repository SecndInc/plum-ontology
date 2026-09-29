---
name: total_activities
version: 1
status: proposed
kind: derived
owner: revops
description: Tasks plus calendar events dated in the period (Salesforce "activities"), excluding sample data.
source: {type: sf_report, ref: 00OKc000001YCvMMAW}
confidence: medium
last_verified: 2026-09-29
topic: activity
format: number
aliases: ["activities", "activity count", "sales activity", "activity volume"]
formula: tasks_by_due_date + meetings_held
inputs: [tasks_by_due_date, meetings_held]
dimensions:
  - {key: owner_profile, column: Owner.ProfileId, label: Owner profile (role proxy)}
---

Follows the org's activity reports that count tasks and events together (type=te, closed=all, dated by ActivityDate).
Tasks are dated by due date and events by meeting date in the org time zone. There is no double counting: tasks and events are separate
objects, and relation rows only repeat the primary record they link to (q24).
Most of the task volume is automated presentation follow-up reminders (see `tasks_by_due_date`), so this counts reminders as well as work done.

## Sweep
Drafted by the activity investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 54
