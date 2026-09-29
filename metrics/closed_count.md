---
name: closed_count
version: 1
status: accepted
kind: base
owner: revops
description: Engagements (Master Opportunities) decided, won or lost, by close date.
source: {type: manual, ref: ontologies/push-media/salesforce/queries/win-rate.md}
confidence: high
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: true}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
topic: bd
format: number
aliases: ["decided deals", "closed deals", "decided engagements"]
---

Won plus lost engagements.
