---
name: new_business_won_count
version: 1
status: proposed
kind: base
owner: revops
description: New-business engagements (Business Type New or New - RFP) won, by close date.
source: {type: manual, ref: Business_Type__c picklist; win-rate.md}
confidence: medium
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsWon, op: "=", value: true}
  - {field: Business_Type__c, op: in, value: [New, New - RFP]}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: service_line, column: Type}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
topic: bd
format: number
aliases: ["new business wins", "new logos won", "new client wins"]
---

New business = Business_Type__c in (New, New - RFP). Organic Growth is treated as existing
business (growth within a current client) — see open question on Organic Growth.
Won = IsWon (Closed Won or any delivery stage), not the stage list used by the BD KPI reports,
which misses Closed Won (see [[won-definition]]). FY2025: 3 wins (New 3, New - RFP 0; q34).

Caveat: Business_Type__c is set by the rep; a few "New" engagements sit on accounts that had
already won business (q39).


## Reviewer note
The aliases "new logos won" and "new client wins" suggest a count of distinct new clients, but the metric counts won engagements, and one client can have several. q39 also shows some "New" engagements sit on accounts with earlier wins. Drop those aliases or add a distinct-account variant.

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 3
