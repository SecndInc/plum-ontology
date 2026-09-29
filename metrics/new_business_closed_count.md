---
name: new_business_closed_count
version: 1
status: proposed
kind: base
owner: revops
description: New-business engagements (Business Type New or New - RFP) decided, won or lost, by close date.
source: {type: manual, ref: Business_Type__c picklist; win-rate.md}
confidence: medium
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: true}
  - {field: Business_Type__c, op: in, value: [New, New - RFP]}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: service_line, column: Type}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
topic: bd
format: number
aliases: ["new business decided", "new business closed"]
---

Denominator of [[new_business_win_rate]]. Same definition of new business as
[[new_business_won_count]]. FY2025: 11 decided (New 6, New - RFP 5; q34).

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 11
