---
name: open_pipeline_amount
version: 1
status: proposed
kind: base
owner: revops
description: Gross value of open engagements (Master Opportunities not yet won or lost), in CAD, by expected close date.
source: {type: manual, ref: "pipeline-and-forecast investigation; stage scope adapted from report 00OJQ00000NjNrI2AV (Forecast - Total)"}
confidence: medium
last_verified: 2026-09-29
topic: pipeline
format: currency
aliases: ["pipeline", "open pipeline", "pipeline value", "open deals value", "unweighted pipeline"]
grain: opportunity
source_table: Opportunity
measure: {agg: sum, column: Amount}
base_filters:
  - {field: RecordType.DeveloperName, op: "=", value: Master_Opportunity}
  - {field: IsClosed, op: "=", value: false}
time_column: CloseDate
time_semantics: fiscal
currency: {column: Amount, convert: true}
dimensions:
  - {key: stage, column: StageName}
  - {key: forecast_category, column: ForecastCategoryName}
  - {key: service_line, column: Type}
  - {key: business_type, column: Business_Type__c}
  - {key: owner_title, column: Owner.Title}
filters:
  - {key: stage, column: StageName, type: picklist, allowed_values: [Discovery, Creds Presentation, Proposal, Negotiation, Contract]}
  - {key: forecast_category, column: ForecastCategoryName, type: picklist, allowed_values: [Pipeline, Best Case, Commit]}
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
coverage_checks:
  - {name: amount_missing, sql_predicate: Amount IS NULL, description: "Open engagement with no amount; counted as zero (5 FY2026 Proposal-stage engagements at snapshot)"}
  - {name: zero_probability_open, sql_predicate: Probability = 0, description: "Open engagement at 0% probability; still counted in unweighted pipeline"}
  - {name: probability_not_bucketed, sql_predicate: "Probability NOT IN (0, 10, 25, 50, 75, 90)", description: "Probability with no bucket in weighted_pipeline_amount; that deal is missing from weighted pipeline"}
  - {name: close_date_before_snapshot, sql_predicate: "CloseDate < '2026-09-29'", description: "Open engagement whose expected close date was already past at the snapshot (stale)"}
---

**Definition.** Sum of `Amount` on Master Opportunities (engagements) where `IsClosed = false`, converted to CAD (USD rate 0.737 per CAD, i.e. CAD = USD / 0.737), bucketed by `CloseDate` in the fiscal calendar (FY = calendar year).

**Why Master, not Sales.** The org's forecast report (Forecast - Total, 00OJQ00000NjNrI2AV) and all BD reports count engagements. 39 open Sales Opportunities are children of open Masters, so adding both record types double counts (claim c94). Project-level pipeline is a separate metric: `project_pipeline_amount`.

**Why IsClosed and not the report's stage list.** The report filters stages "Discovery, Presentation, Proposal, Negotiation, Contract, Financial Setup, Kick-off, Project In Progress, Project Completion". That mixes won delivery stages into the forecast and names a stage ("Presentation") that no longer exists, so it misses the 8 open Creds Presentation engagements (c113). Open = `IsClosed = false` covers every open stage, including ones added later. Not reconciled to that report for this reason.

**Caveats.** One engagement holds 15,000,000 of the FY2026 open total (c108), so show the top deals alongside the total. In September 2026 many open engagements were pushed from 2026 into 2027 (c111), so the split between fiscal years moves a lot from one snapshot to the next. Amount is the gross engagement estimate and is usually larger than the sum of its child projects (c94). At snapshot, FY2026 in CAD: Best Case 27,947,360.24, Commit 15,595,996, Pipeline 100,000 (c96).

## Sweep
Drafted by the pipeline investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0
