---
name: revenue_budget
version: 1
status: proposed
kind: base
owner: revops
description: Annual gross revenue budget, taken from the root Sales campaign's Expected Revenue for the fiscal year, in CAD.
source: {type: sf_report, ref: 00OJQ00000Npum52AB}
confidence: medium
last_verified: 2026-09-29
grain: campaign
source_table: Campaign
measure: {agg: sum, column: ExpectedRevenue}
base_filters:
  - {field: Type, op: "=", value: Sales}
  - {field: ParentId, op: is_null}
time_column: StartDate
time_semantics: fiscal
currency: {column: ExpectedRevenue, convert: true}
coverage_checks:
  - {name: budget_missing, sql_predicate: ExpectedRevenue IS NULL, description: Root budget campaign without an expected revenue}
topic: revenue
format: currency
aliases: ["budget", "revenue budget", "revenue target", "plan", "revenue plan"]
---

**Definition.** The budget is kept as a tree of Campaigns (Type = Sales). A root campaign per year (for example "2025", StartDate 2025-01-01) has client-level children, and those have client × service-line leaf campaigns (Media, Creative, Special Projects) whose ExpectedRevenue is the budget line. The root's ExpectedRevenue (20,016,974.49 for 2025) equals the sum of the 18 leaves (20,016,974). This metric reads the root, which is the only level with a date.

**Traps.**
- Summing every child campaign double counts: the "New Business" middle node repeats its children's 4,083,759.
- Only Master Opportunities are tagged to budget campaigns (CampaignId), so the Campaign's won-amount rollup is engagement value and also includes FY2026 wins.
- Only a 2025 budget exists. No budget is loaded for FY2026.
- Monthly_Revenue_Plan__c and ForecastingQuota are not usable as targets (test and template data).

## Sweep
Drafted by the revenue investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 20016974.49
