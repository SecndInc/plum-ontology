---
name: lead_conversion_rate
version: 1
status: proposed
kind: derived
owner: revops
description: Share of leads created in the period that have been converted.
source: {type: sf_report, ref: 00OKc0000013SqaMAE}
confidence: medium
last_verified: 2026-09-29
formula: leads_converted_of_created / leads_created
inputs: [leads_converted_of_created, leads_created]
dimensions:
  - {key: lead_source, column: LeadSource}
  - {key: lead_owner_title, column: Owner.Title}
filters:
  - {key: lead_source, column: LeadSource, type: picklist, allowed_values: [Referral - Team, Referral - Partner, Website, Other, Trade Show, Employee Referral, Advertisement]}
topic: leads
format: percent
aliases: ["lead conversion rate", "conversion rate", "lead-to-opportunity rate"]
---

Mirrors the org's Conversion Rate report: CONVERTED:SUM / RowCount over leads grouped by CreatedDate. FY2025: 23 of 29.

Caveats:
- Until 2026 Q2 nearly every lead was created only to be converted the same day, so the rate is close to 100% and says little about funnel quality. From 2026 Q3 the 100-lead list import drives it down sharply (19 of 143 in 2026 Q3).
- Recent cohorts rise over time as leads convert later; a rate for the current quarter is provisional.
- Conversion does not always create an opportunity; this is lead-to-account conversion, not lead-to-opportunity. Includes test and seed leads, as the report does.


## Reviewer note
(1) The caveat 'until 2026 Q2 … the rate is close to 100%' contradicts the metric's own FY2025 value of 79% (23/29). 2025 Q1 is 3/8 and Q2 is 4/5; only 2025 Q3 to 2026 Q2 are 100%. (2) The alias 'lead-to-opportunity rate' contradicts the caveat that this is lead-to-account conversion. 8 of 46 conversions created no opportunity, so remove that alias.

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 0.79310344827586206897
