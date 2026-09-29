---
name: open_pipeline_amount_p25
version: 1
status: proposed
kind: base
owner: revops
description: Open engagement pipeline (CAD) on deals whose probability is 25%; building block of weighted pipeline.
source: {type: manual, ref: "pipeline-and-forecast investigation; input to weighted_pipeline_amount"}
confidence: medium
last_verified: 2026-09-29
topic: pipeline
format: currency
aliases: ["pipeline at 25%"]
grain: opportunity
source_table: Opportunity
measure: {agg: sum, column: Amount}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: false}
  - {field: Probability, op: "=", value: 25}
time_column: CloseDate
time_semantics: fiscal
currency: {column: Amount, convert: true}
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
---
Same scope as `open_pipeline_amount`, restricted to `Probability = 25`. Input to `weighted_pipeline_amount`.

## Sweep
Drafted by the pipeline investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0
