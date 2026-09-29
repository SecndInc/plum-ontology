---
name: revenue_budget_attainment
version: 1
status: proposed
kind: derived
owner: revops
description: Won engagement value tagged to the budget campaigns as a share of budgeted revenue.
source: {type: sf_report, ref: 00OJQ00000Npum52AB}
confidence: medium
last_verified: 2026-09-29
formula: campaign_won_value / campaign_revenue_budget
inputs: [campaign_won_value, campaign_revenue_budget]
dimensions:
  - {key: budget_client, column: Parent.Name, label: Client budget group}
  - {key: budget_line, column: Name, label: Client and service line}
topic: leads
format: percent
aliases: ["budget attainment", "% of budget", "revenue vs budget", "campaign %"]
---

The "%" formula of Dashboard - Revenue Budget: AMOUNT_WON:SUM / EXP_REVENUE:SUM (null when budget is 0), computed on leaf campaigns only so the budget is not double counted. FY2025: 18,797,607.02 / 20,016,974.

Caveats: the numerator includes engagements tagged to a 2025 campaign that closed in 2026 (4 wins, 4,416,000); engagements not tagged to any campaign never count toward attainment. Compare with [[gross_revenue]] for project-level revenue.

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0.93908335096004021387
