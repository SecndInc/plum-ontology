---
name: weighted_pipeline_amount
version: 1
status: proposed
kind: derived
owner: revops
description: Open engagement pipeline weighted by each deal's probability (Amount x Probability), in CAD, by expected close date.
source: {type: manual, ref: "pipeline-and-forecast investigation; 'Sum of Weighted Forecast' in report 00OJQ00000NjNrI2AV"}
confidence: medium
last_verified: 2026-09-29
topic: pipeline
format: currency
aliases: ["weighted pipeline", "weighted forecast", "expected revenue", "probability-weighted pipeline"]
formula: 0.1 * open_pipeline_amount_p10 + 0.25 * open_pipeline_amount_p25 + 0.5 * open_pipeline_amount_p50 + 0.75 * open_pipeline_amount_p75 + 0.9 * open_pipeline_amount_p90
inputs: [open_pipeline_amount_p10, open_pipeline_amount_p25, open_pipeline_amount_p50, open_pipeline_amount_p75, open_pipeline_amount_p90]
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
---

**Definition.** For each open engagement (Master Opportunity, `IsClosed = false`): `Amount` (CAD) x `Probability` / 100, summed by fiscal year of `CloseDate`. This is Salesforce's Expected Revenue / "Weighted Forecast" as shown in Forecast - Total (00OJQ00000NjNrI2AV). The Opportunity snapshot has no ExpectedRevenue column and the metric format cannot multiply two columns per row, so the sum is built from probability buckets: every probability used on open engagements at snapshot (0, 10, 25, 50, 75, 90; c95) has a bucket, and 0% contributes nothing.

**Maintenance risk.** If a rep types another probability (open projects already use 80%) or new stages come into use (Stratis stages default to 15, 35, 45%), those deals silently drop out. `open_pipeline_amount` has a coverage check, `probability_not_bucketed`, that flags them; when it fires, add a bucket.

**Record probability, not stage default.** Probability is the rep-editable value. 8 open Proposal engagements differ from the 50% default (c95). For FY2026 Best Case, weighting by record probability gives 12,658,680 CAD and weighting by stage default gives 13,973,680 (c96). We follow Salesforce (record probability); see the open question.

At snapshot, FY2026 weighted: Best Case 12,658,680.12, Commit 14,036,396.4, Pipeline 10,000 (c96). Not reconciled to Forecast - Total, which also counts won delivery stages at 100% and leaves out Creds Presentation.

## Sweep
Drafted by the pipeline investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0
