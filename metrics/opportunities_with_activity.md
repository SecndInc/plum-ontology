---
name: opportunities_with_activity
version: 1
status: proposed
kind: base
owner: revops
description: Distinct opportunities with at least one sales task due in the period, excluding sample data.
source: {type: sf_report, ref: 00OKc0000013Sr0MAE}
confidence: low
last_verified: 2026-09-29
topic: activity
format: number
aliases: ["opportunities with activities", "deals touched", "opportunities worked"]
grain: opportunity
source_table: Task
measure: {agg: count_distinct, column: WhatId}
base_filters:
  - {field: WhatId, op: ">=", value: "006"}
  - {field: WhatId, op: "<", value: "007"}
  - {field: CreatedById, op: "!=", value: 005Kc0000010gjJIAQ}
time_column: ActivityDate
time_semantics: fiscal
dimensions:
  - {key: task_type, column: TaskSubtype, label: Task type}
coverage_checks:
  - {name: no_due_date, sql_predicate: ActivityDate IS NULL, description: Task with no due date (the 2026-07-08 next-step load); outside any period}
---

Counts distinct opportunities with at least one task due in the period.
Task.What is polymorphic and cannot be joined, so "related to an Opportunity" is the Opportunity key prefix 006
(WhatId from "006" up to, not including, "007").
It follows the org's "Opportunities with Activities" report type, which groups by TaskSubtype, so only tasks count (not events).

Caveats: the flow Opportunity_AS_Follow_up_Task makes a "Follow-up after Presentation" task, due the day it is created, on every
opportunity that reaches presentation, so in FY2025 most opportunities "have activity" only because of an automated reminder (q60).
Master and Sales opportunities both count; flow tasks sit on Master opportunities (q20).
The 31 next-step tasks loaded on 2026-07-08 have no due date and never fall in a period.


## Reviewer note
(1) The notes say the flow tasks sit on Master opportunities, but q20 shows 2 on Sales_Opportunity. (2) 'Only tasks count because the report groups by TaskSubtype' doesn't follow: the standard Opportunities with Activities report type covers events as well. Check the report's filters, or state the events exclusion as a choice. (3) In FY2025, 48 of the 49 opportunities have an automated reminder, and all of those reminders are on closed opportunities. The aliases 'deals touched' and 'opportunities worked' would mislead readers; drop them or qualify them.

## Sweep
Drafted by the activity investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 49
