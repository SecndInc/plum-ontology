---
name: avg_project_size
version: 2
status: accepted
kind: base
owner: revops
description: Average gross amount of won projects, in CAD.
source: {type: manual, ref: ontologies/push-media/salesforce/queries/deal-size-and-cycle.md}
confidence: medium
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: avg, column: Amount}
base_filters:
  - {field: RecordType.DeveloperName, op: in, value: [Sales_Opportunity]}
  - {field: IsWon, op: "=", value: true}
  - {field: StageName, op: not_in, value: [Closed Lost]}
time_column: CloseDate
time_semantics: fiscal
currency: {column: Amount, convert: true}
dimensions:
  - {key: owner_title, column: Owner.Title}
coverage_checks:
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: No amount; left out of the average}
  - {name: no_account, sql_predicate: AccountId IS NULL OR Account.Name IS NULL, description: Project without a client}
topic: revenue
format: currency
aliases: ["average project size", "average deal size", "deal size"]
---

Averages exclude projects with no amount.
