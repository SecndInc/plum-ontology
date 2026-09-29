---
name: leads_converted_of_created
version: 1
status: proposed
kind: base
owner: revops
description: Leads created in the period that have since been converted (created-date cohort), the numerator of lead conversion rate.
source: {type: sf_report, ref: 00OKc0000013SqaMAE}
confidence: medium
last_verified: 2026-09-29
grain: lead
source_table: Lead
measure: {agg: count, column: Id}
base_filters:
  - {field: IsConverted, op: "=", value: true}
time_column: CreatedDate
time_semantics: fiscal
dimensions:
  - {key: lead_source, column: LeadSource}
  - {key: lead_status, column: Status}
  - {key: lead_owner_title, column: Owner.Title}
filters:
  - {key: lead_source, column: LeadSource, type: picklist, allowed_values: [Referral - Team, Referral - Partner, Website, Other, Trade Show, Employee Referral, Advertisement]}
  - {key: lead_status, column: Status, type: picklist, allowed_values: [New Lead, New, Working, Nurturing, Internal Debrief, Qualified]}
coverage_checks:
  - {name: test_lead, sql_predicate: "Company IN ('Test', 'Test Company', 'vtg test')", description: Test records converted}
  - {name: no_opportunity, sql_predicate: ConvertedOpportunityId IS NULL, description: Converted without creating an opportunity}
topic: leads
format: number
aliases: ["converted leads by created month", "cohort conversions"]
---

The Conversion Rate report (00OKc0000013SqaMAE, also Marketing Exec Conversion Rate) groups leads by CreatedDate and computes CONVERTED:SUM / RowCount. This metric is CONVERTED:SUM: leads created in the period with IsConverted = true, whenever they converted. It keeps changing for recent periods as leads convert later.

It differs from [[leads_converted]], which counts by ConvertedDate. Dimensions and filters mirror [[leads_created]] so the two can be divided.

## Sweep
Drafted by the leads investigator in sweep sweep-20260929T2239 on snapshot 20260929T163700Z. Computed at draft time: FY2025: 23
