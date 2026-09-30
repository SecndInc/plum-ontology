---
name: open_engagements
version: 1
status: proposed
kind: base
owner: revops
description: Engagements (Master Opportunities) still being pursued (not yet won or lost), by expected close date.
source: {type: manual, ref: OpportunityStage IsClosed}
confidence: medium
last_verified: 2026-09-29
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
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
  - {key: operating_entity, column: Operating_Entity__c}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
coverage_checks:
  - {name: zero_probability_open, sql_predicate: Probability = 0, description: Open engagement at 0% probability (placeholder records with no amount)}
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: Open engagement with no amount}
topic: bd
format: number
aliases: ["open pipeline", "open engagements", "active pursuits", "pipeline count"]
---

Open = IsClosed false: stages Discovery, Creds Presentation, Proposal, Contract (Negotiation is
defined but unused). Snapshot: 47 open engagements dated FY2026 and 33 dated FY2027 (q9). A
past-dated open engagement (one in FY2025) is stale, not pipeline.

Caveat: three open FY2026 Proposal engagements sit at 0% probability with Amount 0 (q53); they are
kept in the count but flagged.

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 1
