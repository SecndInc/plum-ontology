---
name: open_pipeline_count
version: 1
status: proposed
kind: base
owner: revops
description: Number of open engagements (Master Opportunities not yet won or lost), by expected close date.
source: {type: manual, ref: "pipeline-and-forecast investigation; companion to open_pipeline_amount"}
confidence: high
last_verified: 2026-09-29
topic: pipeline
format: number
aliases: ["open deals", "open engagements", "deals in pipeline", "pipeline count"]
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: false}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: stage, column: StageName}
  - {key: forecast_category, column: ForecastCategoryName}
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
  - {key: owner_title, column: Owner.Title}
filters:
  - {key: stage, column: StageName, type: picklist, allowed_values: [Discovery, Creds Presentation, Proposal, Negotiation, Contract]}
  - {key: forecast_category, column: ForecastCategoryName, type: picklist, allowed_values: [Pipeline, Best Case, Commit]}
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
coverage_checks:
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: "Counted here, but contributes nothing to pipeline value"}
  - {name: close_date_before_snapshot, sql_predicate: "CloseDate < '2026-09-29'", description: "Open engagement whose expected close date was already past at the snapshot (stale)"}
---

Counts Master Opportunities with `IsClosed = false` by fiscal year of `CloseDate`. Same scope as `open_pipeline_amount`; engagements, never projects (child Sales Opportunities would double count, c94). At snapshot: 81 open engagements (Discovery 27, Creds Presentation 8, Proposal 23, Contract 23; c107). A few open engagements have close dates already in the past; the `close_date_before_snapshot` check flags them (the date literal is the snapshot date and must be moved forward with each snapshot).

## Sweep
Drafted by the pipeline investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 1
