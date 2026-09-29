---
name: gross_revenue
version: 1
status: accepted
kind: base
owner: revops
description: What clients pay on won projects (Sales Opportunities), in CAD. Business definition of won (IsWon), so it does not reconcile against the stage-named KPI reports; checked against golden pins instead.
source: {type: manual, ref: ontologies/push-media/salesforce/queries/gross-revenue.md}
confidence: high
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: sum, column: Amount}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Sales_Opportunity}
  - {field: IsWon, op: "=", value: true}
time_column: CloseDate
time_semantics: fiscal
currency: {column: Amount, convert: true}
dimensions:
  - {key: service_line, column: Type}
  - {key: operating_entity, column: Operating_Entity__c}
  - {key: client, column: Account.Name}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
coverage_checks:
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: Won project with no amount; counted as zero}
topic: revenue
format: currency
aliases: ["revenue", "gross revenue", "billings", "bookings"]
---

Sum money on projects, never on engagements (see [[master-vs-sales-opportunities]]).
