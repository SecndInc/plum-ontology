---
name: lost_count
version: 1
status: proposed
kind: base
owner: revops
description: Engagements (Master Opportunities) lost, by close date.
source: {type: manual, ref: ontologies/push-media/salesforce/queries/win-rate.md}
confidence: high
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: true}
  - {field: IsWon, op: "=", value: false}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
  - {key: loss_reason, column: Loss_Reason__c}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
coverage_checks:
  - {name: no_loss_reason, sql_predicate: Loss_Reason__c IS NULL, description: Lost engagement with no loss reason recorded}
topic: bd
format: number
aliases: ["losses", "lost deals", "lost engagements", "deals lost"]
---

Lost = closed and not won (the only such stage in use is Closed Lost). Complements
[[won_count]]: won_count + lost_count = [[closed_count]]. FY2025: 10 lost of 52 decided (q9).

Caveat: losses are under-recorded relative to wins in the backfilled history. Most FY2025 wins were
loaded already won, while FY2025 losses mostly came from engagements that entered the pipeline open
(q32). A lost engagement often carries a very large bid Amount (the largest engagements in the
org are lost RFPs, q53), so never sum Amount on this set as "lost revenue" without reading that caveat.

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 10
