---
name: gross_revenue_pipeline
version: 1
status: proposed
kind: base
owner: revops
description: Gross value (Amount) of open projects (Sales Opportunities) still being sold, by expected close date, in CAD.
source: {type: sf_report, ref: 00OKc0000014cxhMAA}
confidence: medium
last_verified: 2026-09-29
grain: opportunity
source_table: Opportunity
measure: {agg: sum, column: Amount}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Sales_Opportunity}
  - {field: IsClosed, op: "=", value: false}
time_column: CloseDate
time_semantics: fiscal
currency: {column: Amount, convert: true}
dimensions:
  - {key: stage, column: StageName}
  - {key: service_line, column: Type}
  - {key: operating_entity, column: Operating_Entity__c}
filters:
  - {key: stage, column: StageName, type: picklist, allowed_values: [Discovery, Proposal, Negotiation, Contract]}
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
coverage_checks:
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: Open project with no amount; counted as zero}
topic: revenue
format: currency
aliases: ["pipeline", "forecast amount", "gross revenue forecast", "open pipeline"]
---

This matches the Gross Revenue - Forecast Amount report (00OKc0000014cxhMAA): Sales Opportunity record type, stages Discovery, Presentation, Proposal, Negotiation and Contract, open only. Every open Sales stage in the data (Discovery, Proposal, Contract) is in that list, so `IsClosed = false` is equivalent and also picks up any new open stage.
It is unweighted. The Forecast reports also show "Weighted Forecast" (Amount × Probability), which this metric does not compute.
It is dated by the expected CloseDate, so past fiscal years only contain opportunities that were left open with a stale close date.
Do not add Master Opportunity pipeline to it. Engagement amounts are separate, larger estimates.


## Reviewer note
The equivalence claim ('every open Sales stage in the data is Discovery/Proposal/Contract') has no query behind it. q17 shows active open stages Creds Presentation, Negotiation, Initial Outreach and others. q66 shows 11 moves into Creds Presentation and 2 into Negotiation in 2026-06 to 2026-09. The report lists 'Presentation', not 'Creds Presentation'. So IsClosed=false may pick up stages the report leaves out, or the report may be missing a stage. Either way, the claim of matching the report is unproven. Add a query of open Sales Opportunities by stage. The stage filter's allowed_values also leave out Creds Presentation.

## Sweep
Drafted by the revenue investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 42000
