---
name: project_pipeline_amount
version: 1
status: proposed
kind: base
owner: revops
description: Gross value of open projects (Sales Opportunities not yet won or lost), in CAD, by expected close date.
source: {type: sf_report, ref: 00OKc0000014cxhMAA}
confidence: medium
last_verified: 2026-09-29
topic: pipeline
format: currency
aliases: ["project pipeline", "gross revenue forecast", "forecast amount", "sales opportunity pipeline"]
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
  - {key: forecast_category, column: ForecastCategoryName}
  - {key: service_line, column: Type}
  - {key: operating_entity, column: Operating_Entity__c}
filters:
  - {key: stage, column: StageName, type: picklist, allowed_values: [Discovery, Creds Presentation, Proposal, Negotiation, Contract]}
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
coverage_checks:
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: "Open project with no amount; counted as zero"}
  - {name: no_parent_engagement, sql_predicate: Parent_Opportunity__c IS NULL, description: "Open project not linked to an engagement (7 at snapshot)"}
reconcile: {sf_report_id: 00OKc0000014cxhMAA, compare_column: Amount, tolerance: 0.01}
---

**Definition.** Sum of `Amount` on Sales Opportunities (projects) with `IsClosed = false`, converted to CAD, by fiscal year of `CloseDate`. This is the org's "Gross Revenue - Forecast Amount" report (00OKc0000014cxhMAA: Sales Opportunity, stages Discovery/Presentation/Proposal/Negotiation/Contract, open only). Every open Sales Opportunity at snapshot is in Discovery, Proposal or Contract (c107), so `IsClosed = false` matches the report's stage list today and also keeps working when stages are added.

**Do not add to `open_pipeline_amount`.** 39 of the 46 open projects are children of open engagements; the engagement Amount already covers them (c94). Use this metric for project-level (revenue-side) forecasting, and the engagement metric for BD pipeline.

**Caveat.** The report's standard filter "probability > 0" has no effect today (no open project is at 0%). The report shows native amounts in the running user's currency; this metric converts USD at 0.737 USD per CAD.


## Reviewer note
The reconcile block (tolerance 0.01 against report 00OKc0000014cxhMAA) conflicts with the currency handling. The metric converts USD at a fixed 0.737, but the report shows amounts in the running user's currency at the org's conversion rates. The body sentence 'shows native amounts in the running user's currency' is self-contradictory. Of 46 open projects, 14 are USD. Reconciliation will fail unless it compares native amounts or the rates match. Either reconcile on native Amount or drop or loosen the tolerance. The report's stage and probability filters are also asserted without evidence.

## Sweep
Drafted by the pipeline investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 42000
