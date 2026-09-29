---
name: clients_won
version: 1
status: proposed
kind: base
owner: revops
description: Number of distinct clients (accounts) with at least one engagement won, by close date.
source: {type: manual, ref: won_count definition}
confidence: medium
last_verified: 2026-09-29
grain: account
source_table: Opportunity
measure: {agg: count_distinct, column: AccountId}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsWon, op: "=", value: true}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
  - {key: operating_entity, column: Operating_Entity__c}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
coverage_checks:
  - {name: no_operating_entity, sql_predicate: Operating_Entity__c IS NULL, description: Won engagement not tagged to an operating entity (nearly all before FY2026)}
topic: bd
format: number
aliases: ["active clients", "clients won", "number of clients", "customers won"]
---

Client = the Account on the engagement (the client company, not PUSH's own operating entity).
Counted on engagements, which carry the win; projects share their engagement's account in 160 of
165 cases (q15). FY2025: 9 clients produced the 42 won engagements, one of them 13 (q45).

Caveats: distinct counts do not add across service lines or operating entities (one client can
appear in several). Parent accounts are not rolled up (ParentId is only 7% filled).


## Reviewer note
The aliases "active clients" and "number of clients" overstate what the metric measures. It counts accounts with an engagement won that fiscal year. A client still being served on an earlier year's win, or with only won projects, would be missed. Drop those aliases, or say that the metric counts clients won in the period, not active clients.

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 9
