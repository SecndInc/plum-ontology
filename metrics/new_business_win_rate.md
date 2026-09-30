---
name: new_business_win_rate
version: 1
status: proposed
kind: derived
owner: revops
description: Share of decided new-business engagements (New or New - RFP) that were won (count-based).
source: {type: manual, ref: win-rate.md; Business_Type__c}
confidence: medium
last_verified: 2026-09-29
formula: new_business_won_count / new_business_closed_count
inputs: [new_business_won_count, new_business_closed_count]
dimensions:
  - {key: service_line, column: Type}
filters:
  - {key: service_line, column: Type, type: picklist, allowed_values: [Media, Creative, Agency]}
topic: bd
format: percent
aliases: ["new business win rate", "new business success rate", "RFP win rate"]
---

FY2025: 3 won of 11 decided, against 39 of 41 for existing-client engagements (q34). The overall
[[win_rate]] (42 of 52) is driven by existing clients and by wins that were backfilled already won
(q32), so it overstates how often PUSH wins new work. Count-based on purpose: engagement Amount
is dominated by a few very large lost RFP bids (q53).


## Reviewer note
The alias "RFP win rate" is misleading. The metric pools New with New - RFP, giving 3/11 = 27% for FY2025, while the actual RFP win rate is 0/5 (and 0/3 in FY2026). A user asking for the RFP win rate would get the wrong number. Remove the alias or build a separate RFP metric. Also note the small denominators, and that in FY2026 the gap narrows to 9/15 new vs 10/13 existing.

## Sweep
Drafted by the bd investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0.27272727272727272727
