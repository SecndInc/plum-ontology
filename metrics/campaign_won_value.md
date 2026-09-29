---
name: campaign_won_value
version: 1
status: proposed
kind: base
owner: revops
description: Value of won engagements tagged to the service-line budget campaigns (Salesforce campaign rollup), in CAD.
source: {type: sf_report, ref: 00OJQ00000Npum52AB}
confidence: medium
last_verified: 2026-09-29
grain: campaign
source_table: Campaign
measure: {agg: sum, column: AmountWonOpportunities}
base_filters:
  - {field: Type, op: "=", value: Sales}
  - {field: Parent.ParentId, op: is_not_null}
time_column: CreatedDate
time_semantics: fiscal
currency: {column: AmountWonOpportunities, convert: true}
dimensions:
  - {key: budget_client, column: Parent.Name, label: Client budget group}
  - {key: budget_line, column: Name, label: Client and service line}
coverage_checks:
  - {name: no_won_engagements, sql_predicate: NumberOfWonOpportunities = 0, description: Budget line with no won engagement tagged to it}
topic: leads
format: currency
aliases: ["won against budget", "campaign won amount", "value won opportunities in campaign", "actuals vs budget"]
---

Sum of the standard rollup "Value Won Opportunities in Campaign" over the 18 service-line leaf campaigns, as the Dashboard - Revenue Budget report sums it. Only the leaves carry rollups (root and client nodes are 0), so leaf-only is the same as all campaigns here; the filter is kept for symmetry with [[campaign_revenue_budget]]. FY2025 (the 2025 budget tree): 18,797,607.02.

Caveats:
- The rollup counts every won opportunity whose CampaignId is the campaign, regardless of close date. Of the 41 tagged won engagements, 37 closed in 2025 (14,381,607.02) and 4 in 2026 (4,416,000). See open question on budget-year attribution.
- Only Master Opportunities (engagements) are tagged with campaigns, so this is engagement value, not the project-level [[gross_revenue]]. Engagements not tagged to a campaign are absent.
- The rollup is a stored value refreshed by Salesforce; it is read as of the snapshot.

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 18797607.02
