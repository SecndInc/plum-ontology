---
name: push_revenue_margin
version: 1
status: proposed
kind: derived
owner: revops
description: Share of gross project revenue that PUSH keeps as its own net revenue (PUSH revenue divided by gross revenue) on won projects.
source: {type: sf_report, ref: 00OJQ00000NjbSo2AJ}
confidence: medium
last_verified: 2026-09-29
formula: push_revenue / gross_revenue
inputs: [push_revenue, gross_revenue]
dimensions:
  - {key: service_line, column: Type}
  - {key: operating_entity, column: Operating_Entity__c}
  - {key: client, column: Account.Name}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
  - {key: operating_entity, column: Operating_Entity__c, type: picklist, allowed_values: [Push Canada, Push USA, Stratis]}
topic: revenue
format: percent
aliases: ["push revenue percentage", "net revenue margin", "take rate", "margin %"]
---

This is an aggregate ratio: sum of PUSH revenue over sum of Amount, both on won Sales Opportunities in CAD.
The reports' "Sum of PUSH Revenue Percentage" adds up per-record percentages, which is meaningless as a total. Use this ratio instead.
The ratio is biased low for Media, because many won Media projects have PUSH revenue of 0 when the fee % or media spend was never entered (see push_revenue).


## Reviewer note
The only bias mentioned is downward, from Media. There is an upward bias too: Vendor_Cost__c is filled on only 3 of 14 CAD Agency, 11 of 43 CAD Creative and 0 of 9 USD Agency/Creative projects. So PUSH revenue equals Amount on most non-Media work (USD Creative/Agency run at 100%), overstating margin there. The 4 FY2026 CAD Closed Won projects also show PUSH revenue equal to Amount. The blended ratio mixes a low-biased Media share with high-biased Creative/Agency shares, so it moves with service mix. Require a service_line breakdown, or exclude records flagged by coverage checks, and document both biases.

## Sweep
Drafted by the revenue investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0.12906549102944777893
