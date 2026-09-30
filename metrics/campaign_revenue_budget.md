---
name: campaign_revenue_budget
version: 1
status: proposed
kind: base
owner: revops
description: Budgeted (expected) gross revenue for the year, from the service-line budget campaigns, in CAD.
source: {type: sf_report, ref: 00OJQ00000Npum52AB}
confidence: medium
last_verified: 2026-09-29
grain: campaign
source_table: Campaign
measure: {agg: sum, column: ExpectedRevenue}
base_filters:
  - {field: Type, op: "=", value: Sales}
  - {field: Parent.ParentId, op: is_not_null}
time_column: CreatedDate
time_semantics: fiscal
currency: {column: ExpectedRevenue, convert: true}
dimensions:
  - {key: budget_client, column: Parent.Name, label: Client budget group}
  - {key: budget_line, column: Name, label: Client and service line}
coverage_checks:
  - {name: no_budget, sql_predicate: ExpectedRevenue IS NULL, description: Service-line campaign with no budget amount}
topic: leads
format: currency
aliases: ["revenue budget", "budget", "expected revenue", "campaign budget", "target revenue"]
---

Campaigns here are not marketing campaigns. They are a budget tree: root campaign "2025" -> client node (five named clients plus "New Business") -> service-line leaf (Creative / Media / Special Projects). Budget (ExpectedRevenue) is entered on the leaves and repeated on the root (20,016,974.49) and on the "New Business" node (4,083,759). This metric sums **leaves only** (campaigns whose parent has a parent), which gives 20,016,974 for 2025 and avoids the double counting.

The Dashboard - Revenue Budget report sums ExpectedRevenue over all Sales campaigns grouped by parent, so its grand total (44,117,707.49) counts the budget two to three times; its per-client groups match this metric's budget_client dimension.

Time: campaigns have no usable start/end dates (only the root has 2025-01-01..2025-12-31), so CreatedDate is used; all 25 were created 2025-12-17..19, which places the whole 2025 budget in FY2025. When a 2026 budget tree is created this must be revisited (see open question).


## Reviewer note
(1) The base filter Type = 'Sales' is not supported by any evidence shown (q25/q42 do not select Type). (2) time_column = CreatedDate is a poor proxy for budget year: the 2025 budget was created in December 2025, a 2026 tree created in late 2025 would land in FY2025 and double the budget, and FY2026 queries return 0. Derive the budget year from the root campaign (its Name or StartDate/EndDate) instead. The leaf-only logic and the 20,016,974 figure are correct.

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 20016974
