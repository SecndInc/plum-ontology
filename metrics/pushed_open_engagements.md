---
name: pushed_open_engagements
version: 1
status: proposed
kind: base
owner: revops
description: Open engagements whose expected close date has been pushed into a later month at least once, by current close date.
source: {type: manual, ref: "pipeline-and-forecast investigation; PushCount checked against OpportunityHistory"}
confidence: medium
last_verified: 2026-09-29
topic: pipeline
format: number
aliases: ["pushed deals", "slipped deals", "slippage", "close date pushes"]
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: false}
  - {field: PushCount, op: ">", value: 0}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: stage, column: StageName}
  - {key: forecast_category, column: ForecastCategoryName}
  - {key: service_line, column: Type}
  - {key: owner_title, column: Owner.Title}
filters:
  - {key: stage, column: StageName, type: picklist, allowed_values: [Discovery, Creds Presentation, Proposal, Negotiation, Contract]}
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
---

**Definition.** Count of open Master Opportunities with `PushCount > 0`. Salesforce adds 1 to PushCount each time the close date moves into a later month. On open engagements PushCount (30) equals the month-crossing pushes rebuilt from OpportunityHistory (c111), so the field can be trusted. Pull-ins and moves within the same month are not counted.

**Reading it.** Slippage is recent and happened in batches: most pushes were in September 2026, and on 2026-09-21 alone 12 open engagements moved from 2026 to 2027 (c111). Bucketed by the current close date, pushed deals show up in the year they were pushed into (mostly FY2027). The count is 0 for FY2025 because no open engagement with a 2025 close date was pushed.

## Sweep
Drafted by the pipeline investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0
