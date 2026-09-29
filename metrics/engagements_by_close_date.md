---
name: engagements_by_close_date
version: 1
status: proposed
kind: base
owner: revops
description: All engagements (Master Opportunities), open, won or lost, counted by their close date — the BD "# of Opportunities" KPI.
source: {type: sf_report, ref: 00OJQ00000NllSr2AJ}
confidence: high
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: count, column: Id}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
time_column: CloseDate
time_semantics: fiscal
dimensions:
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
  - {key: operating_entity, column: Operating_Entity__c}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: business_type, column: Business_Type__c, type: picklist, allowed_values: [Exisiting, New, New - RFP, Organic Growth]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
coverage_checks:
  - {name: no_operating_entity, sql_predicate: Operating_Entity__c IS NULL, description: Engagement not tagged to Push Canada / Push USA / Stratis (almost all engagements closing before FY2026)}
  - {name: no_service_line, sql_predicate: Type IS NULL, description: Engagement without a service line}
reconcile: {sf_report_id: 00OJQ00000NllSr2AJ, compare_column: RowCount, tolerance: 0}
topic: bd
format: number
aliases: ["number of opportunities", "# of opportunities", "engagements this year", "opportunity count"]
---

Mirrors the PUSH KPI reports "BD - # of Opportunities past FY" (00OJQ00000NllSr2AJ) and "this FY"
(00OJQ00000Nlid32AB): Master Opportunity record type, every stage, dated by CloseDate in the fiscal
year (fiscal = calendar year, January start). FY2025 = 53 engagements (q9).

Caveats:
- The count includes open engagements whose CloseDate is only an expected date, so a current or
  future year's count moves as close dates slip.
- Operating entity is blank on 50 of the 53 FY2025 engagements (q56); use that split from FY2026 on.
- Counts engagements, not projects (Sales Opportunities); never add the two record types together.

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 53
